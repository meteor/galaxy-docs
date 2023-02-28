---
title: App
order: 30
description: Learn how to monitor and manage your app
---

<h2 id="overview">Overview</h2>

Get a snapshot of the realtime status of your app and resource usage over time on the app overview page.

<img src="/images/galaxy-app-overview-1.png" style="width: 780px"/>

You may also want to consider using [Meteor APM](/apm-getting-started.html) for more insight.

<h3 id="usage">Usage</h3>

Your app's resource usage is determined by the size and number of containers. Galaxy combines the resources of all containers to determine the resources available to your app. Customers can view app resource usage on the app overview page.

<img src="/images/email-galaxy-performance-graphs-600x468.jpg" style="width: 380px"/>

<h2 id="containers">Containers</h2>

Galaxy containers are packaged environments for Meteor apps. Dive into individual container performance metrics on the container page. Read more in the [containers](/containers.html) and [container environment](/container-environment.html) articles.

<img src="/images/galaxy-app-container.png" style="width: 880px"/>

<h2 id="logs">Logs</h2>

Galaxy records the output of your app's logs in addition to printing operational logs for your deployment. Logs are aggregated from all containers in your app and ordered chronologically. Read more in the [logs](/logs.html) article.

<img src="/images/galaxy-app-logs.png" style="width: 780px"/>

You can [filter logs from a specific container](/containers.html#connect-logs) on the app container page.

<h3 id="icon-meanings">Icons</h3>

Icons in your app's dashboard will display the current state of your app.

<img src="/images/green_circle.png" style="margin: 1em 0;"/>

The green full circle indicates that your app's container set is running, and passed its health checks. For an app that should be running, this is the desired state.

<img src="/images/green_circle_outlined.png" style="margin: 1em 0;"/>

The outlined green full circle means that your app's container set status is starting, updating, or stopping. It should leave this state fairly quickly.

<img src="/images/empty_circle_outlined.png" style="margin: 1em 0;"/>

The outlined green empty circle means that your app's container set has experienced an issue while starting.

This means your app has never successfully run all its containers, or has not since the last time it was stopped, and your app is currently running containers fewer in number than the amount it is trying to run (the containers it is running may also be unhealthy). You will only see this icon upon your app's initial deploy, or when restarting it from a stopped state.

Potential causes include a build failure caused by an inability to build your code as written, or a regular crash upon startup. The problem will need to be resolved before your app can successfully run.

<img src="/images/red_circle.png" style="margin: 1em 0;"/>

The red full circle indicates that all the containers your app is trying to run are unhealthy. Your app won't be able to load or run successfully until you resolve the issue.

<img src="/images/gray_circle.png" style="margin: 1em 0;"/>

The gray full circle indicates that you stopped your entire app, and the process of stopping is complete. By extension, it also means that all the containers in your app's container set are stopped.

If necessary, you can check the Activity Log in your account's right-hand sidebar to determine which user(s) completed this action. You can always restart your app, at any time.

<h2 id="settings">Settings</h2>

<h3 id="stop">Meteor Settings</h3>

View the meteor settings and environment variables in your app's `settings.json` file. Learn more in the [environment variables article](/deploy-setup.html#env-variables).

<h3 id="stop">Domains and SSL</h3>

Manage the custom domains that you can use to access your app and SSL encryption. Learn more about adding [custom domains](/custom-domains.html)  and [enabling SSL encryption](/encryption.html).

<h3 id="stop">Container Size</h3>

Scale vertically by adjusting the size of your containers. Learn more about [scaling your app](/scaling.html).

<h3 id="stop">Stopping & deleting apps</h3>

**Stopping an app** shuts down all of its containers. When stopped, the app's settings are preserved and organization members may continue to view app logs and performance metrics.

**Deleting an app** shuts down all containers and removes the app from your Galaxy account.
