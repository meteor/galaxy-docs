---
title: Migrate your app to Galaxy
order: 12
description: Learn how to migrate your app to Galaxy
---

Welcome to Galaxy, the best place to host your Meteor app!

When migrating your app you'll want to deploy a new instance of your app to Galaxy, ensure it works, and then switch over DNS from your prior hosting provider to Galaxy. This way you'll minimize any disruption to your users during your app migration.

<h2 id="migrate-sign-up">Sign up for Galaxy</h2>
You'll need a Galaxy account that your Meteor Development Account has deploy authorization to use.

[Sign up](https://www.meteor.com/galaxy/signup) here for a new Galaxy Account.

<h2 id="migrate-mongo-configure">Configure your MongoDB database</h2>

If your Meteor application has a package that requires Mongo, then you'll need a Mongo database configured for your application. If you want to use a hosted database provider, we recommend using a dedicated database hosting service such as [mLab](https://www.mlab.com), [compose](https://www.compose.io) or [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).

For optimum performance, we recommend that you setup a database in the same AWS region as your app deployment.

<h2 id="migrate-settings-create">Create a settings file for Galaxy</h2>

Create a Meteor settings file that will define the set of configurations needed for your application to deploy and run on Galaxy. In your application directory, create a file named `settings.json`.

At a minimum, if your app has a package that requires Mongo, the `settings.json` file needs to contain the connection URL to the MongoDB database. Put the Mongo URI in the file, using this format:

```
{
  "galaxy.meteor.com": {
     "env": {
       "MONGO_URL": "mongodb://<dbuser>:<dbpassword>@<dbserver>:<dbport>/<dbname>"
     }
   }
}
```

For a full explanation and a more detailed example of the `settings.json` file, see [Environment Variables](/environment-variables.html).

<h2 id="migrate-select-hostname">Select a hostname</h2>

For this initial deployment of your app, use a hostname from one of the [Galaxy-included](/custom-domains.html#meteorapp-subdomain) `.meteorapp.com` subdomains.

For apps deployed to Galaxy’s US East region, deploy to `<your_app_name>.meteorapp.com`.

For apps deployed to Galaxy’s EU West region, deploy to `<your_app_name>.eu.meteorapp.com`.

For apps deployed to Galaxy’s Asia-Pacific region, deploy to `<your_app_name>.au.meteorapp.com`.

You'll later configure DNS to point your existing domain to your app on Galaxy.

<h2 id="migrate-deploy-app">Deploy your app</h2>

The value of DEPLOY_HOSTNAME will depend on which region you are deploying to:

- To deploy to US East: DEPLOY_HOSTNAME=galaxy.meteor.com

- To deploy to EU West: DEPLOY_HOSTNAME=eu-west-1.galaxy.meteor.com

- To deploy to Asia-Pacific: DEPLOY_HOSTNAME=ap-southeast-2.galaxy.meteor.com

<h3 id="deploy-mac">Mac and Linux</h3>

On the command line, within your app's directory, type:
```
DEPLOY_HOSTNAME=[region] meteor deploy [hostname] --settings [filepath.json]
```

- `region` is 'galaxy.meteor.com' for US East, 'eu-west-1.galaxy.meteor.com' for EU West, and 'ap-southeast-2.galaxy.meteor.com' for Asia-Pacific.
- `hostname` is the fully qualified domain name where you're planning to host your application (using `<your_app_name>` in the `.meteorapp.com` hostname format, in this example).
- `filepath.json` is the path to your settings file (for example, './settings.json').

<h3 id="deploy-windows">Windows</h3>

If you are using Windows, the commands to deploy are slightly different. You need to set the environment variable specifying your region first, then run the deployment command second (the syntax is the same as everything you'd put for meteor deploy).

In the case of US East, the commands would be:

```
$ SET DEPLOY_HOSTNAME=galaxy.meteor.com
```
```
$ meteor deploy [hostname] --settings path-to-settings.json
```

<h2 id="migrate-verify-app">Verify your app deployment</h2>

Verify that the deployment was successful. Check to see if the application is accessible by navigating to your configured URL, which should be using the `.meteorapp.com`  format. Then check the application logs in Galaxy to see if there are any errors that are affecting the deployment.

The location of your application logs will depend on your region. If your app is named `example`, the logs will be found at the following URLs:

- For US East: `galaxy.meteor.com/app/example.meteorapp.com/logs`

- For EU West: `eu-west-1.galaxy.meteor.com/app/example.eu.meteorapp.com/logs`

- For Asia-Pacific: `ap-southeast-2.galaxy.meteor.com/app/example.au.meteorapp.com/logs`

<h2 id="migrate-configure-app">Finish configuring your app deployment</h2>

Once your application is successfully deployed, head on over to the Galaxy dashboard in your region [(example: US East)](http://galaxy.meteor.com) to finish configuring your application.

Add your custom domain in the Galaxy application’s settings page.

You will now update your DNS settings to cut over from pointing to your prior hosting provider to Galaxy.

If you are using a subdomain (for example `www.acme.com` or `app.acme.com`), then use a CNAME and point your DNS to:

- `galaxy-ingress.meteor.com` for applications in the US East region.

- `eu-west-1.galaxy-ingress.meteor.com` for applications in the EU West region.

- `ap-southeast-2.galaxy-ingress.meteor.com` for applications in the Asia-Pacific region.  

If you are deploying to a root domain (for example mydomain.com), then follow the advanced instructions [here](/dns.html).

<img src="images/email-add-domain.png" style="">

[Enable encryption](/encryption.html) as a best practice by generating a free [Let’s Encrypt](https://letsencrypt.org) certificate or uploading your own custom certificate.

<img src="images/email-enable-ssl.png" style="width: 300px;">

<h2 id="get-support">Get support</h2>

If you aren't able to complete your app migration, contact [Galaxy Support](https://galaxy.meteor.com/support) and we'll assist you.
