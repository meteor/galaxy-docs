---
title: Triggers (Auto-scale)
order: 36
description: Galaxy triggers allows you to automatically change your capacity configurations to adapt to traffic. 
---

Galaxy triggers allows you to automatically change your capacity configurations to adapt to traffic.

<img src="/images/triggers-00.png" />

<h2 id="endpoint">Why</h2>

Triggers provide a configurable way to perform actions in your app, this is important for Professional apps that need to adapt to the demand dynamically. For example, an education app uses more resources during the classes but can reduce the capacity overnight and on weekends.

We only charge the running hours of each container, so you can reduce the amount of hours you run each month and save money when your app has fewer connections.

> Triggers are available for all Professional apps. You can configure your triggers going to your app settings on Galaxy dashboard.

<img src="/images/triggers-02.png" />

<h2 id="how-it-works">How it works</h2>

If you prefer video, [click here](https://www.youtube.com/watch?v=rwLoviLzG6s) to watch

[<img src="/images/triggers-07.png" />](https://www.youtube.com/watch?v=rwLoviLzG6s)

Galaxy checks all the triggers every minute, you don't pay anything extra to run triggers, they run on Galaxy servers.

Each trigger can perform a different action according to some rules. For a trigger to run the rules need to match, for each trigger you can choose if every rule needs to match (`AND`) or only one (`OR`) in order to proceed with the action. 

You can also restrict your triggers to run only in specific days and/or specific times (interval between hours). The hours are both inclusive, for example, if you want a trigger running only at 1AM you can set `Start hour` and `End hour` to 1.

It's also available the interval that you want to run your trigger, you can choose how often it will run in seconds (60 seconds is the minimum).

<img src="/images/triggers-01.png" />

We log useful information for each trigger run, you can check them in the Logs section of your trigger. Reading the logs you can understand why your trigger action is executing and why it's not executing as well, so you can adjust your configurations. Every time you save your configurations Galaxy runs your trigger in the next check round (every minute one check round happens).

<img src="/images/triggers-03.png" />

We expose Triggers in our Public [API](./api.html) as well, so you can change your triggers programmatically if you want.

<h2 id="metrics">Metrics</h2>

Triggers use metrics from your app to take decisions based on your rules. You can use the following metrics: CPU Usage (%), Memory Usage (%) and Number of Connections.

We support three sample durations (`Sample duration`): 5 seconds, 3 minutes and hour so you can select the best duration to check your app metrics. You also select how many samples (`Sample quantity`) do you want to use, for instance, you can select 12 samples of 5 seconds that means you are going to take decisions based on the last minute (last 60 seconds).

Every metric is extracted from your containers, and then we calculate the simple average between all containers for every sample from the same timestamp. For example, if you have 3 containers and you selected 3 samples using 3 minutes as sample duration you are going to have 3 values that corresponds to the average of your containers 3 minutes ago, 6 minutes ago and 9 minutes ago.

These metrics are exactly the same you see in the graphs of your container in the Containers tab.

<img src="/images/triggers-06.png" />

Every rule will be compared with these metrics (the average of your samples for each timestamp) to decide if your trigger action is going to be executed or not.

<h2 id="actions">Actions</h2>

We support three actions at the moment, to add, remove, and to kill containers. If you have ideas for new actions please open a ticket (support@meteor.com).

As the actions to add and remove containers change the quantity of running containers of your app we provide limits for you to set. You can select the minimum of containers that your app should have and the maximum. You can also choose how many containers will be added or removed if your trigger action is fired, this configuration is called step.

Important: `add containers` action will never remove containers and `remove containers` action will never add containers then make sure you always have both configured with proper maximum and minimum configurations, and they make sense together. Also minimum and maximum are checked before the rules and if they are not correctly this run will fix it.

<h3 id="add">Add containers</h3>

`add containers` action as the name action name says will add more containers to your app when the rules return true (match). You can configure your trigger as you want.

Usually you will configure it based on CPU Usage (%) or Number of Connections, for example, if you know that your containers usually handle 500 connections you can add a rule to add more containers when you reach 450 connections per container. It's recommended to use `OR` if you want to use more than one rule here, so if any rule returns true you scale up your app.

It's important to turn on the [notification](./notifications.html) for the activity `Trigger add containers limit error` so you know if your `add containers` action is not working because you have reached your account limit. You can always ask us to increase your container limit (support@meteor.com). You can check your current limit in your Account settings. 

> this activity was introduced with Triggers release so review your Notifications

<img src="/images/triggers-05.png" />

<h3 id="remove">Remove containers</h3>
`remove containers` action as the name action name says will remove containers from your app when the rules return true (match). You can configure your trigger as you want.

Usually you will configure it based on CPU Usage (%) or Number of Connections, for example, if you know that your app can provide good experience for your users until 70% of CPU then you can add a rule to remove containers when you reach 60% of CPU usage per container. It's recommended to use `AND` if you want to use more than one rule here, so if any rule is still more than expected you don't scale down your app.

<img src="/images/triggers-04.png" />

<h3 id="kill">Kill containers</h3>
`kill containers` action will kill containers from your app when the rules return true (match). You can configure your trigger as you want.

This action is the same as clicking manually in the "kill container" icon below each container in the dashboard.

Usually you will configure it based on CPU Usage (%) or Number of Connections, for example, if you know that your app can provide good experience for your users until 80% of CPU then you can add a rule to kill containers when it reachs 80% or more of CPU usage. Of course, this action is not going to be enough if you don't have `add containers` action working properly as well in case you start to receive a lot of connections as your CPU usage on each container will continue to go up all the time.

This action is also helpful after a scale up event (`add containers` action) that caused your older containers (containers that were running before the scale up event) to be handling more connections than they should. So this action would force a spread of these connections that were centralized in older containers. As you probably know Galaxy doesn't change existing connections to new containers unless the containers are not available anymore, Galaxy does this to avoid reconnections that could cause more load in your database due to reloading existing subscriptions. 

Another case is when you have different user profiles using your app and some profiles are causing more load than others (heavy users or admins), if you are unlucky you can get a lot heavy users in the same container, causing a huge load on a specific container, so killing this container is also going to cause these heavy users to be spread across containers and improve the experience for your users.

This action doesn't change the number of running containers, it's just going to force the replacement of a specific container. The same as the "kill container" icon in the dashboard. We don't recommend using this action if you have less than 3 containers running in your app.

Galaxy is going to redistribute your users (connections) to other containers after this action but if you want to check the behavior of your app in this case, we recommend that load your app in your browser, check in the Dev Tools of your browser the cookie "galaxy-sticky" (the value will be something like "!s6f3HQaHBwacbYAaK-seree"), after the dash you have your container name, then go to Galaxy dashboard and kill this container manually, you are going to see if your app is handling a reconnection properly as Galaxy is going to reconnect your app to another container. Even if you don't want to use this action it is recommended to see how your app behaves on reconnections as they can happen any time a container is replaced.
