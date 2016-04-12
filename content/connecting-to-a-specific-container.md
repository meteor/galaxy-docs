---
title: Containers
order: 13
description: Learn how to assess performance and troubleshoot containers.
---

Todo:
- Container basics: Galaxy runs on containers. virtual machines...
- Container performance graphs
- Connecting to a specific container
- Killing containers

### Why?

- You suspect that a specific container is misbehaving.
- You would like to access container-specific information, for example from the [meteor-connstats](https://pcarrier.github.io/meteor-connstats) package.

### How?

From your app's containers page, click on the <span class="icon-share"></span> icon near the container's name to see your app as served by this container.

Since we re-route to a new container when your container is unavailable, you should verify which container subscriptions and remote method calls are being routed through.

You can [inspect the `X-Galaxy-Container` response header](https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading#http-headers) for the `websocket` resource using [Chrome DevTools](https://developer.chrome.com/devtools) or the equivalent in your browser.
