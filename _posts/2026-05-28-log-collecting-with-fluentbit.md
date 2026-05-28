---
layout: post
title:  "Log Collecting with fluentbit"
date:   2026-05-28
---

> This is convert from a sharing of meetup on 13 Mar, 2025 (Slide: [https://docs.google.com/presentation/d/1-BgxJXsCRrv8jV0UqEyucalbBCLfyH2RfTPsMJ_uJ2k/edit?usp=sharing](https://docs.google.com/presentation/d/1-BgxJXsCRrv8jV0UqEyucalbBCLfyH2RfTPsMJ_uJ2k/edit?usp=sharing))

## Introducing fluent bit

Fluentd project is a CNCF Graduated project, aim for centralized log collection.
Fluentd is written in Ruby & C with tons of plugins.

Fluent bit is a sub-project of Fluentd. It is completely written with C and come with much lower memory footprint compare with Fluentd.

| Attribute    | Fluentd                                    | Fluent Bit                                     |
|--------------|--------------------------------------------|------------------------------------------------|
| Scope        | Containers / Servers                       | Embedded Linux / Containers / Servers          |
| Language     | C & Ruby                                   | C                                              |
| Memeory      | Greater than 60 MB                         | Approximately 1 MB                             |
| Performance  | Medium Performance                         | High Performance                               |
| Dependencies | Built as a Ruby Gem, depends on other gems | Zero dependencies, unless required by a plugin |
| Plugins      | Over 1,000 external plugins available.     | Over 100 built-in plugins available.           |
| License      | Apache License v2.0                        | Apache License v2.0                            |

Source: https://docs.fluentbit.io/manual/about/fluentd-and-fluent-bit

I would suggest Fluentd for enrich or modify logging records while fluent bit for deploy on node for edge log collection.

## Benefit of using Fluent Bit

Fluent Bit can be used to collect log from different location and send to one single centralized location for better query later.
Fluent Bit is also able to parse log content to extract metadata.
With the metadata, user would be able to modify or filter out the log records.
The cost of ingesting log is currently around 0.5 per GiB nowadays.

### Reason for pre-processing

Filtering and pre-processing would also reduce time in query the specific log you want.
Filtering out log would help in preventing the storage become full in short time for on-perm deployment.

## Common Use case

### Direct to Destination

![Direct to Destination](/assets/2026/05/28/FluentBit-1.png)

If the log message content is not too complicated and the amount of log generated is constant,
sending the log directly to sink would be simplest.

### Combined with Fluentd

![Combined with Fluentd](/assets/2026/05/28/FluentBit-2.png)

Instead of sending to destination directly, it is possible to send the log to a centralized Fluentd with output type `forward`.
Log sent to fluentd could further process (e.g. remove all sensitive information).
This is mainly for the condition of having different teams responsible in different parts.

### Combined with ELK

![Combined with ELK](/assets/2026/05/28/FluentBit-3.png)

If ELK stack is being used currently, instead of removing everything, it possible to only replacing Filebeat with Fluent Bit.
Fluent Bit provide support on output to Logdash directly.
This way could help lower to the hard work for migration.

### Buffer with Kafka and Post-Process with Fluentd

![Buffer with Kafka and Post-Process with Fluentd](/assets/2026/05/28/FluentBit-4.png)

It is possible for having log generating in spike.
In this condition, Kafka could be leveraged as buffer and using Fluentd / Fluent bit to write to the final destination sink.

## How fluent bit works?

![Fluent Bit key components](/assets/2026/05/28/FluentBit-5.png)

### Input

Input is used for get where do the log located.

Common plugins:

- tail
- systemd
- forward

Ref: https://docs.fluentbit.io/manual/pipeline/inputs

### Parser

Parser is used for parsing the log and extract out metadata.

Common plugins:

- JSON
- Logfmt
- Regexp
- Multiline

Ref: https://docs.fluentbit.io/manual/pipeline/parsers

### Filter

Filter would be the place where modify and removal is performed.

Common plugins:

- grep
- Cloud metadata (aws/kubernetes)
- parser
- record modifier

Ref: https://docs.fluentbit.io/manual/pipeline/filters

### Output

Output would put the log into the sink.

Common plugins:

- Object Storage (AWS S3 / GCP GCS / Azure Blob Storage)
- ElasticSearch / OpenSearch
- Graylog
- Loki
- OpenTelemetry
- Syslog server
- Kafka
- Forward (for sending to fluent bit / fluentd)

## Reference

- Fluentd Website: [https://www.fluentd.org/](https://www.fluentd.org/)
- Fluent Bit Manual: [https://docs.fluentbit.io/manual](https://docs.fluentbit.io/manual)
- Fluent Bit GitHub: [https://github.com/fluent/fluent-bit](https://github.com/fluent/fluent-bit)
- Builtin Config: [https://github.com/fluent/fluent-bit/tree/master/conf](https://github.com/fluent/fluent-bit/tree/master/conf)
