---
title: Containers
order: 31
description: Learn how to monitor and manage containers
---

Galaxy containers are packaged environments that are optimized to run Meteor. Each container runs one copy of an app.

<h3 id="usage">Usage</h3>

Each container has CPU and Memory allowance. Galaxy combines the pooled resources of all containers to track overall app performance. You can dive into individual container performance using the graphs on the app's containers page.

<img src="/images/container-item.png" style="margin: 1em 0;"/>

<h4 id="usage">Container sizes</h4>

Since every app has unique architecture and performance characteristics, adjusting the container size helps you meet the specific resource needs of your app.

- Compact: 512 MB/0.5 ECU
- Standard: 1 GB/1 ECU
- Double: 2 GB/2 ECU
- Quad: 4 GB/4 ECU

<h3 id="connect-logs">View logs from a specific container</h3>

Accessing the logs from a specific container can help you diagnose any unexpected behavior. Click on the <span class="icon-document"></span> icon near the container name to see the logs from this container.


<h3 id="connect-container">Connect to a specific container</h3>

If you suspect a container is misbehaving or would like to access container-specific information, you may want to connect to that specific container to learn more. From your app's containers page, click on the <span class="icon-share"></span> icon near the container's name to see your app as served by this container.

Since we re-route to a new container when your container is unavailable, you should verify which container subscriptions and remote method calls are being routed through.

You can inspect the [`X-Galaxy-Container` response header](https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading#http-headers) for the `websocket` resource using [Chrome DevTools](https://developer.chrome.com/devtools) or the equivalent in your browser.

<h3 id="kill">Kill a container</h3>

In instances when application code behaves unexpectedly you may want to kill a container. This forcefully stops the  running process and launches your Meteor app in a fresh container. Kill a container by going to the designated container on your app's containers page and clicking the kill button below the title.

<h3 id="icon-meanings">Icon meanings</h3>

There are several types of icons you may see when deploying, which each have a specific meaning.

<img src="/images/green_circle.png" style="margin: 1em 0;"/>

The green full circle indicates that your container is running, and passed its health checks.

For an app that should be running, this is the icon you want to see.

<img src="/images/green_circle_outlined.png" style="margin: 1em 0;"/>

The outlined green full circle means that your app's status is starting, updating, or stopping. It should move out of this status fairly quickly.

<img src="/images/empty_circle_outlined.png" style="margin: 1em 0;"/>

The outlined green empty circle means that your app is starting, but has encountered an issue.

This can mean:
- your app has never successfully run all its containers (at least, not since the last time it was stopped)
- it is currently running (possibly unhealthy) containers fewer in number than the amount it is trying to run

Possible reasons for this include a build failure, or a crash upon startup.

<img src="/images/red_circle.png" style="margin: 1em 0;"/>

The red full circle indicates that all containers your app is trying to run are unhealthy. Your app won't be able to load or run successfully until the issue is resolved.

<img src="/images/gray_circle.png" style="margin: 1em 0;"/>

The gray full circle indicates that all containers in your app are stopped.

You can check the Activity Log in your account's right-hand sidebar to determine which users completed this action.









