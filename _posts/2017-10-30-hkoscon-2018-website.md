---
layout: post
title:  "Upgrade of Hong Kong Open Source Conference 2018 Website"
date:   2017-10-30
---

As the Call for Communities of Hong Kong Open Source Conference 2018 (HKOSCon 2018) has been released, Team 404 Busters has started working on the HKOSCon 2018 website. We keep the main tools from 2017 website in order to reduce the learning curve and time to work on it. In this article, I would state the part we change in the website building pipeline.

## Upgrade of Node.js

As the LTS of node.js 8 is going to active on 31 Oct 2017, we have upgrade node.js to version 8. With the new node.js 8 supporting `async/await`, we replace the promise chain with async and await in the build script. This help in easier to maintain and debug. nvmrc file is added for the nvm users.

## Change in building

### Webpack Module and Babel Preset

Starting from Webpack 2, webpack come with support of ES6 module import and export, Babel module converting can be removed if only ES6 module is used. After the upgrade, babel-preset-env is used to replace the old preset which would apply the plugins on the environment requested.

### Remove of Gulp

Gulp did bring a hard time for us to maintain and having customisation in 2017. In 2018, we build all the assets with a single build script, which contain the call of webpack API and nunjucks only. The build time is 1 minutes faster by average on Travis CI.

### Using Hash Assets Filename

The output filename has added a content hash which help in skipping the step of waiting cache invalid in Cloudflare. To make add the assets easier, a new parameter `assets` is passed into the pages.

## Change in Development

### Change in command

At before, starting up the development server require for 2 parallel process. After the upgrade, it just required for 1 single process to handle all of these. In the new version, a setup command `yarn setup` is required for setting up environment for development. It would be required to run for every time the entry in webpack config has been changed. After the setting up, the only command required is `yarn dev`, the dev server would be ready for you at 8080 port.

### Rebuild of development server

The development server was painful with different problem in hot reload and restart, specially pair with gulp. We have removed the old `webpack-dev-server` and replaced with an `express` server with different middlewares. `webpack-dev-middleware` and `webpack-hot-middleware` is used to replace the old webpack dev server building. Page is render as template in order to save the time in rebuilding pages.

### Bundling stylesheet

As gulp is removed, all scss files would be import by webpack with `sass-loader`. With webpack hot middleware, the style can be hot-reload and display on browser immediately.

### Conclusion

We have worked hard to improve on the website. Please open an issue or pull request on the [Github repository](https://github.com/404busters/hkoscon-2018) if you find something can still be improved. Also the call for communities is lived now, you may visit and apply for it at [here](https://hkoscon.org/2018/cfc.html).
