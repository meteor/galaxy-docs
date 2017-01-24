---
title: MongoDB
order: 13
description: Learn how to configure your MongoDB provider for Galaxy
---

Since Galaxy doesn’t provide a MongoDB cluster, you will need to host one yourself. We recommend using a dedicated database hosting service such as [mLab](https://mongolab.com/) or [Compose](https://www.compose.io/).

To configure MongoDB for your Meteor application, see the detailed steps in the [Deployment guide](/deploy-guide.html#mongo-configure). 

For optimum performance, please ensure your database is running in the same region.

<h2 id="configure-oplog">Configuring Oplog Tailing</h2>

Meteor can get real time updates from MongoDB by using [oplog tailing](https://github.com/meteor/meteor/wiki/Oplog-Observe-Driver). Oplog tailing involves reading the the MongoDB 'operations log' - a special Mongo collection that records all the write operations as they are applied to your database.

To use Oplog tailing, the database must be a Replica set enabled database. The sandbox database from mLab does not support Oplog tailing.

<h2 id="configuration">Configuring the app settings file</h2>

MongoDB is configured using environment variables in your 'settings.json' file. Refer to the [environment variables](/environment-variables.html) section of the Help Center to find a complete example. Note that a valid `MONGO_URL` is required unless you have removed the `mongo` package from your app. A missing/invalid `MONGO_URL` is a common cause of failed deployments.

**Learn more**

- Read this [compose.io article](https://www.compose.io/articles/meteors-new-galaxy-and-the-perfectly-composed-companion/) for using Compose.io databases with your Meteor app
