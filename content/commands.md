---
title: Commands
order: 46
description: A reference for Galaxy's commands
---

<h2>meteor CLI: Frequently Used Commands</h2>

<h3 id="deployment">deploy</h3>

<h4>Mac and Unix</h4>

`meteor deploy` can be used for creating new apps and updating existing ones.

The full command is:

`DEPLOY_HOSTNAME=[region] meteor deploy [hostname] --settings [path-to-settings-file]`

- `region` should be us-east-1.galaxy.meteor.com for the US region and eu-west-1.galaxy.meteor.com for the EU region
- `hostname` is the fully qualified domain name where you’re planning to host your application (for example, ‘www.facebook.com’).
- `path-to-settings-file` is the path to your JSON settings file (for example, ‘./settings.json’).

You don't have to specify `DEPLOY_HOSTNAME` if:

- your Meteor version is 1.3.3 or higher, and you are deploying to the US region
- your Meteor version is 1.3.3 or higher, you are deploying to the EU region and have already configured your hostname's DNS settings

If your app satisfies these conditions, the deployment command can be simplified to:

`meteor deploy [hostname] --settings [path-to-settings-file]`

<h4>Windows</h4>

On Windows, the deploy command should be split into two separate commands, occupying two separate lines.

`DEPLOY_HOSTNAME=...` should be changed to `SET DEPLOY_HOSTNAME...` and should occupy one line.
`meteor deploy` should occupy another line.

You don't have to set `DEPLOY_HOSTNAME` if you app meets the conditions described above.

<h3 id="transfer-app">transfer</h3>

`meteor authorized` can be used to transfer applications.

- Transfer with Meteor 1.3 or higher versions: `DEPLOY_HOSTNAME=galaxy.meteor.com meteor authorized [your_existing_hostname] --transfer [new_account_name]`

- Transfer with Meteor 1.2 or lower versions: `DEPLOY_HOSTNAME=galaxy.meteor.com meteor authorized [your_existing_hostname] --add [new_account_name]`

For this to work, you must have deploy privileges to the account `new_account_name`.

<h3 id="whoami">whoami</h3>

`meteor whoami` will tell you which user you are logged in as.

This can be important for troubleshooting, if you are a member of one or more organizations and are having access issues.

<h3 id="login">login</h3>

`meteor login` will prompt you for a username and password to log you in, given the correct credentials.

<h3 id="login-token">login with token</h3>

`METEOR_SESSION_FILE=[token-file] meteor login` will ask you for your username and password, then create a deployment token you can use to issue other commands, such as the deploy command.

This token will be good for 90 days from the time of generation.

- `token-file` is the path to your JSON deployment token file (for example, ‘./token.json’).

<h3 id="logout">logout</h3>

`meteor logout` will log you out as the current user.

<h3 id="list-sites">list-sites</h3>

`meteor list-sites` lists all the apps you have access to, across all your organizations.

<h3 id="update">update</h3>

`meteor update` allows you to update your Meteor version. You can use the `--release` flag to specify a version.

This can resolve issues involving deployment and application uptime, especially if the Meteor version used to deploy your app significantly predates the most recent Meteor version.


