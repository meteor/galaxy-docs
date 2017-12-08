---
title: Optimizing Your Meteor App for Live Queries
order: 59
---

_Note: This content originally appeared on https://kadira.io/academy/meteor-performance-101 ._

Live Query support is one of the major competencies in Meteor. Normally, a new Live Query is created when you return a cursor from a publication. Then it’ll reactively watch the query and send changes to the client.

In order to detect these changes, Live Queries do some amazing work behind the scenes. To do this, they need to spend some CPU cycles. Therefore, Live Queries are a major factor affecting your app’s CPU usage.

However, the count of Live Queries itself does not cause many issues. These are the factors affecting the CPU usage:

* Number of documents fetched by Live Queries
* Number of live changes happening
* Number of oplog notifications Meteor is receiving

Fortunately, there are some easy ways to optimize our apps for better-utilized Live Queries. Let’s take a look.

<u>Let’s discuss some optimizations we can implement.</u>

### Try to fetch as little as possible

This is the rule of thumb you can apply for any app. But you can’t decide which publication to optimize until you go live or launch a load test. After that, you can use Meteor APM to find out which publications fetch a lot of data from MongoDB. Here’s how to [check this](https://cldup.com/HMW4ZQxrSI.gif):

* Go to Meteor APM Live Queries tab
* Sort the publications by “Fetched Documents”

Now you can see a set of publications sorted by the number of documents they fetched from MongoDB. Here are some optimizations you can apply to them:

* If the "Observer Reuse Ratio" is low, try to increase it. We’ll talk more about this in a second.
* If possible, try to reduce the number of documents fetched by changing your code. For instance, You could use a limit when fetching data.

### Reuse observers as much as possible

When you create a Live Query, it’ll create an observer internally. Observers are responsible for watching changes in the DB and notifying the Live Query. However, if there is an existing observer for a similar query, Meteor won’t create a new observer.

To be a similar query, both the query and the options passed to `Collection.find()` should be the same.

**Now let’s try to find some Live Queries to optimize**

* Sort publications by “Fetched Documents.”
* Then, check their Observer Reuse value.
* If that’s low, then we can optimize.

There are few simple things you can do to increase your observer reuse ratio. Take a look at this guide: [How to Reuse Observers](http://galaxy-guide.meteor.com/apm-improve-cpu-and-network-usage.html#How-to-Reuse-Observer)

### Optimize busy Live Queries

Another key point is to identify busy subscriptions and try to optimize them. A busy subscription is a subscription that triggers a lot of events, such as added, changed or removed, after it is created.

To identify busy subscriptions, [sort publications](https://cldup.com/A1bmCWO2mR.gif) with “Observer Changes: Live Updates”. These are the busy publications in your app.

> We calculate Live Updates by combining all the Observer Changes events except “Added (Initially)”.

Now that you know the busy publications in your app, try to see whether there is any chance to reduce the changes in those queries. Sometimes, you can add a field filter and try to avoid unnecessary changes, but it’s totally dependent on your app.

### Prevent unwanted oplog notifications

Meteor watches the MongoDB oplog to see changes happening in the MongoDB. If there is something happen in the DB, Meteor will receive it as a notification. The notification is attached to a collection. Then, Meteor will forward this notification to most of the observers created for that collection.

Now let’s try to see whether we are getting unwanted oplog notifications or not.

For this, look at the trends of observer changes with the trends of oplog notifications. If there is a big difference in trends (but not in the count), that means there are some unwanted notifications.

![](https://cldup.com/dmu3MVzycI.gif)

<b><sup>[This is how you can check trends]</sup></b>

This is usually because of doing bulk write operations in the DB. In that case, Meteor will also get those operations and try to handle them, even if there are no observers related to those updates. There is no direct fix; the only option is to avoid those bulk updates.

One possible option is to move the collection related to those writes into a different database and [manually connect](http://stackoverflow.com/a/20537457) to that database without the oplog.

Then, you can use a publication or a Meteor method to access that data. If you use a publication, keep in mind that it’ll poll the DB every 10 seconds.

<hr />

These are just a couple of ways to optimize your app for Live Queries. Some of these fixes are very easy to implement. Always try to fix the subscriptions that are used frequently; otherwise this may lead to premature optimization.
