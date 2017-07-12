---
title: Troubleshooting
order: 39
description: Learn how to troubleshoot your deploy and get answers to frequently asked questions
---

<h2 id="general-advice">General Advice</h2>

Check these items if you're having trouble with uptime, performance or deployment.
* Your Meteor version. More current versions may resolve issues found in older Meteor versions. While the reverse is rare and generally shouldn't happen, if you're recently upgraded Meteor versions and start having difficulties, consider reverting to your last Meteor version.
* Your container's memory and CPU usage. If your app is running out of memory, you may need to switch to a larger container, use more containers, or refactor your app to use less memory. In the short term, the only guaranteed solution is to scale up and use enough Galaxy resources to exceed your app's memory needs.
* Your app's [logs](/logs.html). While 'All' shows all output, consider breaking it down by tab. If your app is running and struggling before failing, check the 'App' tab. If your app fails when Galaxy tries to build it into a container image, check the 'Service' tab. Note that both can happen simultaneously: the earlier version of your app may be throwing errors, while the recent version created to fix the problem may have a code issue preventing deployment.
* Consider using  [meteor logout](/commands.html) and [meteor login](/commands.html), if your username should be able to deploy but cannot.
* Check <a href="http://github.com/meteor/meteor/issues/">GitHub</a> to see if any related Meteor issue lists workarounds or solutions.
* Check the <a href="https://forums.meteor.com/">forums</a> for related issues and solutions.
* Consider running more than 1 container, or 3 containers to qualify for high-availability status. If you run only one container, that makes the machine your container is running on a single point of failure. In the event of a hardware failure, your app will be down until Galaxy starts it on a new machine.
* Email <a href="mailto:support@meteor.com">support</a>. To minimize the back-and-forth, please send in the name of the affected app, the conditions that trigger the issue (confirmed or suspected), steps to reproduce, and relevant logs. Try to resolve errors listed in the logs before writing in. If your app's container is running with the error, please try to leave it in the running state for our team to examine.

Note that code-level review lies outside the scope of Galaxy's support. If this is important to you, consider [Meteor Development Support](/support.html).

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

<h2 id="deployment-failure">Deployment failures</h2>

A deployment failure means that you or your system cannot build a container to deploy your app.

If you should be able to deploy but cannot, try using the [commands](/commands.html) `meteor logout` and `meteor login`.

If our system tried to build a container to deploy your app but failed, the failure will be noted in your logs.

Check the [Logs](/logs.html) tab to see if your app is crashing. The 'Service' tab may show you important build errors, in addition to the stopping and starting of containers.

Most of the time, the key to a solution will be found in the exception or error messages. Keep iterating on code fixes and deployments until the error goes away, a new error appears, or your app deploys successfully.

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

<h2 id="memory-issues">Memory issues or Out-of-Memory errors</h2>

Memory issues are frequently indicated in your logs. The log message `The container has run out of memory. A new container will be started to replace it.` means that the container running your application tried to get more memory than was allocated to it. Containers in this state are automatically killed.

If you continue to run your app as is, the only way to prevent it from dying is to allocate resources with more than enough memory. A working solution may include more containers, bigger containers, or both.

You can see memory utilization in the [container view](/containers.html) of your app. If you see memory spiking to 90% or more, that is almost certainly the problem. Your app may be experiencing memory issues even if your metrics never reach this level, if your container is running out of memory and crashing before our metrics can register the increase.

You can upgrade to Galaxy Professional and use [Meteor APM](/apm-getting-started.html) in order to get a more exact sense of your app's memory usage over time, among other things. Using Meteor APM, your app's memory usage can be profiled for periods as short as 1 hour, and as long as 30 days.

You can also use npm modules to profile your memory usage and pinpoint erratic memory usage. The <a href="https://www.npmjs.com/package/heapdump">heapdump</a> npm module is one such module, though you'll need to transfer the file it creates to a place like S3 for download and closer examination. Another such module is <a href="https://www.npmjs.com/package/memwatch-next">memwatch-next</a>. While Galaxy does not officially support specific third-party modules, the community has found the use of modules of this type to be helpful.

In the short term, you may need to [scale up](/scaling.html). You can always scale back down after refactoring your app to consume less memory.

<h2 id="else">If none of the above worked</h2>

Consider if [Meteor APM](/apm-getting-started.html) might help you to identify your issue.

Confirm you're able to run your app locally. If possible, try to duplicate the issues in your app. This may involve running your app locally for longer than usual and simulating traffic, to recreate real-world conditions.

Try adding more exception handlers, as an uncaught exception may cause your app to crash.

Finally, try printing more information to your logs. If you can't spot any error messages or warnings in your app's current form, printing more information may help you to troubleshoot. Any minor changes to your code to enable can always be disabled once you've diagnosed the issue.

If you believe your issue is related to Meteor, you can [file a bug](https://github.com/meteor/meteor/blob/devel/Contributing.md#reporting-a-bug-in-meteor) or add a comment to an existing bug to pursue resolution. Consider searching [Stack Overflow](https://stackoverflow.com/questions/tagged/meteor) for a solution, if applicable.
