---
title: Billing
order: 70
description: Learn how Meteor Cloud bills per plan and container size
---

<h2 id="billing-usage">Flexible Payment Options</h2>

We have four different plan levels to choose from, which fit many different use cases.  
- Free Plan
- Essential 
- Professional
- Enterprise

Deciding which plan best suits your needs will be based on features available for each plan, as well as the container sizes and usage needed for your app. Your pricing varies with the plan selected and the quantity and size of containers used to run your app, pro-rated to the second. **Note: Free accounts support up to 1 Tiny container per app**. 

All Meteor Cloud accounts start on the Free Plan. Once you have an app deployed, your account will be charged depending on your container size and plan selected on your Meteor Cloud Dashboard. You pay for only what you use. If stop or delete all of your running apps, you will not be charged.

For all paid accounts, billing from the beginning to the end of the month will be billed at the beginning of the following month. If you stop or delete your app during the month, you’ll only be billed for your usage until the point when you stop or delete your app. 

Container usage pricing (monthly):

Approximate costs, per container/plan 
- Tiny: 256MB RAM, 0.3 ECU. Essential: $9 / month: Professional:  $18 / month
- Compact: 512MB RAM, 0.5 ECU. Essential: $29 / month. Professional:  $40 / month
- Standard: 1GB RAM, 1 ECU. Essential: $58 / month. Professional: $79 / month
- Double: 2GB RAM, 2 ECU. Essential: $115 / month. Professional: $158 / month
- Quad: 4GB RAM, 4 ECU. Essential: $230 / month. Professional: $317 / month

Please note that prices are estimated for a container running 30 days (billed by hour).

Container options: 

| Container | Tiny    | Compact | Standard  | Double  | Quad   |
|-----------|---------|---------|-----------|---------|--------|
| Memory    | 256mb   | 512mb   | 1GB       | 2GBs    | 4GBs   |
| CPU       | 0.3 ECU | 0.5 ECU | 1 ECU     | 2 ECUs  | 4 ECUs |

Plan costs: 
 
 - Professional: 0.11 per hour 
 - Essential: 0.08 per hour
 
Apps running Tiny Containers benefit from a cost reduction on both the Essential (0.01 per hour) and Professional (0.025 per hour) plans. 

Pricing is impacted by:
- Plan type (Free, Essential, Professional or Enterprise)
- Number of running containers
- Size of running containers

Pricing is not impacted by:
- Number of connected clients/traffic
- Number of command line deployments
- Number of users
- Environment (Development, Testing, Staging or Production)

Push to Deploy deploys are charged using the same cost per hour per GB as the plan of your app.

If you’d like to economize, consider using a savings plan. Contact support@meteor.com for more details.

<h2 id="cloud-plans">Meteor Cloud Plans</h2>

You can see the differences between our plans in our [website](https://www.meteor.com/cloud#pricing-section).

<h2 id="savings-plan">Savings Plan</h2>

Savings plans are simple. All we need is an approximate forecast on what you might spend in the coming 12 months. This is usually an average of your monthly bill, and multiplied by 12 calendar months. From there, we can provide you with an accurate quote for your pre-payment, which allows you to save 20% overall on your costs. 

If you decide to move forward with pre-payment, but might grow in the next 6-12 months, we can also provide you with additional savings credits later on so you continue to save while you grow. 

Contact support@meteor.com if you'd like to add savings plan to your account.

<h2 id="billing-update">Payment and statements</h2>

Meteor Cloud accepts PayPal and major credit cards: Visa, MasterCard, American Express, and Discover. You may view and change payment details in your account settings page.

Every month a statement is emailed for your total monthly usage. Statements show metered usage broken out by app. You may view and download past statements in your Meteor Cloud account profile for individual users, and organization pages for teams.

<h2 id="stopping-charges">Stopping Charges</h2>

While you can’t change charges for resources used in the past, you can minimize charges, going forward, by stopping your apps or deleting your account. Please note that, if you stop your app during the month, you won’t be charged for usage until after the end of the billing period, typically the end of the month.

To be charged the minimum fees, you must reduce your containers in every region where they are running to the Tiny Container option. To check your regions, add your account name to the end of https://galaxy.meteor.com/, https://eu-west-1.galaxy.meteor.com/ and https://ap-southeast-2.galaxy.meteor.com/ and make sure you have no running apps.

Every app listed in your account will have a full gray circle next to it, if its containers have been stopped.  If you're sure that you'll never reuse the containers in an app, you can delete the app to permanently remove it. 

There is no cost difference between deleting or stopping your apps.

<h2 id="preventing-interruptions">Preventing Service Interruptions</h2>

If Meteor Cloud is unable to charge your account, the account address you have on file will be emailed a warning. Whenever a payment fails, we will send your account an email notification.

If, after receiving a warning or multiple warnings, the charge remains unpaid, your account may be suspended. Since Meteor Cloud charges for services already rendered, this prevents unpaid charges from growing larger. 

Typical reasons for account suspension include:
- your payment information is out of date
- your bank will not allow the charge to go through
- your bank requires your express permission before Galaxy can charge it

If you need to change your payment information, or have talked to your bank to enable your card to be charged, contact support@meteor.com for assistance.

As long as your account is suspended, you won't be able to deploy, start or run containers on your account.

Once the invoiced amount is successfully paid, your full account functionality will be restored. 

To avoid service interruptions for billing-related reasons, make sure you have an email address that you regularly check for notifications. Ensure you have a current and working payment method at all times. 

If your invoice is past due, update your payment information at the earliest possible opportunity to prevent any interruptions in service.  

