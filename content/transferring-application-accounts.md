---
title: Transferring apps
order: 23
description: Learn how to transfer an app to another account
---

You can deploy an application to one Galaxy account at a time.

Galaxy utilizes the following policy to select the account to deploy your app to:

1. If an application with the specified hostname already exists in an account, Galaxy deploys to the same account.
2. If it is a new application, Galaxy chooses the individual user account if it exists.
3. If it is a new application, and individual user account does not exist, Galaxy chooses the first Galaxy organization account that you are a member of.

If you are a member of two or more accounts, you can then transfer the application to a different account.

### Meteor 1.3
To transfer the application, on the command line, type:
`DEPLOY_HOSTNAME=galaxy.meteor.com meteor authorized [your_existing_hostname] --transfer [new_account_name]`

### Meteor < 1.2
To transfer the application, on the command line, type:
`DEPLOY_HOSTNAME=galaxy.meteor.com meteor authorized [your_existing_hostname] --add [new_account_name]`

You need to have deploy privileges to the account `new_account_name`.
