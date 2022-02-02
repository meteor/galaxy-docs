---
title: MongoDB
order: 13
description: Learn how to configure your MongoDB provider for Galaxy
---

Since Galaxy doesn’t provide a MongoDB cluster for production usage, you will need to host one yourself. We recommend using a dedicated database hosting service such as [ScaleGrid](https://console.scalegrid.io/users/register?partnerID=meteor.com) or [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).

To configure MongoDB for your Meteor application, see the detailed steps in the [Deployment guide](/deploy-setup.html#mongo-configure).

For optimum performance, please ensure your database is running in the same region.

<h2 id="configuration">Configuring the app settings file</h2>

MongoDB is configured using environment variables in your `settings.json` file. Refer to the [environment variables](/deploy-setup.html#common-env-variables) section to find a complete example.

Note that a valid `MONGO_URL` is required unless you have removed the `mongo` package from your app. A missing/invalid `MONGO_URL` is a common cause of failed deployments.

<h2 id="authentication">Connecting to your database</h2>

Galaxy is agnostic about how you talk to MongoDB, as long as you provide the appropriate credentials. If you can't connect, follow these steps:

1. Review the settings and examples on the [Environment variables](/deploy-setup.html#common-env-variables) section.
2. Try connecting without a Mongo Oplog URL to see if that is causing the issue.
3. Verify the URL and username/password by connecting through a MongoDB tool or CLI.

If it still isn't working, you may want to check <a href="http://github.com/meteor/meteor/issues/">GitHub</a> and the <a href="https://forums.meteor.com/">forums</a>, or write to your database provider. They'll usually have more visibility into the issue than anyone in Galaxy support.

<h2 id="configure-oplog">Configuring Oplog Tailing</h2>

Meteor can get real time updates from MongoDB by using [oplog tailing](https://github.com/meteor/meteor/wiki/Oplog-Observe-Driver). Oplog tailing involves reading the MongoDB 'operations log' - a special Mongo collection that records all the write operations as they are applied to your database.

To use Oplog tailing, the database must be a Replica set enabled database. Refer to the [environment variables](/deploy-setup.html#common-env-variables) section to find an example.

<h2 id="learn-more">Learn more</h2>

- Learn how to [configure your apps](/deploy-setup.html) on Galaxy.
- Read our main [guide for deploying applications](/deploy-to-galaxy.html)  on Galaxy.
- Read this [OK GROW! article](https://github.com/meteor/guide/files/4450467/okgrow-oplog.tailing.pdf) to connect your Meteor app to MongoDB Atlas with Oplog tailing
