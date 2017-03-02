---
title: Logging
order: 45
description:
---

Logging should be your first stop when troubleshooting any Galaxy issue. When working with Galaxy support, an agent will usually begin by consulting your logs. If a clearly noted issue has been marked there, you can save time by reading the logs and iterating on your code until the error goes away.

You can reach the logs dashboard by clicking on your app, then clicking the "Logs" tab.

<img src="/images/logs_section.png" style="margin: 1em 0;"/>

<h3 id="tabs">Tabs</h3>

There are several logging tabs you can click, below the "Logs" tab itself. These are:

- All: for the combined view.
- App: for application-specific messages and errors.
- Service: for messages generated during the build process.
- Errors: exclusively for errors, which are flagged in red in other tab views.

Breakdown by tab will be especially useful if you have multiple containers running, and are regularly deploying.

<h4 id="all">All</h4>

Every message and error will be shown here.

If your containers are working correctly and have been up for a while, this may be the most convenient tab to check. If you have multiple containers and builds succeeding and failing, this view may be too crowded.

<h4 id="app">App</h4>

Any messages or errors thrown by your app will be shown here, assuming our image builder was able to build your app and successfully launch it.

Check this to see what your app is doing during normal operations. You can always add lines to your code to print what your app is doing for added visibility.

<h4 id="service">Service</h4>

If your app isn't successfully deploying, this is the tab you'll want to check. Our image builder tries to build your app into a container; if it fails, the failure will be noted here.

A <a href="https://github.com/meteor/meteor/issues/8136">common error</a> is that a particular version of a package wasn't able to be built by our image builder. If this happens to your app, the output will frequently include a line like this, after the package install line:

`node-pre-gyp install --fallback-to-build`

A working solution in such cases is usually to revert to an earlier version of the package. 

<h4 id="errors">Errors</h4>

Errors will be shown in this tab. Check to see if there are any outstanding errors if your app is malfunctioning.

<h3 id="storage">Storage</h3>

Logs are stored for the past week. If any errors or messages thrown by your app are older than 1 week, they won't appear in your logs.

If you'd like to explore more permanent log storage options, contact <a href="mailto:support@meteor.com">support@meteor.com</a>.

