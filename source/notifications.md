---
title: Notifications
order: 33
description: Learn how to set Galaxy's notification to your account and apps
---

<h2 id="what-it-does">What it does</h2>

With the notifications on, you will be able to receive notification through either your slack or email.

<h2 id="account-settigs">Account settings</h2>

Let's begin setting the account settings. Go to <b>https://<your-region\>/<your-account\>/settings</b>, bellow the section PLAN, your will see the section NOTIFICATIONS.

When you click on CHANGE, if you already have an account, the two available options, email and slack, will be disabled. If you just create the account, the email option will be enabled with some activities already checked.

<h3 id="setting-email">Setting Email</h3>

To enable the email is pretty straightforward. You just need to click on ENABLE EMAIL NOTIFICATIONS and choose which of the activities do you want to receive email about and click on the SAVE in the end of the section. 

Now, if you have a user account, nothing more will have to be done. But if you have an organization account, you'll have to set which members should receive the emails.

You can do this going to <b>https://<your-region\>/<your-account\>/manage</b> and bellow EMAIL NOTIFICATIONS you will see all members of your organization. If you just created the account, your card will be green, meaning you are already enabled to receive the emails by default. If you already have an account, all members will be disabled. To enable or disable a member just click on they card and, after set this up, hit the save button.

Now it is done!  All chosen members will receive the notifications by email.

<h3 id="setting-slack">Setting Slack</h3>

Fist of all, you will need to add an Incoming WebHooks app to a channel in your Slack . You can see how to do so [here](https://slack.com/intl/en-br/help/articles/202035138-Add-an-app-to-your-workspace). Once you get your URL (that will be something like this: https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX ), go to <b>https://<your-region\>/<your-account\>/settings</b> and in the NOTIFICATION SETTINGS, click in ENABLE SLACK NOTIFICATIONS.

You can go ahead and paste your URL in the <b>Slack Incoming WebHooks URL</b> field. In the table bellow this field you can choose which activities do you want to receive notifications, and you also can fill the <b>Custom Slack Channel</b> with a name of an existing channel that you have in you slack account. With this, you can have different activity notifications to different channels. If you don't fill this field, we will send the notification to the channel that you first used to install the Incoming WebHooks app in your slack.

<img src="/images/slack-notifications-example.png" style="width: 775px"/>

After setting everything up, just hit the save button and all will be done!

<h2 id="app-settings">App settings</h2>

The settings above will be applied to all your account's app. But you can custom these settings by each app.

On you account, choose an app that you what to have a custom notification settings. Then go to settings and, bellow DOMAINS & ENCRYPTION you'll see NOTIFICATIONS. When you click in CHANGE the button ENABLE CUSTOM APP NOTIFICATIONS will appear, once you click in this button, the same options from your account's notification setting will be displayed.

Now, for example, if you click on ENABLE CUSTOM APP NOTIFICATIONS, keeping the Email and Slack options disabled, and hit SAVE, you will be disabling the notifications for that app. That means that you have control over all your applications. Each application can have a Custom Slack Channel for the same activity, or even a different Slack per application, for example.

The way to set up the Email and Slack option here is the same from <b>Account Settings</b>.