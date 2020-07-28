---
title: App Protection
order: 36
description: Learn how Galaxy protects your app
---

Galaxy's Network layer has a custom proxy tailored to work with Meteor apps.

Our proxy servers handle the HTTP and WebSocket requests to your app always selecting the best container to serve each specific request considering how many connections are already open on each container.

It also allows you to use multiple domains in our apps.

<h2 id="attacks">Attacks</h2>

DoS and DDoS attacks are attempts to make your app overloaded and unavailable for legitimate requests.

Galaxy proxy servers are in front of every request going to your app and this is a great advantage for your app as in our proxy servers we can isolate eventual attack attempts from your apps. This feature is called App Protection and it is enabled for all Galaxy clients.

Galaxy provides out-of-the-box protection against attacks analyzing all requests that are coming to our servers, aggregating the data across all servers and then making decisions about which type of requests are over our expected limits.

> App Protection was introduced in July 28th, 2020.

When a type of request is classified as abusive we stop sending these requests to your app, and we start to return HTTP 429 (Too Many Requests).

We also have some rules to define for how long this type of request will be blocked. If you have specific use cases that may need different limits please reach us out in the support (support@meteor.com).

We are not going to explain here in details how we identify abusive requests and what are our rules otherwise it would be easier for attackers to workaround them, also we are going to improve our App Protection feature every time we identify new opportunities for protection.

If you are going to perform load testing it is also recommended contacting us at least 2 business days in advance explaining how are you going to do it, from which IPs and targeting which hosts (domains).

> Attacks can happen in different scales so we are not promising that we can prevent any kind of attack but we can prevent most of them as our proxy layer is robust and definitely can handle a large amount of requests. We also use standard AWS protection in front of our servers.

You should configure your app as well to limit the messages received via WebSockets as our proxy servers are only acting in the first connection and not in the WebSocket messages after the connection is established. 

Meteor provides [rate limits](https://docs.meteor.com/api/methods.html#ddpratelimiter) so you can use it to protected your app further. 
