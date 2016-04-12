---
title: Troubleshooting
order: 6
description: Learn how to troubleshoot your deploy and get answers to frequently asked questions
---

# Troubleshooting 502 errors

A 502 error (“Bad Gateway”) typically means that no containers have successfully started your app or that all app containers have become unhealthy (usually caused by CPU load).

A common cause of the former is that your `MONGO_URL` variable is missing or is set incorrectly. You can verify what `MONGO_URL` Galaxy is using by going to the app's dashboard and choosing the settings tab. To learn how to set it correctly, check the following resources:

* [How do I set Environment Variables?](https://galaxy.meteor.com/help/setting-environment-variables) will show you how to set up your `settings.json` file.
* [This compose.io article](https://www.compose.io/articles/meteors-new-galaxy-and-the-perfectly-composed-companion/) explains the settings for `MONGO_URL` and `MONGO_OPLOG_URL` in detail.

If you believe your `MONGO_URL` is set correctly, try the following:

* Check the app dashboard and verify the app status is green (healthy)
* Check the logs tab to see if the app is crashing. If so, look at the exception to determine the issue.
* Run `dig +show [your app's domain]` in the terminal and verify that its CNAME points to `galaxy-ingress.meteor.com`. You can learn how to set up DNS [here](configuring-dns). If you recently changed your DNS settings, you may need to wait for the new records to propagate. DNS changes often propagate within 30 minutes (depending on the TTL configured for the record set), but in some cases it can take up to 24 hours. Contact your DNS provider if you think there is a problem.



#Deploy fails with Package not compatible
Apps that contain local packages with NPM dependancies which include binary components will fail to deploy to Galaxy by default. You'll know you've run into this issue when a `meteor deploy` to Galaxy fails with
 _"[package] is not compatible with architecture 'os.linux.x86\_64"_ (where [package] is replaced by the package name that is causing the issue).

Version 1.2.1 of Meteor (and higher) provides the `METEOR_BINARY_DEP_WORKAROUND` environment variable for Galaxy deployment (this does *not* work with meteor.com free hosting). To deploy your app to Galaxy using the workaround:

1. Upgrade your app to Meteor version 1.2.1 or higher with `meteor update`
2. Next, deploy to galaxy by setting the `METEOR_BINARY_DEP_WORKAROUND=t` environment variable. An example deploy command would look like `METEOR_BINARY_DEP_WORKAROUND=t DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy ...` , replacing `...` with the rest of your deployment command (URL, settings, etc.).

If you are uncertain if this matches your situation, you can use [this test app](https://github.com/zol/meteor-bignum-test) to reproduce the error and confirm a fix.
