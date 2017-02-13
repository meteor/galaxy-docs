---
title: Scaling
order: 40
description: Learn how to improve your app’s performance by scaling
---

Scaling and sizing your application is specific to the architecture and performance characteristics of your app. As apps grow they often require more resources to perform well. Galaxy accommodates growth by offering vertical and horizontal resource scaling. Scaling with Galaxy happens without downtime so your users will not experience service interruption.

<h3 id="what-to-look-for">What to look for</h3>

We recommend that you scale when your app’s container usage exceeds either 70% memory, 80% CPU, or consistently spikes to 100% CPU. Use Galaxy’s performance graphs to track your resource usage over time. 

<img src="images/email-galaxy-performance-graphs-600x468.jpg" style="">

<h3 id="how-to">How to scale</h3>

By default new applications are deployed to Compact containers. Compact containers are appropriate for small apps. For large codebases we recommend that you run your app on Standard containers for best performance.

You may need to change your garbage collection settings for optimal performance. Garbage collection, in this context, refers to automatic memory management, where the garbage refers to memory occupied by objects that are no longer in use by the program and can be freed up for general use.

Garbage collection settings for Meteor apps should be based on how much memory is available to the container. Since all Meteor apps run in a Node.js environment, it's important to know that Node's default settings effectively limit you to slightly over 1 GB (1400 MB) of memory. This is the amount of heap size that can be used by the main process, by default.

You can manage the amount of memory dedicated to garbage collection by setting the environment variable $NODE_OPTIONS. To set aside 2000 MB for garbage collection, for example, you would set $NODE_OPTIONS="--max-old-space-size=2000".

Users of Standard/Compact sized containers may want to lower this setting to prevent OOM (out-of-memory) errors. More significantly, users of Double/Quad containers are advised to set the flag to higher than its default of 1400 MB in order to use all their memory.

**Vertical scaling** increases your app's available resources by expanding the size of each container. Use this method of scaling when your app requires more CPU or RAM than the current container size can handle.

Vertical scaling works best for one-time changes, when you won't need to change container sizes often. If handling a single user/connection needs more memory/CPU than will fit in the currently used container size, you'll need to vertically scale, even if the usage doesn't last for long. You should set $NODE_OPTIONS higher than the default of 1400 MB to take full advantage of larger-sized containers.

Vertical scaling restarts all your containers. Note that larger containers may take slightly longer to scale up or restart.

<img src="images/container-upsize.gif" style="">

<img src="images/email-scale-up.gif" style="float:right">
**Horizontal scaling** increases your app’s available resources by adding more containers. This is useful when sudden increases in usage or traffic cause your app to be less performant. Horizontal scaling does not restart your containers.

A good rule of thumb is to use the smallest container size that can handle a single user's load, and scale horizontally beyond this.

If you need to scale up and down gradually and frequently, horizontal scaling is your best option.
