---
title: Deploy guide
order: 2
description: Learn how to deploy an app to Galaxy with these detailed instructions.
---
After reading this guide, you’ll know:

1. How to create an app to demo the environment before deploying the "real" app
2. How to sign up for Galaxy
3. How to add a MongoDB database and configure a DB user
4. How to create a settings file for Galaxy
5. Deploy an app to Galaxy
6. What you need to configure to begin accessing your app via a custom domain

<h2 id="create-app">Create a Meteor app</h2>

<h2 id="sign-up">Sign up for Galaxy</h2>

You need a Meteor Developer Account.
Go to webform at meteor.com

<h2 id="mongo-connect">Connect your MongoDB database</h2>
If you have one:
If you need one:

<h3 id="mongo-add-user">Add a database user</h3>

<h2 id="settings-create">Create a setting file for Galaxy</h2>

<h2 id="galaxy-deploy">Deploy your app to Galaxy</h2>

<h3 id="account-selection">Specify an account to deploy</h3>

Galaxy utilizes the following policy to select the account to deploy your app to:

1. If an application with the specified hostname already exists in an account, Galaxy deploys to the same account.
2. If it is a new application, Galaxy chooses the individual user account if it exists.
3. If it is a new application, and individual user account does not exist, Galaxy chooses the first Galaxy organization account that you are a member of.

If you are a member of two or more accounts, you can specify an owner username (available in Meteor 1.3) with `--owner [username]`.

```
DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy [hostname] --settings path-to-settings.json --owner [username]
```

Where `username` is the Galaxy account username the app should deploy into. You need to have deploy privileges to the account.  Note: this only applies for new apps, as any subsequent deploys will already be attached to an account and re-use the same account.


<h2 id="configure-app">Configure your app</h2>










**Learn more**

- Based on the [deploy guide](http://coderchronicles.org/2016/03/15/deploying-a-meteor-app-to-galaxy/) by Anders Ramsay
- Read our [quickstart guide]() for deploying apps
- Learn how to [deploy to a specific account]()
- Learn how to [transfer apps]() between accounts
