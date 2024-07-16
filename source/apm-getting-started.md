---
title: Getting Started with APM
order: 51
description: Learn how to start with Monti APM
---

This guide will help you get started with Monti APM, to better understand how your app behaves and identify areas for improvement.

## Installation

1. Run `meteor add montiapm:agent` inside your Meteor project.
2. Once you have deployed your app, enable "Galaxy Professional" from the app settings page.

### Migrate from Meteor APM

Your app cannot have both Meteor APM and Monti APM agents enabled at the same time.

This means that you'll need to remove the `mdg:meteor-apm-agent` package from your app.

1. Run `meteor add montiapm:agent` inside your Meteor project to install the Monti APM agent.
2. Run `meteor remove mdg:meteor-apm-agent` inside your Meteor project to remove the old Meteor APM agent.

### Migrate from existing Monti APM configuration

In order to use our provided Monti APM app, you will need to remove any existing Monti APM configuration from your app.

To ensure that Monti APM will connect with our provided app, you will need to:

1. Ensure there's no `"monti"` settings in your Meteor settings file.
2. Ensuring you don't call `Monti.connect()` in your code.

## Monitoring your app

After connecting your app to Monti APM following the steps above, your app will send information to Monti APM. Visit [Galaxy 2](https://galaxy-beta.meteor.com) to find links to your Monti APM dashboard.

Links can be found in your app overview page.

<img src="/images/apm-view-app.gif" style="margin: 1em 0;"/>

## Learn More
For more information on Monti APM and how to get started, visit the [Monti APM Docs](https://docs.montiapm.com/getting-started).