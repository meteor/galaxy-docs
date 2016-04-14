---
title: App
order: 11
description: Learn how to monitor and manage your app
---

<h2 id="overview">Overview</h2>

Get a snapshot of the realtime status of your app and resource usage over time on the app overview page.

<img src="/images/galaxy-app-overview.png" style="width: 600px"/>

<h3 id="usage">Usage</h3>

Your app's resource usage is determined by the size and number of containers. Galaxy combines the resources of all containers to determine the resources available to your app. Customers can view app resource usage on the app overview page.

<img src="/images/email-galaxy-performance-graphs-600x468.jpg" style="width: 300px"/>

<h2 id="containers">Containers</h2>

Galaxy containers are packaged environments for Meteor apps. Dive into individual container performance metrics on the container page. Read more in the [container article](/container.html).

<img src="/images/galaxy-app-container.png" style="width: 600px"/>

<h2 id="logs">Logs</h2>

Galaxy records the output of your app's logs in addition to printing operational logs for your deployment. Logs are aggregated from all containers and ordered chronologically.

<img src="/images/galaxy-app-logs.png" style="width: 600px"/>

You can [filter logs from a specific container](/containers.html#connect-logs) on the app container page.

<h2 id="settings">Settings</h2>

<h3 id="stop">Meteor Settings</h3>

View the meteor settings and environment variables in your app's `settings.json` file. Learn more in the [environment variables article](/environment-variables.html).

<h3 id="stop">Domains and SSL</h3>

Manage the custom domains that you can use to access your app and SSL encryption. Learn more about adding [custom domains](/custom-domains.html)  and [enabling SSL encryption](/encryption.html).

<h3 id="stop">Container Size</h3>

Scale vertically by adjusting the size of your containers. Learn more about [scaling your app](/scaling.html).

<h3 id="stop">Stopping & deleting apps</h3>

**Stopping an app** shuts down all of its containers. When stopped, the app's settings are preserved and organization members may continue to view app logs and performance metrics.

**Deleting an app** shuts down all containers and removes the app from your Galaxy account.
