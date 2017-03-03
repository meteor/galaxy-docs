---
title: CDN
order: 43
description: Learn how to configure a CDN with Galaxy
---

Configuring a CDN with Galaxy is largely the same as [using a CDN with Meteor in any context](http://guide.meteor.com/deployment.html#cdn).

In general, you don’t want to forward cookies from your CDN, as it leads to overcaching. Specifically, you should not forward the `galaxy-sticky` cookie, as it will result in caching one copy of every asset per container that you application runs. However, you do want to configure your CDN to forward query string parameters.

Once you’ve set up the CDN with your application as its origin (for example, a [CloudFront](https://aws.amazon.com/cloudfront/) distribution named d12345678.cloudfront.net which proxies for www.exampleapp.com), you can tell Meteor to serve static JS and CSS assets from the CDN with

```
WebAppInternals.setBundledJsCssUrlRewriteHook((url) => {
  return `https://d12345678.cloudfront.net${url}&_g_app_v_=${process.env.GALAXY_APP_VERSION_ID}`;
});
```

The `_g_app_v_` query parameter tells Galaxy to only send this request to containers running the same version as the container that served the app HTML to you.  Since different versions of your app are likely to have different versions of JS and CSS (and thus different bundled filenames), you want to ensure that the CDN looks at a container that will actually contain the file in question.

This isn't a concern without a CDN, because Galaxy uses cookies to ensure that the JS/CSS request is routed to the same container as the HTML if possible, and Meteor knows to refresh the whole page if that's no longer possible.  But because you should not configure your CDN to forward cookies, the normal mechanism does not work and the `_g_app_v_` technique is necessary.

If you have static assets such as images used in your templates (for example `<img src="foo.png" />`) that you would also like to have cached by the CDN, you'll need to include the CDN prefix and `_g_app_v_` query parameter in the image tag too. Combined with the previous example, the image would tag become `<img src="https://d12345678.cloudfront.com/foo.png?_g_app_v_={process.env.GALAXY_APP_VERSION_ID}" />`. We recommend you create a helper that does this for you only in production.
