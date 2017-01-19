---
title: Transfer apps
order: 23
description: Learn how to transfer an app to another account
---

You can deploy an application to one Galaxy account at a time. Galaxy utilizes the following policy to select the account to deploy your app to:

1. If an application with the specified hostname already exists in an account, Galaxy deploys to the same account.
2. If it is a new application, Galaxy chooses the individual user account if it exists.
3. If it is a new application, and individual user account does not exist, Galaxy chooses the first Galaxy organization account that you are a member of.

If you are a member of two or more accounts, you can then transfer the application to a different account.

<h2 id="meteor-13">Transfer with Meteor 1.3 or high versions</h2>

To transfer the application, on the command line, type:
`DEPLOY_HOSTNAME=galaxy.meteor.com meteor authorized [your_existing_hostname] --transfer [new_account_name]`

<h2 id="meteor-12">Transfer with Meteor 1.2 or lower versions</h2>

To transfer the application, on the command line, type:
`DEPLOY_HOSTNAME=galaxy.meteor.com meteor authorized [your_existing_hostname] --add [new_account_name]`

You need to have deploy privileges to the account `new_account_name`.

<h2 id="across-regions">Transfer across regions</h2>

To transfer an app from one region to another, re-deploy the app to the target region.

1. Deploy the same app code to the target region with a new hostname. Use the DEPLOY_HOSTNAME for the target hostname and set up DNS for the new hostname to point to the target region's ingress point.
2. Stop the app in the original region.

<h2 id="billing-after-transfer">Billing for transferred applications</h2>

The application container usage that occurred while the application was owned by the old account will be billed to the old account. Any new application container usage that occurs after the transfer to the new account will be billed to the new account.
