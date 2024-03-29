---
title: How to view stopped and crashed containers using Meteor APM
order: 67
description: Learn how to use Meteor APM to view the logs of stopped and crashed containers
---

<h2 id="apm-data">How to view metrics for crashed/stopped containers</h2>

Viewing stopped and crashed containers can be helpful for troubleshooting problems with your applications. For example, if you are seeing errors in your application logs, you can view the logs of stopped and crashed containers to get more information about the cause of the errors.

To find the crashed or stopped containers on Galaxy, go to the Logs tab in your app:
![Alt text](image-1.png)

Search for crashed or stopped to filter the results and find the container ID:
![Alt text](image-2.png)

Click on the container ID to view its logs. Then, click "View on APM" to see Meteor APM metrics.
![Alt text](image-3.png)

Open Meteor APM and filter your hosts (containers) with the desired container ID:
![Alt text](image-4.png)

After identifying the stopped or crashed container in Galaxy, you can utilize Meteor APM to examine the container logs and resolve the problem. However, please note that Meteor APM is only available on Professional plans. If you are currently on a free or Essentials plan, you will need to upgrade to a Professional plan in order to access this feature.
