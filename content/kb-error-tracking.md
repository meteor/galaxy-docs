---
title: Error Tracking
order: 65
---

## Introduction

Meteor APM has a built in error tracking solution which can be used to track both client and server errors.

<img src="/images/apm-error-tracking-intro-1.png" style="width: 500px"/>

## Type of Errors Tracked

﻿Meteor APM can track both server and client side errors alike. Here's the list:

**Server Side**

- Server Crash - Errors caused to crash your server
﻿- Method Errors - Errors thrown inside Meteor methods
- Subscriptions Errors - Errors thrown inside the publication (when you subscribed)
- Internal Meteor Errors - Errors thrown inside Meteor core platform

**Client Side**

- Internal Meteor Errors (via `Meteor._debug`)
- Errors captured via window.onerror

## Error Traces

﻿Meteor APM not only tracks errors, but it also trace errors and shows the context for your error. It includes, all the major events related to the trace. Then you can easily reproduce and fix the error very quickly. See below for example error traces which have been captured.

<img src="/images/apm-error-tracking-intro-2.png" style="width: 500px"/>

## Using Zones

With [Zone.JS](https://github.com/angular/zone.js) integration, we can follow Meteor's async execution path (in client) and identify more information which is not possible before.

As a result of that, error tracking can be improved and it can be used to capture stack traces over the async execution path.

To install zones:

`meteor add meteorhacks:zones`

If you've added zones into your Meteor application, error tracking on client can be improved dramatically. Take a look at the following error trace:

<img src="/images/apm-error-tracking-zones.png" style="width: 500px"/>
