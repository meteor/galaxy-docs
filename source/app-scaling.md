---
title: App Scaling
order: 14
description: Learn how to scale your app the right way
---

Meteor is using Node.js in the server and Node.js by default is single-threaded, or at least almost single-threaded except for things it defers to the OS.

> If you want to learn more about event-loop and "single-threaded" we recommend the following content:
> - JavaScript VM internals, EventLoop, Async and ScopeChains - Arindam Paul on [YouTube](https://www.youtube.com/watch?v=QyUFheng6J0)
> - Event Loop - Jake Archibald on [YouTube](https://www.youtube.com/watch?v=cCOL7MC4Pl0)
> - What the heck is the event loop anyway? - Philip Roberts on [YouTube](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
> - Everything You Need to Know About Node.js Event Loop - Bert Belder on [YouTube](https://www.youtube.com/watch?v=PNa9OMajw9w)
> - The Node.js Event Loop: Not So Single Threaded - Bryan Hughes on [YouTube](https://www.youtube.com/watch?v=zphcsoSJMvM)
> - Node's Event Loop From the Inside Out - Sam Roberts on [YouTube](https://www.youtube.com/watch?v=P9csgxBgaZ8)

This behavior affects how you scale your app. We will talk about two types of scaling here, and in the end how you should proceed with your app.

<h2 id="vertical-scaling">Vertical scaling</h2>

Vertical scaling refers to adding more resources (CPU/RAM/DISK) to your server as on demand. 

The issue with this approach for Node.JS applications, like Meteor, is that even after adding more CPU there is a limit to the number of requests it can process.

<img src="/images/app-scaling-rps-cpu.png" />

<figcaption align = "center"><b>Requests per second x CPU. <a href="https://betterprogramming.pub/horizontal-vs-vertical-scaling-in-node-js-1b4f3ec8282">Source</a> </b></figcaption>

You can see in the above load-test that there is a point when adding more CPU is not converting in more RPS for the server. This is the point you should stop vertical scaling, and it highly depends on your application.

Sometimes, if you have more CPU than node can use, you will get numbers like 40% CPU usage even when your app is almost down.

<h3 id="vertical-tips">RAM when Vertical Scaling</h3>

Node limits the heap size to 1400MB by default in 64bit, so if you are growing memory in your container to something more than 2GB remember to set the --max-old-space-size to be greater than 1400MB.


<h2 id="horizontal-scaling">Horizontal scaling</h2>

Horizontal scaling is the best way to serve more requests. You can add more containers which will multiply your RPS limit by its number.

A good approach for scaling Meteor apps is to limit your container to a reasonable size to fit your application and then, after that, horizontal scale(add more containers) as your connections increase.

