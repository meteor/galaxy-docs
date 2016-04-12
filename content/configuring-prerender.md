---
title: SEO with prerender
order: 17
description:
---

<h2 id="prerender">Prerender.io integration</h2>

Galaxy provides an integrated pre-rendering service, Prerender.io, to optimize your Meteor app for search engines (SEO). The Prerender.io service is included as part of Galaxy at no additional cost. See [https://prerender.io/](https://prerender.io/) for more information about the Prerender.io service.

<h3 id="prerender-use">Add prerendering</h3>

Type `$ meteor add mdg:seo` in your app's directory to add the prerender package. Galaxy will then automatically  enable the Prerender.io service when you deploy your app.

<h3 id="prerender-alternative">Using your own Prerender service</h3>

You can use your own Prerender service by configuring it in the application settings. If Galaxy finds a pre-configured Prerender service, then Galaxy will not configure the application to use Galaxy's integrated Prerender.io service.
