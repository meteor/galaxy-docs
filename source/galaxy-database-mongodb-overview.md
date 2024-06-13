---
title: MongoDB - Database Management Overview
order: 15
description: Overview of managing a MongoDB database instance in Galaxy Databases, including details on database type, plan information, access credentials, and usage instructions.
---

## Overview

After creating a MongoDB database, users will have access to a comprehensive interface providing all necessary information to manage and access their database. The interface is structured into several main sections, including database type, plan details, access credentials, and additional configuration and support options.


To access details of the created database, click open.

#### User Interface

#### Sidebar Menu

In the sidebar menu (located on the left), users will find the following options:

- **Databases:** Options related to databases.

<img src="/images/galaxy-databases-mongodb-overview-1.png" style="width: 1080px"/>

- **Overview:** Details of the selected database.

#### Main Section

In the main section of the interface, the following information is presented:

<img src="/images/galaxy-databases-mongodb-overview-2.png" style="width: 1080px"/>

#### Database Details

- **Database Name:** amazonprime
- **Type:** STANDALONE
- **Region:** us-east-1

#### Plan Information

- **Plan:** Standard
- **MongoDB Version:** v7.0
- **Resources:**
  - RAM: 2 GB
  - CPUs: 2
  - Storage: 20 GB
- **Status:** Running
- **Containers in Use:** 1
- **Monthly Cost:** $42 / month

#### Credentials

The credentials section provides necessary information to access the database:

- **Username:** admin
- **Password:** password
- **Connection String:**
  `mongodb://username:<password>@philippeaquino92_amazonprime-01.mongodb.meteor.io:31002/admin`

## Usage Instructions

#### Accessing the Database

1. Use the provided credentials:
   - Copy the username and password.
   - Use the provided connection string to connect to the database.

2. Connection Example:
   ```bash
   mongo "mongodb://username:<password>@philippeaquino92_amazonprime-01.mongodb.meteor.io:31002/admin"
   ```

   Replace `<password>`:
   - Make sure to replace `<password>` with the provided password.

#### Managing the Database

- **Create Specific Users for Applications:**
  It is recommended to create users with specific permissions for each application that will access the database.

- **Access Documentation:**
  Use the documentation link in the sidebar menu to get detailed information about using and connecting to MongoDB.

- **Monitor Status:**
  Regularly check the service status to ensure the database is operating as expected.

- **Request Support:**
  Use the support option in the sidebar menu to resolve any issues or questions that may arise.

This documentation provides comprehensive guidance for users to understand and effectively use the MongoDB creation system interface in Galaxy Databases.