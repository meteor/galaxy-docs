---
title: Reduce Bandwidth and CPU Waste
order: 54
---

Iron Router normally unsubscribes all previous subscriptions when entering into a new route.

Actually, this is not an Iron Router issue. It's a feature of Meteor's Deps package. Read [this article](http://meteorhacks.com/meteor-subscription-optimizations.html) to learn more about this.

## Why is this bad?

Although this is a nice feature it causes two main issues.

1. User has to wait between routes, even for a recently visited route.
2. There is an increase in subscription rate, which introduces cpu and network issues.

## Identifying this issue

With meteor APM you can identify the subscriptions that have this issue and apply a fix.

First visit the PubSub detailed view. Then sort publications by "Shortest Lifespan". Next, Select publications with the short lifespan and high throughput.

![Sort with Shortest Lifespan](https://i.cloudup.com/9VOU29DPwP.png)

Publications identified by the above selection criteria have the shortest lifespan and high subscription rates, which means they change very rapidly. The following fixes can be applied to resolve the issue.

## Potential Fix

Fixing this issue is not that hard. Simply using Subscriptions Manager, you could be able to avoid this issue. This is how you can fix the issue with Subscriptions Manager. Instead of using `Meteor.subscribe`, create a [Subscriptions Manager](https://github.com/meteorhacks/subs-manager) and subscribe with that.

~~~js
var subs = new SubsManager();

Router.map(function() {
  this.route('home', {
    path: '/',
    waitOn: function() {
      return subs.subscribe('postList');
    }
  });

  this.route('singlePost', {
    path: '/post/:id',
    waitOn: function() {
      return subs.subscribe('singlePost', this.params.id);
    }
  });
})
~~~

See [Subscriptions Manager docs](https://github.com/meteorhacks/subs-manager) for more info.

If you have a lot of users, simply fixing this issue will help you greatly reduce CPU cycles and Bandwidth.
