---
title: MongoDB - Connect Database with MongoDB Compass
order: 17
description: Step-by-step guide to connect to a MongoDB database instance using MongoDB Compass, provided by Galaxy Databases.
---

<h2 id="objective">Objective</h2>

This guide provides detailed instructions on how to connect to a MongoDB database instance using MongoDB Compass, a popular Open Source (SSPL) management tool for MongoDB.

<h2 id="requirements">Requirements</h2>

- Access to the Galaxy Control Panel.
- Request a MongoDB database from the Galaxy team.
- MongoDB Compass installed (stable version) and an internet connection.

<h2 id="instructions">Instructions</h2>

#### Installation

1. **To install MongoDB Compass:**
   Follow the [official documentation](https://docs.mongodb.com/compass/current/install/).

#### Connect with MongoDB Compass

1. **Open MongoDB Compass:**
   Launch MongoDB Compass on your computer.

2. **Enter Connection Details:**
   - In the connection field, enter the Service URI provided by the Galaxy team.
   
3. **Establish Connection:**
   - Click "Connect" to establish a connection to the MongoDB instance.

<h2 id="detailed-steps">Detailed Steps</h2>

1. **Access the Control Panel:**
   Ensure you have access to the Galaxy Control Panel to obtain the credentials and the database service URI.

2. **Request the Database:**
   Contact the Galaxy team and request the creation of a MongoDB database.

3. **Install MongoDB Compass:**
   If MongoDB Compass is not installed, visit the [official website](https://www.mongodb.com/try/download/compass) and follow the installation instructions for your operating system.

4. **Obtain the Service URI:**
   - In the Galaxy Control Panel, navigate to “Galaxy Database” and locate the service URI for your MongoDB database.

5. **Connect in MongoDB Compass:**
   - Open MongoDB Compass.
   - Copy the provided service URI and paste it into the connection field in MongoDB Compass.

   <img src="/images/galaxy-databases-mongodb-compass-connection.png" style="width: 1080px"/>

   - Click the "Connect" button to establish a connection to the database.

    <img src="/images/galaxy-databases-mongodb-compass-connection-done.png" style="width: 1080px"/>

<h2 id="security-considerations">Security Considerations</h2>

- Ensure secure handling of MongoDB credentials and URIs.
- Use strong, unique passwords for database access.
- Regularly review access permissions and audit logs for security purposes.

By following these steps, you will be able to efficiently connect to and manage your MongoDB database instance using MongoDB Compass, facilitated by Galaxy Databases.