---
title: CDN
order: 43
description: Learn how to configure a CDN with Galaxy
---

Configuring a CDN with Galaxy is largely the same as [using a CDN with Meteor in any context](http://guide.meteor.com/deployment.html#cdn). Once you’ve setup the CDN with your application as its origin (for example, a [CloudFront](https://aws.amazon.com/cloudfront/) distribution named xyz.cloudfront.net which proxies for www.exampleapp.com), you can tell Meteor to serve static JS and CSS assets from the CDN with

```
WebAppInternals.setBundledJsCssPrefix(
  'https://xyz.cloudfront.com');
```

If you have static assets such as images used in your templates (for example `<img src="foo.png" />`) that you would also like to have cached by the CDN, you'll need to include the CDN prefix in the image tag. Combined with the previous example, the image would tag become `<img src="https://xyc.cloudfront.com/foo.png" />`. We recommend you create a helper that does this for you only in production.


<h3 id="forward-cookies">Forwarding Cookies from the CDN</h3>

In general, you don’t want to forward cookies from your CDN, as it leads to overcaching. Specifically, you should not forward the `galaxy-sticky` cookie, as it will result in caching one copy of every asset per container that you application runs.
