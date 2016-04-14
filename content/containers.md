---
title: Containers
order: 11
description: Learn how to monitor and manage containers
---

Galaxy containers are packaged environments that are optimized to run Meteor. Each container runs one copy of an app.

<h3 id="usage">Usage</h3>

Each container has CPU and Memory allowance. Galaxy combines the pooled resources of all containers to track overall app performance. Users can dive into individual container performance using the graphs on the app's containers page.

<img src="/images/container-item.png" style="margin: 1em 0;"/>

<h4 id="usage">Container sizes</h4>

Since every app has unique architecture and performance characteristics, adjusting the container size helps you meet the specific resource needs of your app.

- Compact: 512 MB/0.5 ECU
- Standard: 1 GB/1 ECU
- Double: 2 GB/2 ECU
- Quad: 4 GB/4 ECU

<h3 id="connect-specific">Connect to a specific container</h3>

If you suspect a container is misbehaving or would like to access container-specific information, you may want to connect to that specific container to learn more. From your app's containers page, click on the <span class="icon-share"></span> icon near the container's name to see your app as served by this container.

Since we re-route to a new container when your container is unavailable, you should verify which container subscriptions and remote method calls are being routed through.

You can [inspect the `X-Galaxy-Container` response header](https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading#http-headers) for the `websocket` resource using [Chrome DevTools](https://developer.chrome.com/devtools) or the equivalent in your browser.

<h3 id="kill">Kill a container</h3>

In instances when application code behaves unexpectedly you may want to kill a container. This forcefully stops the  running process and launches your Meteor app in a fresh container. Kill a container by going to the designated container on your app's containers page and clicking the kill button below the title.
