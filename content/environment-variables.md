---
title: Environment variables
order: 12
description: Learn how to adjust Galaxy environment variables using your app's settings.json file
---

Environment variables in Galaxy are managed using your app's `settings.json` file. Galaxy interprets key/value pairs found in the `{"galaxy.meteor.com": {"env": { ... }}` section of your settings as environment variables.

<h3 id="common-env-variables">Commonly used environment variables</h3>

The following environment variable are commonly set for Galaxy apps:

- `MONGO_URL`: If you have any Meteor packages that requires a Mongo database, then this environment variable must be set. See your database provider instructions to determine the correct format and content for the URL.
- `MONGO_OPLOG_URL`: This is an optional environment variable if you are using MongoDB for your application. This is a performance optimization that we recommend for production applications. Read more in our [detailed documentation](https://github.com/meteor/docs/blob/master/long-form/oplog-observe-driver.md#oplogobservedriver-in-production) or in [this useful guide](https://meteorhacks.com/mongodb-oplog-and-meteor/).
- `ROOT_URL`: This is an optional environment variable. If you have any Meteor packages that need to generate a URL, then those packages will use `ROOT_URL` to identify the URL where the app is hosted. The default value for this is the primary hostname that your app is deployed to. This variable hooks up to the Meteor.absoluteUrl() API.
- `MAIL_URL`: This is required if you have the `email`  package in your application. In order to send email from the application, the `MAIL_URL` environment variable needs to be set.

The following are example formats for Mongo URL variables. You will have to configure a database and a user account with rights to access that database with your database provider.

`"MONGO_URL": "mongodb://<db_username>:<db_password>@<db_server_host>:<db_server_port>/<db_name>"`

`"MONGO_OPLOG_URL": "mongodb://<oplog_username>:<oplog_password>@<db_server_host>:<db_server_port>/<oplog_db_name>?authSource=admin"`

The following is an example setting for the `MAIL_URL` environment variable:
`smtp://postmaster%40your.mailserver.address.com:password@mailserver.smtp.address.com:587`

<h3 id="settings-example">settings.json example</h3>

```json
{
  "galaxy.meteor.com": {
    "env": {
      "MONGO_URL": "...",
      "MONGO_OPLOG_URL": "..."
    }
  },
  ... other keys can go here
}
```

<h3 id="see-also">See also</h3>
`Meteor.settings` in [Meteor docs](http://docs.meteor.com/#/full/meteor_settings).
