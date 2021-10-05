---
title: Background jobs
order: 14
description: Learn how to have background jobs without affecting your connected users
---

Meteor is using Node.js in the server and Node.js by default is single-threaded, or at least almost single-threaded except for things it defers to the OS.

In a single-threaded environment like Node.js if you perform long-running tasks in the same containers that you are processing your connected users actions they are going to compete using the event-loop. This competition could cause many problems, like slowness or even the feeling that your app is down even when it is not down. In these cases your app is really busy.

> If you want to learn more about event-loop and "single-threaded" we recommend the following content:
> - JavaScript VM internals, EventLoop, Async and ScopeChains - Arindam Paul on [YouTube](https://www.youtube.com/watch?v=QyUFheng6J0)
> - Event Loop - Jake Archibald on [YouTube](https://www.youtube.com/watch?v=cCOL7MC4Pl0)
> - What the heck is the event loop anyway? - Philip Roberts on [YouTube](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
> - Everything You Need to Know About Node.js Event Loop - Bert Belder on [YouTube](https://www.youtube.com/watch?v=PNa9OMajw9w)
> - The Node.js Event Loop: Not So Single Threaded - Bryan Hughes on [YouTube](https://www.youtube.com/watch?v=zphcsoSJMvM)
> - Node's Event Loop From the Inside Out - Sam Roberts on [YouTube](https://www.youtube.com/watch?v=P9csgxBgaZ8)

Let's focus now and how you could solve this competition in your Meteor app.

<h2 id="split">Split into multiple apps</h2>

Every Meteor app has a settings file, the settings file is used in runtime, but it's not use at build time. This means that you have the opportunity to use the settings json file to change some behaviors of your system even if you have a single code base.

The idea here is to use the same code to provide a different environment for long-running tasks (like background jobs) and another environment for your connected users, so you don't need to worry about shared dependencies, multiple apps to update Meteor packages, multiple apps to update npm dependencies and so on. 

> It is ok if you want to have two independent apps with some shared code but in most cases we believe using the same code is the most effective way.
> 
> But in some companies they already have many different apps so it makes sense to create an app just for long-running tasks.

Here is how we would do, in our settings file we would have a boolean like `runJobs` and in settings for our connected users app we would use:
```json
{
  "runJobs": false
}
```
In the app for running long tasks we would use:
```json
{
  "runJobs": true
}
```
So in the file jobs file that is imported in your `server/main.js`:

```js
// server/main.js

import '../infra/jobs.js';
```

You would have a logic to decide based on your settings if you should run your long-running tasks or not:
```js
// infra/jobs.js
import { Meteor } from 'meteor/meteor';
import { SyncedCron } from 'meteor/littledata:synced-cron';
import { NotificationsCollection } from '../data/NotificationsCollection';

Meteor.startup(() => {
  console.time('jobs');

  // we want to run jobs in development as well, no matter the settings
  if (!Meteor.isDevelopment && !Meteor.settings.runJobs) {
    logger.log('** APP: SyncedCron are not started on app instance **');
    console.timeEnd('jobs');
    return;
  }

  SyncedCron.add({
    name: 'send notifications',
    schedule: parser => parser.text('every minute'),
    job: () => NotificationsCollection.sendNotifications(),
  });

  SyncedCron.start();
  console.timeEnd('jobs');
});
```

<h2 id="deploying">Deploying apps</h2>
