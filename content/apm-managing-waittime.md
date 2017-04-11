---
title: Managing Wait Time
order: 56
---

_Note: This content originally appeared on https://kadira.io/academy/meteor-performance-101 ._

 In this article, I'll explain to you about the waitTime and how you can manage it. waitTime is not something evil, but you need to learn how to manage it.

## What is wait time?

Internally, Meteor executes all the DDP messages for a given client sequentially. Let me explain with an example:

> When I refer to "DDP messages", they include both subscriptions and method calls made to the server.

Let's say I have a simple **blog** running with Meteor. When a user simply visits a page, a few things are happening behind the scenes:

* a subscription to get postList (which will be shown in the sidebar)
* a call to the detectCountry method to get the country from the IP address
* a subscription to get the blogPost
* a subscription to get comments
* a subscription to get categories

Now, Meteor loads all these DDP messages in a sequence by default. So, categories will be executed at the end and the result will be delayed!
You can easily see this behaviour by analyzing a Kadira trace for the categories method:

![Showing Meteor WaitTime](https://cldup.com/CBdwsq8BYo.png)

[See Complete Trace](https://ui.kadira.io/pt/d6235716-ab27-4f09-a876-503e5934b228)

You can clearly see it has a waitTime of **6415** milliseconds.

## Using this.unblock

Now let's think about these DDP messages:

* the `detectCountry` method has no dependencies on other DDP messages
* all the other DDP messages should load after the blogPost subscription

By looking at the rules above, we don't need detectCountry to block any other messages in particular, since it took almost 5 seconds to execute.
So we can invoke this.unblock inside the method body as shown below and tell Meteor to stop blocking other messages.

~~~js
Meteor.methods({
  detectCountry: function() {
    this.unblock();
    // other logic
  }
});
~~~

We need the blogPost subscription to load before the others but the other subscriptions may execute in parallel. So, we can add this.unblock inside blogPost publications as well.  

But, unfortunately, this.unblock is available only inside methods and we can't use it inside publications.

> But there is a cure for this. We've created a package called meteorhacks:unblock, which allows you to use this.unblock inside a publication.
>
> Simply install it using `meteor add meteorhacks:unblock` and use `this.unblock`

Now we've added the necessary optimizations. Let's run the app and see what's happening right now:

![Meteor WaitTime fixed](https://cldup.com/Zt3IGxMD0n.png)

[See Complete Trace](https://ui.kadira.io/pt/1ad4420f-0282-456c-b95e-a29a6ea11df9)

Wow, that's great. We've reduced the initial subscription load time from **6415 to 360** milliseconds. That's a huge achievement.

If you carefully look at the above trace, we still have the waitList because the `blogPost` subscription is a blocking one. But you can clearly see that other messages don't block the execution.

## Unblock Carefully

So, `this.unblock` cannot be enabled for all methods and subscriptions by default since it might give you some [unexpected behaviors](https://meteorhacks.com/understanding-meteor-wait-time-and-this-unblock.html#why-thisunblock-does-not-always-work). But, if your methods and subscriptions don't depend on others, there is a good chance you can unblock them and reduce the waitTime. But finally, it all depends on your app.

If you need to ask a specific question related to your app, please post it on [**Kadira Hub**](https://hub.kadira.io) and let's carry on the discussion.
