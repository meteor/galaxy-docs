---
title: Notifications
order: 33
description: Learn how to set Galaxy's notification to your account and apps
---

Galaxy's notifications is the best way to receive news about your apps running on Galaxy. We support notifications via Slack and Email.

<h2 id="activity-types">Activity Types</h2>

The notifications are sent when you have new activities in your apps.

<img src="/images/notifications-activities.png" />

We believe you should at least activate the notifications for:
- Deploy failed
- Build failed temporarily
- Build failed permanently
- App automatically stopped
- Container unhealthy
- App unavailable
- Certificate generation error

So Galaxy will reach you out as soon as these activites happen.

<h2 id="usage">Usage</h2>

<h3 id="account-settigs">Account settings</h3>

Let's begin configuring your account settings. Go to your Galaxy dashboard and click in the Settings tab of your account, bellow the section PLAN, you will see the section NOTIFICATIONS.

When you click on CHANGE, if your account was created before Notifications existed on Galaxy everything will be disabled. If your account was created when Notifications were already on Galaxy so the email option will be enabled with some type of activities already checked.

<h4 id="email-settings">Email Settings</h4>

To enable the email is pretty straightforward. You just need to click on ENABLE EMAIL NOTIFICATIONS and choose which types of activity you want to receive an email about and click on the SAVE in the end of the section. 

Now, if you have an individual account, nothing more needs to be done. But if you have an organization account, you'll have to set which members of your organization should receive the emails.

You can do this going to your Galaxy dashboard and clicking in the MEMBERS tab, bellow EMAIL NOTIFICATIONS you will see all members of your organization. If you just created the account, your card will be green, meaning you are already enabled to receive the emails by default. If you already have an account, all members will be disabled. To enable or disable a member just click on their card and, after set this up, hit the save button.

Now it is done! All chosen members will receive the notifications by email.

<h4 id="slack-settings">Slack Settings</h4>

Fist of all, you will need to add an Incoming WebHooks to a channel in your Slack. You can see how to do this [here](https://slack.com/intl/en-br/help/articles/202035138-Add-an-app-to-your-workspace). 

Once you got your URL (that will be something like this: https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX ), go to your Galaxy dashboard and in the NOTIFICATION SETTINGS, click in ENABLE SLACK NOTIFICATIONS.

You can go ahead and paste your URL in the <b>Slack Incoming WebHooks URL</b> field. In the table bellow this field you can choose which activities do you want to receive notifications, and you also can fill the <b>Custom Slack Channel</b> with a name of an existing channel that you have in you slack account. With this, you can have different activity notifications to different channels. If you don't fill this field, we will send the notification to the channel that you first used to install the Incoming WebHooks app in your Slack.

<img src="/images/slack-notifications-example.png" style="width: 775px"/>

After setting everything up, just hit the save button and all will be done!

<h3 id="app-settings">App Settings</h2>

The settings above will be applied to every app in your account but you can customize these settings for each app.

On you account, choose an app that you want to have a custom notification settings. Then go to settings and, bellow DOMAINS & ENCRYPTION you'll see NOTIFICATIONS. When you click on CHANGE the button ENABLE CUSTOM APP NOTIFICATIONS will appear, once you click in this button, the same options from your account's notification setting will be displayed. From now on every notification for this app will behave respecting the app settings and not the account settings.

Now, for example, if you click on ENABLE CUSTOM APP NOTIFICATIONS, keeping the Email and Slack options disabled, and hit SAVE, you will be disabling the notifications for that app. That means you fine control over the notifications on each app, if you want. Each application configuration is independent, you can customize everything in the app level.

The way to set up the Email and Slack option here is the same from <b>Account Settings</b>.
