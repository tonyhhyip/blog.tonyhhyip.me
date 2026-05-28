---
layout: post
title:  "The rebuild of HKOSCon 2019 website whitepaper"
date:   2019-04-01
---

P.S. As due to some of the HKOSCon committee cannot stand for the original version, you are reminded that this is **not** a publishment of the HKOSCon official

Recently, the conference committee has updated and released the result of the call for paper on the website. And we, Team 404 Busters, found the website performance in some remote area and old mobile device is pretty poor, this leads us to deeply reflect on the design of the website.

## The goal of the re-design

The main goal of the re-build is to provide a great experience to everyone, no matter how poor is the network and how old is your mobile browser.

### The reason behind the problem

In order to archive the goal, we have made a lot of research and benchmarking in different network condition and device, and for a more accurate result, we measure it in a packed underground metro in both Hong Kong and Taipei during the peak hour.

The data collected during the research tell us the reason behind the issues: it is because the parsing engine of the browser is too slow while we current render the website with Vue.js. To overcome this, we have to make the page to be as simple as possible, so that the parsing engine wouldn’t take long to parse all the code.

## Solution

In order to overcome the problem, we have tried on making the whole page is in one small HTML with some style tag only. However, it stills takes much time to download for the poor network condition.

During the research, we come up with a new idea after reading [an article published by Flutter](https://medium.com/flutter-io/hummingbird-building-flutter-for-the-web-e687c2a023a8). Since Hummingbird is not yet published, so we decided using Rust Web Assembly to write our own implements of the Flutter embedding API.

With the power of Flutter, we are able to render the page as rendering engine itself while skipping the parsing process. The result is so great, the benchmark on metro test has dropped down to less than 0.1s for loading the whole page. After finish loading the page, you can drop offline and continue to browse the page.

![Masked Conference Brand New Landing Page due to the complaint of logo and conference name (ask me if you want to see the original one)](/assets/2019/04/01/HKOSCon2019-1.webp)

## Conclusion

Thanks for reading tills here and have a Happy April Fool. We are having some re-design of the page so that it would be able to reflect our brand image and core value.

Please give us a star to our repository if you walk by. And don’t be shy to submit any new idea and improvement to us.

[https://gitlab.com/404busters/hkoscon/hkoscon-2019](https://gitlab.com/404busters/hkoscon/hkoscon-2019)
