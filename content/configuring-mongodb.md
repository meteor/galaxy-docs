---
title: Configuring MongoDB
order: 5
description: Learn how to configure your MongoDB provider for Galaxy
---

After reading this guide, you’ll know:

1. Which MongoDB providers recommended for use with Galaxy
2. How to determine the right region for your database
3. How to add a MongoDB database and configure a DB user


Since Galaxy doesn’t provide a MongoDB cluster, you will need to host one yourself. We recommend using a service such as [mongolab](https://mongolab.com/).

Currently, Galaxy runs in the 'US-East-1' AWS region. For optimum performance, please ensure your database is running in the same region.


### Configuration

MongoDB is configured using environment variables in your 'settings.json' file. Refer to the [environment variables](setting-environment-variables) section of the Help Center to find a complete example. Note that a valid `MONGO_URL` is required unless you have removed the `mongo` package from your app. A missing/invalid `MONGO_URL` is a common cause of failed deployments.
