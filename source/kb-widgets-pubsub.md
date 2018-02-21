---
title: Widgets for PubSub
order: 62
---

## PubSub Summary

<img src="/images/apm-pubsub-summary.png" style="width: 500px"/>

Pubsub Summary is a set of important performance metrics related to your publications. These are the metrics:

- Response Time - Average time taken to process your publications in the server
- Sub Rate - Rate of new subscriptions
- Active Subs (Average)

## Sub Rate and Unsub Rate

<!-- Sub Rate (Subscriptions Per Minute) -->

<img src="/images/apm-sub-rate.png" style="width: 500px"/>

This chart shows the rate of subscriptions and unsubscriptions per minute. We can see how busy our application is in terms of new subscriptions and unsubscriptions.

## Active Subs and Average Lifetime

<img src="/images/apm-active-subs-average-lifetime.png" style="width: 500px"/>

This chart shows the number of active subscriptions on the server and the average lifetime of a subscription. With this information, we can see how busy our subscriptions are in terms of quantity and lifetime. ﻿

## Publication Breakdown

<img src="/images/apm-publication-breakdown.png" style="width: 500px"/>

Publication Breakdown allows you to sort by different values and find out how your publications work. These are the values you can sort:

- Sub Rate
- Unsub Rate
- Response Time
- Network Latency
- Est. Memory Usage
- Low Update Ratio
- Low Observer Reuse
- High Observer Reuse
- Shortest Lifespan
- Active Subs

## Response Time with Traces

<img src="/images/apm-response-time-traces-1.png" style="width: 500px"/>

Response Time chart shows how the Response Time changed with the time.

Additionally, if you like to inspect a trace of a method call at a particular point, simply find that point on the chart and click it. You'll get a few sample method traces: you can have it analyzed with just a click. ﻿

**How do we track traces?**

﻿It is impossible to send all the subscription traces processed on your app into Meteor APM. Instead we pick outliers and send them. We send all the collected traces (if exists) once a minute.

﻿This is how a trace looks like:

<img src="/images/apm-response-time-traces-2.png" style="width: 500px"/>
