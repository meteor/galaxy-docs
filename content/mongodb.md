---
title: MongoDB
order: 5
description: Learn how to configure your MongoDB provider for Galaxy
---

Since Galaxy doesn’t provide a MongoDB cluster, you will need to host one yourself. We recommend using a dedicated database hosting service such as [mLab](https://mongolab.com/) or [Compose](https://www.compose.io/).

Currently, Galaxy runs in the 'US-East-1' AWS region. For optimum performance, please ensure your database is running in the same region.


<h3 id="configuration">Configuration</h3>

MongoDB is configured using environment variables in your 'settings.json' file. Refer to the [environment variables](/environment-variables.html) section of the Help Center to find a complete example. Note that a valid `MONGO_URL` is required unless you have removed the `mongo` package from your app. A missing/invalid `MONGO_URL` is a common cause of failed deployments.
