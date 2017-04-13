---
title: Widgets for Methods
order: 64
---

## Methods Summary

<img src="/images/apm-methods-summary.png" style="width: 500px"/>

Methods Summary shows the summary of the method in the selected date range. It applies to the selected screen. For example, if you have selected Methods Overview and Detailed View, the Methods Summary will show a summary for all the methods. But if you select a method in the Detailed View, the summary will show only data for that method.

Here is a list of the metrics shown in the widget:

- Mean Res. Time - The mean response time per method. It is shown in milliseconds.
- Throughput  - The number of method calls received per minute. This is an average metric.
- Total Methods  - Total number of method calls received, including errors.
- Error Rate  - Percentage of errors, calculated using the following equation:
(total number of calls with errors/total number of calls for the method)* 100
- Total Errors -  Total number of method calls with errors received.

## Average Response Time

<img src="/images/apm-average-response-time-ms.png" style="width: 500px"/>

The chart above shows response time for method calls for the selected date range. The X-axis contains the date and the Y-axis contains the response time in milliseconds.

## Throughput (Requests Per Minute)

<img src="/images/apm-throughput.png" style="width: 500px"/>

This chart shows throughput for method calls for the selected date range. The X-axis contains the date and the Y-axis contains the requests (method calls) per minute.

## Time Breakdown

<img src="/images/apm-time-breakdown.png" style="width: 500px"/>

This pie chart shows what your method spent time doing during the selected date range. It groups time into following categories:
- db  - Time spent on database activities, including read and write operations.
- http - Time spent on processing HTTP requests (accessed with Meteor's HTTP package)
- compute - Time spent on CPU-intensive tasks inside a method (e.g. time spent sorting and calculating some value).
- async - Time spent on async activities, especially with NPM modules.
- email  - Time spent sending emails.
- wait - Time the method spent waiting to be processed. This metric is important because methods from a single client are processed sequentially, and so a method can sometimes idle in the queue waiting to be processed.

## Error Rate and Errors

<img src="/images/apm-error-rate-and-errors.png" style="width: 500px"/>

This chart shows errors (in methods) for the selected date range. At the bottom of the chart, a list of common errors is shown. The X-axis contains the date and the Y-axis contains the requests (method calls with errors) per minute.

## Method Breakdown

<img src="/images/apm-method-breadown-1.png" style="width: 300px"/>

This chart allows you to drill down into the data. It shows a list of methods sorted by metric, which can be selected on top. In the chart above, methods have been sorted by average response time. Options for sorting are shown below.

<img src="/images/apm-method-breadown-2.png" style="width: 300px"/>

For each method, two progress bars are shown. The green progress bar represents the sorted metric, while the orange bar represents the throughput of the metric. This throughput bar is shown regardless of the metric you've sorted. Sometimes, even though the metric value is high, it may not have a considerable amount of throughput.  The throughput bar on this chart enables you to detect that situation.

Another feature of this chart is the ability to select the method. Once you have selected a method, all the other graphs will show data corresponding to the selected method.

<img src="/images/apm-method-breadown-3.png" style="width: 300px"/>
