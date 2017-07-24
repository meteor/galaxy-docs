---
title: Memory Issues
order: 39
description: Learn how to troubleshoot memory issues
---

<h2 id="memory-issues">Memory issues or Out-of-Memory errors</h2>

Memory issues are a common but often poorly understood problem. In order to effectively resolve them, you may need to profile your app and iterate on your code in order to improve memory usage.

Memory issues are frequently indicated in your [logs](/logs.html). Check your logs for clues about the source of the issue.

If you see the log message `The container has run out of memory. A new container will be started to replace it,` this means that the container running your application tried to get more memory than was allocated to it. Containers in this state are automatically killed.

If you continue to run your app as is, the only way to prevent it from dying is to allocate resources with more than enough memory. A working solution may include more containers, bigger containers, or both.

You can see memory utilization in the [container view](/containers.html) of your app. If you see memory spiking to 90% or more, that is almost certainly a problem you'll need to troubleshoot.

Your app may be experiencing memory issues even if your metrics never reach this level, if your container is running out of memory and crashing before our metrics can register the increase.

You can upgrade to Galaxy Professional and use [Meteor APM](/apm-getting-started.html) in order to get a more exact sense of your app's memory usage over time, among other things. Using Meteor APM, your app's memory usage can be profiled for periods as short as 1 hour, and as long as 30 days.

You can also use npm modules to profile your memory usage and pinpoint erratic memory usage. The <a href="https://www.npmjs.com/package/heapdump">heapdump</a> npm module is one such module, though you'll need to transfer the file it creates to a place like S3 for download and closer examination. Another such module is <a href="https://www.npmjs.com/package/memwatch-next">memwatch-next</a>. While Galaxy does not officially support specific third-party modules, the community has found the use of modules of this type to be helpful.

In the short term, you may need to [scale up](/scaling.html). You can always scale back down after refactoring your app to consume less memory.
