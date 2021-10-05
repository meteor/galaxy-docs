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

Let's focus now on how you could solve this competition in your Meteor app.

<h2 id="split">Split into multiple apps</h2>

Every Meteor app has a settings file, the settings file is used in runtime, but it's not use at build time. This means that you have the opportunity to use the settings json file to change some behaviors of your system even if you have a single code base.

The idea here is to use the same code to provide a different environment for long-running tasks (like background jobs) and another environment for your connected users (web), so you don't need to worry about shared dependencies, multiple apps to update Meteor packages, multiple apps to update npm dependencies and so on. 

> It is ok if you want to have two independent apps with some shared code but in most cases we believe using the same code is the most effective way.
> 
> But in some companies they already have many different apps so it makes sense to create an app just for long-running tasks.

Here is how we would do, in our settings file we would have a boolean like `runJobs` and in the settings for our connected users app (web) we would use (`settings-web.json`):
```json
{
  "runJobs": false
}
```
In the app for running long tasks we would use (`settings-jobs.json`):
```json
{
  "runJobs": true
}
```

So we have enabled the jobs just in the jobs app. So in the file jobs file that is imported from your server `mainModule` you would have (`server/main.js`):

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

In this example we are using `synced-cron` package to communicate between the apps using MongoDB. But you could use a different package or create your own solution.

Another idea that you could use with this double app set up is to send data from one app to the other using DDP calls, some clients use this setup, so they can defer almost all the work for the jobs app, like processing an image, generating an Excel file, so everything that takes more than a few milliseconds is not going to cause slowness in the containers that are responding to user direct actions.

<h2 id="deploying">Deploying apps</h2>

Now that you have your code ready and also your settings ready we need to think about the deploy.

As you have the same code base you don't need to build twice, and this is possible using a deploy flag `--cache-build`.

Here is how we would do it:
```shell
# deploy.sh

# build and deploy the jobs app
meteor deploy jobs.yourdomain.com --settings settings-jobs.json --cache-build

# deploy the web app
meteor deploy app.yourdomain.com --settings settings-web.json --cache-build
```

The second deploy command is going to skip the build part, it is just going to upload your bundle and deploy your second app much faster.

See that they are two different apps on Meteor Cloud (Galaxy), which is really great as you can isolate them, use different [triggers](./triggers.html), analyze their performances in different APM dashboards, everything is isolated in runtime, except your database.

The jobs app for example could be just a backend app, without any domain accessing it. You just leave it without a CNAME pointing to it in your DNS configurations.

<h2 id="deploying">Monitoring</h2>

As you have two different apps now it's simple to customize your app for a specific type of workload. 

For example, if your jobs app is using Worker Threads you could use container sizes that will allow you to have more than one core. That would probably don't make a lot of sense in your web app if you are not using Worker Threads there.

Another important aspect is to analyze APM, Galaxy Metrics and logs independently. Including Galaxy notifications, so you will receive specific notifications if something is happening in the app, for example, maybe you know that your jobs app is going to be unhealthy with heavy jobs and this is ok, you can even turn off this notification if you want.

And of course, all Galaxy configurations will independent for each app, as such, triggers, app protection, grace period, unhealthy container replacement, etc.

<h2 id="costs">Costs</h2>

Running two different apps with the same load is not going to increase your costs. Actually it could reduce your costs as you can use different container sizes instead of the large possible for all workloads. You could also use different triggers and scale down more aggressively as you are going to have more control of the tasks that are running in which app.

<h2 id="alternative">Alternative approaches</h2>

- You could use different apps with different code bases, this is fine as well, as we explained above the only downside is that you need to manage two Meteor apps, two package.json, two of everything, so maybe it's more work. Also, you need to have a way to share packages what is fine but one more thing to be concerned about.

- You could use `GALAXY_CONTAINER_ID` to try to control what is running in each container, but it's hard to manage your containers relying on Galaxy internals. Also, you would need to make sure you always have the container assigned to a specific job available. Another problem would be to avoid long-running task containers from user access as Galaxy proxy is managing the balance for you and that is what you want to avoid in the first place: mixing user requests and long-running tasks. The monitoring of our app will be harder as well you are going to have metrics from different work loads mixed up in the same app.

<h2 id="example">Example</h2>

To wrap up we also have an [example](https://github.com/meteor/examples/#double-app) app implementing this approach.

We use this approach a lot internally as well, and we are sharing here as a best practice as we really believe it is a very effective way to solve this problem.

Feel free to provide feedback about this approach at support@meteor.com.
