---
title: Puppeteer and common cases base images
order: 17
description: Aside from the base image, we identified common used libraries and we have created official images supporting this usage
---

Most Galaxy users run their app with the [default base image](/base-image-packages.html).  This provides a basic environment for running most Meteor apps.

But, for some use cases this is not enough, and you don't want/don't know how to create a custom image to meet your needs.

We do provide some basic images for common uses, like:


<h2 id="build">Puppeteer (meteor/galaxy-puppeteer) </h2>

This image bundles every library puppeteer needs to be able to run. You can use it by doing the follow on your settings.json:

```json
{
  "galaxy.meteor.com": {
    "env": { "MONGO_URL": "mongodb://..." },
    "baseImage": {
      "repository": "meteor/galaxy-puppeteer",
      "tag": "latest"
    }
  }
}
```
It's also expected that your usage of puppeteer uses the following flags:

```js
const browser = await puppeteer.launch({
    args: [
    '--no-sandbox',
    '--disable-setuid-sandbox',
    '--disable-dev-shm-usage'
    ]
});
const page = await browser.newPage();
await page.goto("https://www.google.com");
```
