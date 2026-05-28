---
layout: post
title:  "HKOSCon 2019 Website Phase 1 Release"
date:   2019-01-31
---

Team 404 Busters has finished on the building and deployment of the HKOSCon 2019 website.

HKOSCon 2019 Website is now online, check it out at [https://hkoscon.org/2019/](https://hkoscon.org/2019/)

In here, on behalf of Team 404 Busters, I would like to give some insight of content and technical update on the website

## Content Update

### Form for Call for Paper

The call for paper has been started. A new CFP page has been added to the website. Check it out and submit your paper on [https://hkoscon.org/2019/cfp/](https://hkoscon.org/2019/cfp/)

## Technical Update

### Upgrade of Node.js

As the LTS of node.js 10 is active since 30 Oct 2018, we have upgrade node.js to version 10. With the new version of V8 and new ES standard implements, we are able to roll faster in development progress.

### Migrate to nuxt.js

We have migrated from the custom-built site generator to [nuxt.js](https://nuxtjs.org/), so that we are able to enjoy the great ecosystem of Vue and great SEO from the pre-rendering jobs done by nuxt.js. Also, nuxt.js brings the Webpack 4 and babel 7 into the building and providing a smaller bundle and better performance.

### Migrate to Bulma

Previously, we are using [materialize](https://materializecss.com/) for the website and since [Bulma](https://bulma.io/) is pure css framework, we are able to get more control on the component and reduce the rendering time of the browser.

### Change sass implements

Since the old node-sass packages require a cpp binding, which brings inconveniently to developers and force them to install make, python, and g++. Moreover, `node-sass` is single-thread and blocking when rendering, this results in slow performance. As a result, we switch to `sass` which is an implementation written in [Dart](https://www.dartlang.org/) and compile to js and provided better performance than before.

## Call for contributor

Last but not least, we greatly welcome anyone come and contributes to the website. You can find the release repository at [https://gitlab.com/hkoscon/2019](https://gitlab.com/hkoscon/2019) and the development repository, which is owned by Team 404 Busters, at [https://gitlab.com/404busters/hkoscon/hkoscon-2019](https://gitlab.com/404busters/hkoscon/hkoscon-2019)
