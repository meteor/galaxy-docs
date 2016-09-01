---
title: Troubleshooting
order: 6
description: Learn how to troubleshoot your deploy and get answers to frequently asked questions
---

<h2 id="503-errors">503 errors</h2>

The 503 error ("Service Unavailable: No healthy enpoints to handle the request.") indicates that our image builder was not able to successfully create a container, when attempting to deploy. We would suggest that you test and debug this locally, as this usually indicates a problem in your code that prevents deployment.

<h2 id="502-errors">502 errors</h2>

A 502 error (“Bad Gateway”) typically means that no containers have successfully started your app or that all app containers have become unhealthy (usually caused by CPU load).

A common cause of the former is that your `MONGO_URL` variable is missing or is set incorrectly. You can verify what `MONGO_URL` Galaxy is using by going to the app's dashboard and choosing the settings tab. To learn how to set it correctly, check the following resources:

* [How do I set Environment Variables?](https://galaxy.meteor.com/help/setting-environment-variables) will show you how to set up your `settings.json` file.
* [This compose.io article](https://www.compose.io/articles/meteors-new-galaxy-and-the-perfectly-composed-companion/) explains the settings for `MONGO_URL` and `MONGO_OPLOG_URL` in detail.

If you believe your `MONGO_URL` is set correctly, try the following:

* Check the app dashboard and verify the app status is green (healthy)
* Check the logs tab to see if the app is crashing. If so, look at the exception to determine the issue.
* Run `dig +show [your app's domain]` in the terminal and verify that its CNAME points to `galaxy-ingress.meteor.com`. You can learn how to set up DNS [here](configuring-dns). If you recently changed your DNS settings, you may need to wait for the new records to propagate. DNS changes often propagate within 30 minutes (depending on the TTL configured for the record set), but in some cases it can take up to 24 hours. Contact your DNS provider if you think there is a problem.


<h2 id="package-not-compatible">Package not compatible</h2>

Apps that contain local packages with NPM dependancies which include binary components will fail to deploy to Galaxy by default. You'll know you've run into this issue when a `meteor deploy` to Galaxy fails with `[package] is not compatible with architecture 'os.linux.x86\_64` (where [package] is replaced by the package name that is causing the issue).

Version 1.2.1 of Meteor (and higher) provides the `METEOR_BINARY_DEP_WORKAROUND` environment variable for Galaxy deployment (this does *not* work with meteor.com free hosting). To deploy your app to Galaxy using the workaround:

1. Upgrade your app to Meteor version 1.2.1 or higher with `meteor update`
2. Next, deploy to galaxy by setting the `METEOR_BINARY_DEP_WORKAROUND=t` environment variable. An example deploy command would look like `METEOR_BINARY_DEP_WORKAROUND=t DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy ...` , replacing `...` with the rest of your deployment command (URL, settings, etc.).

If you are uncertain if this matches your situation, you can use [this test app](https://github.com/zol/meteor-bignum-test) to reproduce the error and confirm a fix.

<h2 id="package-error">Module missing or npm error</h2>

This usually indicates that the module or package working locally in your application is not working after deployment. While third-party packages are unsupported, an explanation of our system may assist you in your troubleshooting.
 
When you deploy an app, we bundle node_modules into it. npm packages that are required on the client side get built into the bundle uploaded to Galaxy. As a result, Galaxy doesn't need to use npm install for client side bundling to work.

If you are using dynamic requires - for example, require(variable) instead of require("fixed-name") - that may cause issues. To avoid this, put require("react/package.json") somewhere in your application code to make sure it gets bundled.

If you happen to be using an older version of Meteor, consider updating to a more recent version, as that has been known to resolve issues in some cases.

You may also find these commands helpful:
meteor npm --save invariant
meteor npm --save object-assign

A recommended method to mimic Galaxy is to run locally with --production. The way node_modules are pulled in is different on a remote deployment to a server (including Galaxy) than when building locally. The --production setting will minimize and concatenate all the JS into one file, which should assist you in the troubleshooting process.



