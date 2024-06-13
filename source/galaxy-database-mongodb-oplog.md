---
title: MongoDB - Oplog user Setup
order: 18
description: Guide to setting up oplog tailing for MongoDB databases in Galaxy Database, enabling real-time data synchronization and integration with third-party tools.
---

## Overview

Connect your MongoDB deployments to third-party tools by setting up oplog tailing to read events from the MongoDB oplog. The oplog (operations log) is a special capped collection that keeps a rolling record of all operations modifying the database data. Oplog tailing is particularly beneficial for Meteor apps, ensuring real-time data synchronization.


## Oplog Functionality

Oplog functionality in Galaxy Database is available exclusively for replicaset implementations. This feature allows operations to be replicated and integrated with third-party tools, providing real-time notifications for database changes.

## Creating a MongoDB User for Oplog Tailing

Once your MongoDB cluster is set up, create a new user for oplog tailing:

1. Log in to the Galaxy Database Console.
2. Navigate to your cluster and connect using the admin user.
3. Execute the following command to create the oplog user:
   ```bash
   use admin;
   db.createUser({user: "oploguser", pwd: "PasswordForOplog", roles: [{role: "read", db: "local"}]});
   ```

## Connecting to the MongoDB Oplog

To connect to the oplog, ensure your connection string's authSource is set to the admin database where the oplog user is created, pointing to the local database where the oplog resides.

#### Oplog User Credentials

- **Username:** oploguser
- **Password:** PasswordForOplog

#### Connection String Example

```plaintext
mongodb://oploguser:PasswordForOplog@galaxyhostingdb.meteor.com/local?authSource=admin&replicaSet=replicaSetName
```

Find your MongoDB Connection String under the Overview tab of your MongoDB cluster details page in the Galaxy Database console.

This documentation provides guidance on setting up oplog tailing for MongoDB databases using Galaxy Database.