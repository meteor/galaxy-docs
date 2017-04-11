---
title: Widgets for PubSub
order: 62
---

## PubSub Summary

<img src="/images/apm-pubsub-summary.png" style="width: 500px"/>

Pubsub Summary is a set of important performance metrics related to your publications. These are the metrics:

- Response Time - Average time taken to process your publications in the server
- Sub Rate - Rate of new subscriptions
- Network Latency - Time spent to send your initial publication data set to the client. Click here to learn more about how we calculate Network Latency.
- Update Ratio - Update ratio is the percentage of updated data against the total data sent to the client. See how we calculate this metric.
- Observer Reuse - Observer Reuse is the percentage of observers reused in your publication. See how we calculate this metric. ﻿

## Sub Rate and Unsub Rate

<img src="/images/apm-sub-rate.png" style="width: 500px"/>

This chart shows the rate of subscriptions and unsubscriptions per minute. We can see how busy our application is in terms of new subscriptions and unsubscriptions.

## Average Response Time

<img src="/images/apm-average-response-time.png" style="width: 500px"/>

This chart shows the average response time for sending the initial data set for  subscriptions. We calculate this metric when we detect this.ready() for a publication. This chart shows you whether your subscriptions are slow to process initially. ﻿

## Network Latency

<img src="/images/apm-network-latency.png" style="width: 500px"/>

This chart shows the Network Latency across the selected Time Rage.

## Active Subs and Average Lifetime

<img src="/images/apm-active-subs-average-lifetime.png" style="width: 500px"/>

This chart shows the number of active subscriptions on the server and the average lifetime of a subscription. With this information, we can see how busy our subscriptions are in terms of quantity and lifetime. ﻿

## Publication Breakdown

<img src="/images/apm-publication-breakdown.png" style="width: 500px"/>

Publication Breakdown allows you to sort by different values and find out how your publications work. These are the values you can sort:

﻿- Sub Rate
- Unsub Rate
- Response Time
- Network Latency
- Est. Memory Usage
- Low Update Ratio
- Low Observer Reuse
- High Observer Reuse
- Shortest Lifespan
- Active Subs

## PubSub Recommendations

PubSub Recommendations analyzes crucial publications in your app and how they can be improved in both Network Latency and Response Time. By default, method breakdown is sorted with SubRate: once you click on a publication, you'll see a view like the following:

<img src="/images/apm-pubsub-recommendations.png" style="width: 500px"/>

**1.Response Time**

The green boxes represent Response Time. They show you the speed-up in Total Response Time you can gain if you manage to reduce 10ms from the Response Time for that particular publication. If the SubRate is lower, the impact is less.

Sometimes, it’s simply not possible to reduce the Response Time of that particular publication. In that case, try the next publication.  You can refer to this guide on How to Reduce Publication Response Time.

**  2.Network Impact**

The brown boxes represent Total Network Latency.  They denote how much speed you can gain (as a percentage) if you reduce a single kilobyte from your subscription data for that publication. Again, if the SubRate is lower, the impact is less. In cases where it’s impossible to reduce the amount subscription data, try analysing the next publication.

## Response Time with Traces

<img src="/images/apm-response-time-traces-1.png" style="width: 500px"/>

Response Time chart shows how the Response Time changed with the time.

Additionally, if you like to inspect a trace of a method call at a particular point, simply find that point on the chart and click it. You'll get a few sample method traces: you can have it analyzed with just a click. ﻿

**How do we track traces?**

﻿It is impossible to send all the subscription traces processed on your app into Kadira. Instead we pick outliers and send them. We send all the collected traces (if exists) once a minute.

﻿Currently, there is no way to alter how we collect traces in your app. But we will provide an API allow you decide how to collect traces and decide when to send them.

﻿This is how a trace looks like:

<img src="/images/apm-response-time-traces-2.png" style="width: 500px"/>

## Bandwidth Selector

<img src="/images/apm-bandwidth-selector.png" style="width: 500px"/>

Network Latency is calculated based on a predicated bandwidth of your target user base. This Bandwidth Selector helps you to change the bandwidth and see how Network Latency changes in accordance.
