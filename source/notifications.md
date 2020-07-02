---
title: Notifications
order: 34
description: Learn how to set Galaxy's notification to your account and apps
---

Galaxy notifications are the best way to stay informed about your apps running on Galaxy. We support notifications via Slack and Email.

<h2 id="activity-types">Activity Types</h2>

Notifications are sent when actvitiy occurs in your account:

<img src="/images/notifications-activities.png" style="max-width: 40%"/>

We recommend activating notifications for at least these types:
- Deploy failed
- Build failed temporarily
- Build failed permanently
- App automatically stopped
- Certificate generation error

In order for you to ensure minimal disruption, should critical issues occur. 

It could be also important to enable these types below if your app can consume too much CPU or Memory, then you can receive notifications when this starts to affect your users, these activities also produce logs in the service tab:
- Container unhealthy
- App unavailable

<h2 id="usage">Usage</h2>

<h3 id="account-settigs">Account settings</h3>

Let's begin configuring your account settings. Go to your Galaxy dashboard and click in the Settings tab of your account. Below the section PLAN, you will see the section NOTIFICATIONS.

When you click on CHANGE, if your account was created before Notifications existed on Galaxy, everything will be disabled. If your account was created when Notifications were already on Galaxy, the email option will be enabled with some type of activities already checked.

<h4 id="email-settings">Email Settings</h4>

Enabling email notifications is simple. You just need to click on ENABLE EMAIL NOTIFICATIONS and choose which types of activity you want to receive an email about, then click SAVE at the end of the section. 

If you have an individual account, nothing more needs to be done. If you have an organization account, you'll have to set which members of your organization should receive the emails.

You can do this by going to your Galaxy dashboard and clicking in the MEMBERS tab. Below EMAIL NOTIFICATIONS you will see all members of your organization. If you just created the account, your card will be green, meaning you are already enabled to receive the emails by default. If you already have an account, all members will be disabled. To enable or disable a member just click on their card, then hit the save button.

Then you're good to go! All chosen members will receive the notifications by email.

<h4 id="slack-settings">Slack Settings</h4>

First, you will need to add an Incoming WebHooks to a channel in your Slack. To do this, please go to [this page](https://slack.com/intl/en-br/help/articles/202035138-Add-an-app-to-your-workspace). 

Once you get your URL (that will be something like this: https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX ), go to your Galaxy dashboard. In the NOTIFICATION SETTINGS, click in ENABLE SLACK NOTIFICATIONS.

You can go ahead and paste your URL in the <b>Slack Incoming WebHooks URL</b> field. In the table below this field you can choose which activities you want to receive notifications for, and you also can fill the <b>Custom Slack Channel</b> with a name of an existing channel that you have in you slack account. With this, you can receive different activity notifications to different channels. If you don't fill this field, we will send the notification to the channel that you first used to install the Incoming WebHooks app in your Slack.

<img src="/images/notifications-slack-settings.png" style="max-width: 80%"/>

After setting everything up, just hit the save button!

<h3 id="app-settings">App Settings</h3>

The settings above will be applied to every app in your account. However, you can customize these settings for each app.

To do so, choose an app that you want to have a custom notification settings, then go to settings. Below DOMAINS & ENCRYPTION you'll see NOTIFICATIONS. When you click on CHANGE the button ENABLE CUSTOM APP NOTIFICATIONS will appear. When you click this button, the same options from your account's notification setting will be displayed. From now on all notifications for this app will behave respecting the app settings and not the account settings.

Now, for example, if you click on ENABLE CUSTOM APP NOTIFICATIONS, keeping the Email and Slack options disabled, and hit SAVE, you will be disabling the notifications for that app. This means you have control over the notifications on each app. Each application configuration is independent, you can customize everything at the app level!

The way to set up the Email and Slack option here is the same from <b>Account Settings</b>.
