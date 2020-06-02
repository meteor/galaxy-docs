---
title: Triggers (Auto-scale)
order: 36
description: Galaxy triggers allows you to automatically change your capacity configurations to adapt to traffic. 
---

Galaxy triggers allows you to automatically change your capacity configurations to adapt to traffic.

<h2 id="endpoint">Why</h2>

Triggers provide a configurable way to perform actions in your app, this is important for Professional apps that need to adapt to the demand dynamically. For example, an education app uses more resources during the classes but can reduce the capacity overnight and on weekends.

We only charge the running hours of each container, so you can reduce the amount of hours you run each month and save money when your app has fewer connections.

> Triggers are available for all Professional apps. You can configure your triggers going to your app settings on Galaxy dashboard.

<h2 id="how-it-works">How it works</h2>

Galaxy checks all the triggers every minute, you don't pay anything extra to run triggers, they run on Galaxy servers.

Each trigger can perform a different action according to some rules. For a trigger to run the rules need to match, for each trigger you can choose if every rule needs to match (`AND`) or only one (`OR`) in order to proceed with the action. 

You can also restrict your triggers to run only in specific days and/or specific times (interval between hours). It's also available the interval that you want to run your trigger, you can choose how often it will run in seconds (60 seconds is the minimum).

<img src="/images/triggers-01.png" style="width: 500px"/>

<h2 id="metrics">Metrics</h2>

Triggers use metrics from your app to take decisions based on your rules. You can use the following metrics: CPU Usage (%), Memory Usage (%) and Number of Connections.

We support three series of metrics: every 5 seconds, every 3 minutes and every hour so you can select the best frequency to check your app metrics. You also select how many metrics do you want to use, for instance, you can select 12 metrics of 5 seconds that means you are going to take decisions based on the last minute (last 60 seconds).

Every metric is extract from your containers, and then we calculate the simple average between all containers for every timestamp. For example, if you have 3 containers and you selected 3 metrics using 3 minutes series you are going to have 3 values that corresponds to the average of your containers 3 minutes ago, 6 minutes ago and 9 minutes ago.

Every rule will be compared with these metrics (the average of your metrics for each timestamp) to decide if your trigger action is going to be executed or not.

<h2 id="actions">Actions</h2>

We support two actions at the moment, to add and remove containers. We are going to expand this in the next releases of Galaxy, if you have ideas for new actions please open a ticket (support@meteor.com).

As these two actions change the quantity of running containers of your app we provide limits for you to set. You can select the minimum of containers that your app should have and the maximum. You can also choose how many containers will be added or removed if your trigger action is fired, this configuration is called step.

Important: `add containers` action will never remove containers and `remove containers` action will never add containers then make sure you always have both configured with proper maximum and minimum configurations, and they make sense together.

<h3 id="actions">Add containers</h3>

<h3 id="actions">Remove containers</h3>
