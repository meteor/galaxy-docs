---
title: Getting Started with APM
order: 51
description: Learn how to start with Monti APM
---

This guide will help you get started with Monti APM, to better understand how your app behaves and identify areas for improvement.

## Install and Configure Monti APM

1. Run `meteor add montiapm:agent` inside your Meteor project.
2. Once you have deployed your app, enable "Galaxy Professional" from the app settings page.

## Migrate from Meteor APM

If you are already using Meteor APM, you can migrate the APM agent to Monti APM by following the steps below:

1. Run `meteor add montiapm:agent` inside your Meteor project.
2. Run `meteor remove mdg:meteor-apm-agent` inside your Meteor project.

> You don't need to invoke `Monti.connect()` in your app. The configuration for Monti APM is done automatically during the deployment process.


Now your app will send information to Monti APM. Visit [Galaxy](https://galaxy.meteor.com) to find links to your Monti APM dashboard.  Links can be found in the following places:

- In the *Performance* area on the App Overview & Containers pages.
- In the *Galaxy Professional* area on the App Settings page.

For more information on Monti APM and how to get started, visit the [Monti APM Docs](https://docs.montiapm.com/getting-started).