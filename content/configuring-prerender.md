---
title: Enable SEO with pre-render
order: 17
description:
---

Todo:
Why pre-rendering?

Galaxy provides an integrated pre-rendering service, Prerender.io, to improve your Meteor app’s search engine optimization (SEO). The Prerender.io service is included as part of Galaxy and does not incur an additional cost.

See [https://prerender.io/](https://prerender.io/) for more information about the Prerender.io service.

## Enabling Prerender.io SEO for your application

Add the mdg:seo package to your application.

`$ meteor add mdg:seo`

When you deploy this application to Galaxy, Galaxy will automatically enable Prerender.io service for the application.

## Using your own Prerender service

You can use your own Prerender service by configuring it in the application settings. If Galaxy finds a pre-configured Prerender service, then Galaxy will not configure the application to use Galaxy's integrated Prerender.io service.
