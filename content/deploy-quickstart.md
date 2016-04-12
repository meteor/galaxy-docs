---
title: Deploying Quickstart Guide
order: 1
description: Learn how to quickly deploy an app to Galaxy with these step-by-step instructions.
---

After reading this guide, you’ll know:

1. How to get your Meteor app ready for deployment
2. How to deploy your app via the command line
3. How to deploy if you're using Mac or Linux
4. How to deploy if you're using Windows
5. What to configure in your app to begin accessing it via a designated domain


<h2 id="get-started">Deploying with Galaxy</h2>
Galaxy makes it simple to deploy, scale, and monitor your Meteor app. This quickstart guide will walk new users through deploying your first app. It is the abridged version of the [comprehensive guide]() aimed at developers who have experience deploying apps with remote databases.

<h3 id="get-ready-for-deploy">Get your app ready for deploy</h3>
Before you begin, [configure access to your MongoDB database]() and set up any [environment variables]() your app depends on using your app’s settings.json file.

<h3 id="deploy-app">Deploy your app</h3>
On the command line, within your app's directory, type:
```
DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy [hostname] --settings path-to-settings.json
```

- `hostname` is the fully qualified domain name where you're planning to host your application (for example, 'www.facebook.com').
- `path-to-settings.json` is the path to your settings file (for example, './settings.json').


<h4 id="deploy-windows">Deploying with Windows</h4>
If you are using Windows, the commands to deploy are slightly different. You need to set the environment variable first, then run the deployment command second (the syntax is the same as everything you'd put for meteor deploy). The commands will look like this:

```
$ SET DEPLOY_HOSTNAME=galaxy.meteor.com
```
```
$ meteor deploy [hostname] --settings path-to-settings.json
```

<h3 id="configure-app">Configure your app</h3>
Once your app is successfully deployed, head on over to your [Galaxy dashboard](http://galaxy.meteor.com) to configure your app by adding a custom domain name and enabling SSL encryption.

Add a domain in your app’s settings and point your DNS to `galaxy-ingress.meteor.com`.

[Enable encryption]() to secure sensitive data by generating a free [Let’s Encrypt]() certificate or uploading a custom certificate.


<h3 id="related">Learn more</h3>
- Read our [comprehensive guide]() for deploying apps
- Learn how to [deploy to a specific account]()
- Learn how to [transfer apps]() between accounts
