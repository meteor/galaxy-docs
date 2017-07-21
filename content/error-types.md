---
title: Error Types
order: 38
description: Learn how to deal with common error types
---

<h2 id="five-hundred-two-errors">502 errors</h2>

You may see a 502 error with the message `Registered endpoints failed to handle the request` when you try to visit your URL. This means that the request failed, despite the fact that our system thought there was a healthy container at the beginning of the request.

This often happens because your backend wasn't able to respond, when communicating with our proxy servers. You may need to profile your app to determine the cause of this error. Check the [Logs](/logs.html) tab to potentially find out more information about the issue.

<h2 id="five-hundred-three-errors">503 errors</h2>

Your app may throw a 503 error and show `Service Unavailable: No healthy endpoints to handle the request` when you try to visit your URL.  This means no healthy containers are currently available to serve your app.

Potential reasons for this include:
- all containers are unhealthy, because they are all stuck in a CPU loop
- no containers are running, because they are stopped or because every container crashed (especially if the total number of your containers is 1, and your app hasn't had time to restart)
- your build failed, if this is the first time you're deploying a container for that app or if the only other available containers built successfully but are unhealthy

The most common cause of the 503 error is a problem in your code that prevents deployment - a [deployment failure](#deployment-failure). Check the [Logs](/logs.html) tab to potentially find out more information about the issue.

A common reason that your app may be crashing on startup is that your `MONGO_URL` variable is missing or is set incorrectly. You can verify what `MONGO_URL` Galaxy is using by going to the app's dashboard and choosing the settings tab. To learn how to set it correctly, check the following resources:

* [Environment variables](/environment-variables.html) will show you how to set up your `settings.json` file.
* [This compose.io article](https://www.compose.io/articles/meteors-new-galaxy-and-the-perfectly-composed-companion/) explains the settings for `MONGO_URL` and `MONGO_OPLOG_URL` in detail.

If you believe your `MONGO_URL` is set correctly, try the following:

* Check the app dashboard and verify the app status is green (healthy).
* Run `dig +show [your app's domain]` in the terminal and verify that its CNAME points to Galaxy. You can learn how to set up DNS [here](/dns.html).
  * If you are in the US region, your CNAME should point to `us-east-1.galaxy-ingress.meteor.com`
  * If you are in the EU region, your CNAME should point to `eu-west-1.galaxy-ingress.meteor.com`
  * If you are in the Asia-Pacific region, your CNAME should point to `ap-southeast-2.galaxy-ingress.meteor.com` 

If you recently changed your DNS settings, you may need to wait for the new records to propagate. DNS changes often propagate within 30 minutes (depending on the TTL configured for the record set), but in some cases it can take up to 24 hours. Contact your DNS provider if you think there is a problem.

<h2 id="package-error">Module missing or npm error</h2>

This usually indicates that the module or package working locally in your application is not working after deployment. While we don't offer support for the use of specific third-party packages, an explanation may help you to troubleshoot.

When you deploy an app, we bundle node_modules into it; npm packages that are required on the client side get built into the bundle uploaded to Galaxy. Galaxy doesn't need to run `npm install` for client side bundling to work.

Note that dynamic requires may cause issues. An example would be using `require(variable)` instead of `require("fixed-name")`. To avoid this, put `require("react/package.json")` somewhere in your app's code to ensure it gets bundled.

You may find the `meteor npm install --save package` command to be helpful, where `package` should be replaced with the name of the package you are trying to install. This will add the package to your package.json file, using the latest version and any needed dependencies.

Alternatively, you can specify the package name directly in your package.json file, with the version number and any necessary dependencies.

A common type of npm error will show up during the build process, in the 'All' or 'Service' tab of your logs. If you were deploying an example package using version number 1.0.0, it would show up as follows:

`Failed at the example@1.0.0 install script 'prebuild --install'`

This means that this package failed to install, using that version. A long term solution may involve either communicating with the package maintainer, or the Meteor release manager, to massage the issue. In the short term, the best immediate solution usually involves changing the version - either of the package version, or of the Meteor version, if builds suddenly start failing upon upgrading to a new Meteor version.

If you happen to be using an older version of Meteor, consider updating to a more recent version, as that has been known to resolve issues in the past.

If neither of those solutions work, try removing the package entirely, and making any necessary adjustments to your app to accommodate this change.

A recommended method for emulating Galaxy is to run locally with `--production`. The way node_modules are pulled in is different on a remote deployment to a server (including Galaxy) than when building locally. The `--production` setting will minimize and concatenate all the JS into one file.

<h2 id="package-not-compatible">Package not compatible</h2>

Apps that contain local packages with NPM dependencies which include binary components will fail to deploy to Galaxy by default. You'll know you've run into this issue when a `meteor deploy` to Galaxy fails with `[package] is not compatible with architecture 'os.linux.x86\_64` (where [package] is replaced by the package name that is causing the issue).

Version 1.2.1 of Meteor (and higher) provides the `METEOR_BINARY_DEP_WORKAROUND` environment variable for Galaxy deployment. To deploy your app to Galaxy using the workaround:

1. Upgrade your app to Meteor version 1.2.1 or higher with `meteor update`
2. Next, deploy to galaxy by setting the `METEOR_BINARY_DEP_WORKAROUND=t` environment variable. An example deploy command would look like `METEOR_BINARY_DEP_WORKAROUND=t DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy ...` , replacing `...` with the rest of your deployment command (URL, settings, etc.).

If you are uncertain if this matches your situation, you can use [this test app](https://github.com/zol/meteor-bignum-test) to reproduce the error and confirm a fix.

