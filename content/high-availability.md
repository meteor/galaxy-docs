---
title: High-availability
order: 41
description: Learn how to make your app fault tolerant by enabling high-availability
---

High-availability increases the likelihood that your app stays up in the event of unforeseen container, machine, or availability zone failures. We recommend high-availability for all business critical and production apps. Galaxy supports high-availability by default.  Just run three or more Standard containers to enable it for your app.

<h3 id="turn-on">Turn high-availability on</h3>

1. Check if your app has enabled high-availability on the app overview page <img src="images/galaxy-app-overview.png" style="width: 400px; margin: 1em;">
2. Change the container size to Standard or larger in your app settings <img src="images/container-upsize.gif" style="display: block; width: 300px; margin: 1em;">
3. Add three or more containers on the app overview page <img src="images/email-scale-up.gif" style="display: block; margin: 1em;">
4. Verify that it's enabled via the UI <img src="images/ss-high-availability-on.png" style="display: block; width: 300px; margin: 1em;">

<h3 id="turn-on">How we do it</h3>

For deployments with three or more Standard containers, Galaxy will distribute an app's containers to a different availability zones in the same region. Dividing infrastructure across multiple data centers ensures that high-availability apps are fault tolerant.
