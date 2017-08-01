---
title: Troubleshooting
order: 37
description: Learn how to troubleshoot your deploy and get answers to frequently asked questions
---

<h2 id="general-advice">General Advice</h2>

Check these items if you're having trouble with uptime, performance or deployment.
* Your Meteor version. More current versions may resolve issues found in older Meteor versions. While the reverse is rare and generally shouldn't happen, if you're recently upgraded Meteor versions and start having difficulties, consider reverting to your last Meteor version.
* Your container's memory and CPU usage. If your app is running out of memory, you may need to switch to a larger container, use more containers, or refactor your app to use less memory. In the short term, the only guaranteed solution is to scale up and use enough Galaxy resources to exceed your app's memory needs.
* Your app's [logs](/logs.html). While 'All' shows all output, consider breaking it down by tab. If your app is running and struggling before failing, check the 'App' tab. If your app fails when Galaxy tries to build it into a container image, check the 'Service' tab. Note that both can happen simultaneously: the earlier version of your app may be throwing errors, while the recent version created to fix the problem may have a code issue preventing deployment. If you find a specific error, check our [error types](/error-types.html) article for more information.
* Consider using  [meteor logout](/commands.html) and [meteor login](/commands.html), if your username should be able to deploy but cannot. If you're using a deployment token, considering reissuing yours, in case it has expired.
* Check <a href="http://status.meteor.com/">status.meteor.com</a> in case Galaxy issues are affecting your deployment.
* Check <a href="http://github.com/meteor/meteor/issues/">GitHub</a> to see if any related Meteor issue lists workarounds or solutions.
* Check the <a href="https://forums.meteor.com/">forums</a> for related issues and solutions.
* Consider running more than 1 container, or 3 containers to qualify for [high-availability](/high-availability.html) status. If you run only one container, that makes the machine your container is running on a single point of failure. In the event of a hardware failure, your app will be down until Galaxy starts it on a new machine.
* Email <a href="mailto:support@meteor.com">support</a>. To minimize the back-and-forth, please send in the name of the affected app, the conditions that trigger the issue (confirmed or suspected), steps to reproduce, and relevant logs. Try to resolve errors listed in the logs before writing in. If your app's container is running with the error, please try to leave it in the running state for our team to examine.

Note that code-level review lies outside the scope of Galaxy's support. If this is important to you, consider [Meteor Development Support](/support.html).

<h2 id="five-hundred-two-errors">502 errors</h2>

You may see a 502 error with the message `Registered endpoints failed to handle the request` when you try to visit your URL. This means that the request failed, despite the fact that our system thought there was a healthy container at the beginning of the request. See our [error types](/error-types.html) article for more information.

<h2 id="five-hundred-three-errors">503 errors</h2>

Your app may throw a 503 error and show `Service Unavailable: No healthy endpoints to handle the request` when you try to visit your URL.  This means no healthy containers are currently available to serve your app. See our [error types](/error-types.html) article for more information.

<h2 id="deployment-failure">Deployment failures</h2>

A deployment failure means that you or your system cannot build a container to deploy your app.

If you should be able to deploy but cannot, try using the [commands](/commands.html) `meteor logout` and `meteor login`.

If our system tried to build a container to deploy your app but failed, the failure will be noted in your logs.

Check the [Logs](/logs.html) tab to see if your app is crashing. The 'Service' tab may show you important build errors, in addition to the stopping and starting of containers.

Most of the time, the key to a solution will be found in the exception or error messages. Keep iterating on code fixes and deployments until the error goes away, a new error appears, or your app deploys successfully.

<h2 id="else">If none of the above worked</h2>

Consider if [Meteor APM](/apm-getting-started.html) might help you to identify your issue.

Confirm you're able to run your app locally. If possible, try to duplicate the issues in your app. This may involve running your app locally for longer than usual and simulating traffic, to recreate real-world conditions.

Try adding more exception handlers, as an uncaught exception may cause your app to crash.

Finally, try printing more information to your [logs](/logs.html). If you can't spot any error messages or warnings in your app's current form, printing more information may help you to troubleshoot. Any minor changes to your code to enable can always be disabled once you've diagnosed the issue. You can look up specific error types in our [error types](/error-types.html) article. 

If you believe your issue is related to Meteor, you can [file a bug](https://github.com/meteor/meteor/blob/devel/Contributing.md#reporting-a-bug-in-meteor) or add a comment to an existing bug to pursue resolution. Consider searching [Stack Overflow](https://stackoverflow.com/questions/tagged/meteor) for a solution, if applicable.
