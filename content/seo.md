---
title: SEO with Prerender
order: 42
description:
---

<h2 id="prerender">Prerender.io integration</h2>

Galaxy provides an integrated pre-rendering service, Prerender.io, to optimize your Meteor app for search engines (SEO). The Prerender.io service is included as part of Galaxy at no additional cost. See [https://prerender.io/](https://prerender.io/) for more information about the Prerender.io service.

<h2 id="prerender-use">Add prerendering</h2>

Type `$ meteor add mdg:seo` in your app's directory to add the prerender package. Galaxy will automatically enable the Prerender.io service when you deploy your app. 

If you're using the spiderable package, please remove it, since the prerender and spiderable packages are not compatible with each other.

<h2 id="confirmation">Confirmation</h2>

You can check to see if your changes took hold by running the <a href="https://curl.haxx.se/download.html">curl</a> command. If the URL of your app is www.example.com, you would run this command:

`curl 'https://www.example.com/?_escaped_fragment_='`

Confirm that the output contains the text that your site shows once the JS is run. If you only see a header and a reference to a script file, you may need to troubleshoot.

<h2 id="testing">Testing</h2>

It's easy to run a test prerender server on your machine to check for errors. [As descibed at prerender](https://prerender.io/documentation/test-it), first run these commands:

```
git clone https://github.com/prerender/prerender.git
cd prerender
npm install
node server.js
```

If your site is named example.com, then open another shell and use the command:

`curl 'http://localhost:3000/https://example.com'`

You should then see any relevant error messages, if you're experiencing an issue.

<h2 id="prerender-details">Administration and Cache Freshness</h2>

The prerendering service offered by Galaxy is designed to provide a shared service across all apps in Galaxy, with pre-determined caching policies and no need for per app management or administration through the service.

We currently offer a guarantee of at most 4 days as the cache freshness policy. There is no login available to users. 

If you need to trigger your recaches for specific pages, or need to recache more frequently, we recommend that you set up your own prerender.io service.

<h2 id="prerender-alternative">Using your own Prerender service</h2>

You can use your own Prerender service by configuring it in the application settings file (settings.json). If Galaxy finds a pre-configured Prerender service, then Galaxy will not configure the application to use Galaxy's integrated Prerender.io service.

The token and service URL can be configured via your application's settings.json like so:
```
{
  "PrerenderIO": {
    "serviceUrl": "https://service.prerender.io",
    "token": "yourtoken"
  }
}
```
If you intend to continue using Prerender's hosted service with your own token, we recommend setting the `serviceUrl` as above explicitly because the npm package supporting prerender defaults to a non-secure `http` url.

Refer to the [package documentation](https://github.com/dferber90/meteor-prerender/) for more information
