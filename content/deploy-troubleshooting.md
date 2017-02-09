---
title: Troubleshooting
order: 15
description: Learn how to troubleshoot your deploy and get answers to frequently asked questions
---

<h2 id="general-advice">General Advice</h2>

Check these items if you're having trouble with uptime, performance or deployment.
- Your Meteor version. More current versions may resolve issues found in older Meteor versions. While the reverse is rare and generally shouldn't happen, if you're recently upgraded Meteor versions and start having difficulties, consider reverting to your last Meteor version.
- Your container's memory and CPU usage. If your app is running out of memory, you may need to either switch to a larger container or refactor your app to use less memory. In the short term, the only guaranteed solution is to use a container large enough to handle all your app's memory needs.
- Your app's logs. While 'All' shows all errors, consider breaking it down by tab. If your app is running and struggling before failing, check the 'App' tab. If your app is crashing before deployment and never successfully launching, check the 'Service' tab. Note that both can happen simultaneously: the earlier version of your app may be throwing errors, while the recent version created to fix the problem may have a code error preventing deployment. In that case, 'Service' will be more helpful.
- Check GitHub to see if your issue is listed with a suggested workaround or solution.
- Consider running more than 1 container, if uptime for your app is mission-critical and you're currently running a single container.
- Write in to support. To minimize the back-and-forth, please send in the name of the affected app, the conditions that trigger the issue (confirmed or suspected), steps to reproduce, and relevant logs. Try to resolve errors listed in the logs before writing in.

Note that code-level review lies outside the scope of Galaxy's support.

<h2 id="503-errors">503 errors and Deployment failures</h2>

The 503 error will show `Service Unavailable: No healthy endpoints to handle the request` when you try to visit your URL. This indicates that our image builder was not able to successfully create a container, when attempting to deploy. This usually indicates a problem in your code that prevents deployment.

You may see the 503 error temporarily, if trying to resolve a URL in your browser within 1-2 minutes of issuing your deploy command. If you've waited 15 minutes or more, the problem will almost surely not resolve itself by waiting longer.

Begin by checking the logs tab to see if your app is crashing. The 'Service' tab will show build errors. Most of the time, the key to a solution will be found in the exception or error messages. Keep iterating on code fixes and deployments until the error goes away, a new error appears, or your app deploys successfully.

A common cause of the 503 error is that your `MONGO_URL` variable is missing or is set incorrectly. You can verify what `MONGO_URL` Galaxy is using by going to the app's dashboard and choosing the settings tab. To learn how to set it correctly, check the following resources:

* [Environment variables](/environment-variables.html) will show you how to set up your `settings.json` file.
* [This compose.io article](https://www.compose.io/articles/meteors-new-galaxy-and-the-perfectly-composed-companion/) explains the settings for `MONGO_URL` and `MONGO_OPLOG_URL` in detail.

If you believe your `MONGO_URL` is set correctly, try the following:

* Check the app dashboard and verify the app status is green (healthy).
* Run `dig +show [your app's domain]` in the terminal and verify that its CNAME points to `galaxy-ingress.meteor.com`. You can learn how to set up DNS [here](configuring-dns). If you recently changed your DNS settings, you may need to wait for the new records to propagate. DNS changes often propagate within 30 minutes (depending on the TTL configured for the record set), but in some cases it can take up to 24 hours. Contact your DNS provider if you think there is a problem.

<h2 id="package-error">Module missing or npm error</h2>

This usually indicates that the module or package working locally in your application is not working after deployment. While third-party packages are unsupported, an explanation may help you to troubleshoot.
 
When you deploy an app, we bundle node_modules into it; npm packages that are required on the client side get built into the bundle uploaded to Galaxy. Galaxy doesn't need to use `npm install` for client side bundling to work.

Note that dynamic requires may cause issues. An example would be using `require(variable)` instead of `require("fixed-name")`. To avoid this, put `require("react/package.json")` somewhere in your app's code to ensure it gets bundled.

You may find these commands to be helpful:
`meteor npm --save invariant`
`meteor npm --save object-assign`

If you happen to be using an older version of Meteor, consider updating to a more recent version, as that has been known to resolve issues in the past.

A recommended method is to mimic Galaxy and run locally with `--production`. The way node_modules are pulled in is different on a remote deployment to a server (including Galaxy) than when building locally. The `--production` setting will minimize and concatenate all the JS into one file.

<h2 id="package-not-compatible">Package not compatible</h2>

Apps that contain local packages with NPM dependancies which include binary components will fail to deploy to Galaxy by default. You'll know you've run into this issue when a `meteor deploy` to Galaxy fails with `[package] is not compatible with architecture 'os.linux.x86\_64` (where [package] is replaced by the package name that is causing the issue).

Version 1.2.1 of Meteor (and higher) provides the `METEOR_BINARY_DEP_WORKAROUND` environment variable for Galaxy deployment. To deploy your app to Galaxy using the workaround:

1. Upgrade your app to Meteor version 1.2.1 or higher with `meteor update`
2. Next, deploy to galaxy by setting the `METEOR_BINARY_DEP_WORKAROUND=t` environment variable. An example deploy command would look like `METEOR_BINARY_DEP_WORKAROUND=t DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy ...` , replacing `...` with the rest of your deployment command (URL, settings, etc.).

If you are uncertain if this matches your situation, you can use [this test app](https://github.com/zol/meteor-bignum-test) to reproduce the error and confirm a fix.

<h2 id="memory-issues">Memory issues or Out-of-Memory errors</h2>

Memory issues are frequently indicated in your logs. The log message `The container has run out of memory. A new container will be started to replace it.` means that the container running your application tried to get more memory than was allocated to it. Containers in this state are automatically killed.

You can see memory utilization in the container view of your app. Check the 5 minute, 1 hour, 1 day and 30 day views; if you see memory spiking to 90% or more, that is almost certainly the problem.

If your container is running out of memory, you may need to [scale up](/scaling.html) to fix this. You can always scale back down after refactoring your app to consume less memory. If you continue to run your app as is, the only way to prevent it from dying is to allocate containers with more than enough memory.

You can also use npm modules to profile your memory usage and pinpoint erratic memory usage. The heapdump npm module is one such module, though you'll need to transfer the file it creates to a place like S3 for download and closer examination. Another such module is memwatch-next.

While Galaxy does not officially support the use of third-party modules, our community has found the use of memory-profiling npm modules to be helpful. Check the GitHub page of your module for more information.





