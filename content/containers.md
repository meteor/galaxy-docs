---
title: Containers
order: 31
description: Learn how to monitor and manage containers
---

Galaxy containers are packaged environments that are optimized to run Meteor. Each container runs one copy of an app.

<h2 id="usage">Usage</h2>

Each container has CPU and Memory allowance. Galaxy combines the pooled resources of all containers to track overall app performance. You can dive into individual container performance using the graphs on the app's containers page.

<img src="/images/container-item.png" style="margin: 1em 0;"/>

<h3 id="usage">Container sizes</h3>

Since every app has unique architecture and performance characteristics, adjusting the container size helps you meet the specific resource needs of your app.

- Compact: 512 MB/0.5 ECU
- Standard: 1 GB/1 ECU
- Double: 2 GB/2 ECU
- Quad: 4 GB/4 ECU

[ECU](https://aws.amazon.com/ec2/faqs/#hardware-information) is defined by Amazon and is designed to provide a relative measure of processing power. The abbreviation stands for EC2 Compute Unit.

<h3 id="connect-logs">View logs from a specific container</h3>

Accessing the logs from a specific container can help you diagnose any unexpected behavior. Click on the <span class="icon-document"></span> icon near the container name to see the logs from this container.

<h3 id="connect-container">Connect to a specific container</h3>

If you suspect a container is misbehaving or would like to access container-specific information, you may want to connect to that specific container to learn more. From your app's containers page, click on the <span class="icon-share"></span> icon near the container's name to see your app as served by this container.

Since we re-route to a new container when your container is unavailable, you should verify which container subscriptions and remote method calls are being routed through.

You can inspect the `X-Galaxy-Container` [response header](https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading#http-headers) for the `websocket` resource using [Chrome DevTools](https://developer.chrome.com/devtools) or the equivalent in your browser.

<h3 id="kill">Kill a container</h3>

In instances when application code behaves unexpectedly you may want to kill a container. This forcefully stops the  running process and launches your Meteor app in a fresh container.

You can kill a container by going to the designated container on your app's containers page and clicking the kill button below the title.

<h3 id="restarts">Container restarts</h3>

Containers may be restarted for several reasons, such as:

1. A bug in an app caused memory to spike, which caused its container to be killed and then restarted. 
2. The app was working correctly, but it was overwhelmed by the number of connections or the load placed on it. Consequently, its container ran out of memory, was killed and restarted. 
3. Our system underwent an upgrade, and as part of the upgrade, all containers were restarted.

If constant uptime is a core requirement, we recommend running your app on more than 1 container. Since periodic system updates and container restarts can be expected on Galaxy, this can help prevent unwanted downtime. When an app runs on multiple containers, traffic can be routed elsewhere when a single container becomes unresponsive.

Please note that, if you do choose to run a 1 container app, downtime will be unavoidable in the event of a container restart. Due to the need for system maintenance, we cannot guarantee that containers will not be restarted. Containers will also restart when you deploy a new version of your app. 
