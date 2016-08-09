---
title: SEO with Prerender
order: 17
description:
---

<h3 id="prerender">Prerender.io integration</h3>

Galaxy provides an integrated pre-rendering service, Prerender.io, to optimize your Meteor app for search engines (SEO). The Prerender.io service is included as part of Galaxy at no additional cost. See [https://prerender.io/](https://prerender.io/) for more information about the Prerender.io service.

<h4 id="prerender-use">Add prerendering</h4>

Type `$ meteor add mdg:seo` in your app's directory to add the prerender package. Galaxy will then automatically enable the Prerender.io service when you deploy your app. You will see a prerender token in your application's logs. 

<h4 id="prerender-details">Administration and settings</h4>

The prerendering service offered by Galaxy is designed to provide a shared service across all apps in Galaxy, with pre-determined caching policies and no need for per app management or administration through the service. There is no login available to users. We currently offer a guarantee of at most 4 days as the cache freshness policy.

If you need to trigger your own recaches, for specific pages, then you should use your own prerender.io service.

<h4 id="prerender-alternative">Using your own Prerender service</h4>

You can use your own Prerender service by configuring it in the application settings file (settings.json). If Galaxy finds a pre-configured Prerender service, then Galaxy will not configure the application to use Galaxy's integrated Prerender.io service.
