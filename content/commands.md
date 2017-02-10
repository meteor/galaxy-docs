---
title: Commands
order: 46
description: A reference for Galaxy's commands
---

<h2 id="deployment">Deployment</h2>

The deployment command is as follows:

`DEPLOY_HOSTNAME=[region] meteor deploy [hostname] --settings [path-to-settings-file]`

- `region` should be us-east-1.galaxy.meteor.com for the US region and eu-west-1.galaxy.meteor.com for the EU region
- `hostname` is the fully qualified domain name where you’re planning to host your application (for example, ‘www.facebook.com’).
- `path-to-settings-file` is the path to your JSON settings file (for example, ‘./settings.json’).

On Windows, this command should be split into two separate commands, with `DEPLOY_HOSTNAME=...` changed to `SET DEPLOY_HOSTNAME...` and occupying one line, and `meteor deploy` occupying another line.

<h2 id="transfer-app">Transfer application</h2>

- Transfer with Meteor 1.3 or higher versions: `DEPLOY_HOSTNAME=galaxy.meteor.com meteor authorized [your_existing_hostname] --transfer [new_account_name]`

- Transfer with Meteor 1.2 or lower versions: `DEPLOY_HOSTNAME=galaxy.meteor.com meteor authorized [your_existing_hostname] --add [new_account_name]`

For this to work, you must have deploy privileges to the account `new_account_name`.

<h2 id="login">login</h2>

`meteor login` will prompt you for a username and password to log you in, given the correct credentials.

<h2 id="login-token">login with token</h2>

`METEOR_SESSION_FILE=[token-file] meteor login` will use a deployment token (good for 90 days from the time of generation) to log you in.

- token-file is the path to your JSON deployment token file (for example, ‘./token.json’).

<h2 id="logout">logout</h2>

`meteor logout` will log you out as the current user.

<h2 id="whoami">whoami</h2>

`meteor whoami` will tell you which user you are logged in as. This can be important if you are a member of one or more organizations and are having access issues.

<h2 id="mup">mup</h2>

The `mup` utility is not officially supported on Galaxy. While you are free to use it, please know that you may encounter issues with mup that Galaxy support cannot resolve.

