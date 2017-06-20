---
title: Billing
order: 70
description: Learn how Galaxy bills per container
---

<h2 id="billing-usage">Pay for what you use</h2>

Billing is based on Galaxy container usage, pro-rated to the second. Your metered pricing varies with the quantity and size of containers used to run your apps.

Billing begins when you deploy and stops when you stop or delete your app. With the current pricing, it will cost you less than $0.17 to run a compact container for 4 hours.

If you want to stop billing, stop your app; billing will stop from that point onwards, even though the app is still visible in the UI and can be restarted at any time.

Billing from the beginning to the end of the month will be billed at the beginning of the following month. If you stop or delete your app during the month, you'll only be billed for your usage until the point when you stop or delete your app.

Container usage pricing:

- Galaxy Essentials (all regions): $0.08 per GB/hour
- Galaxy Professional (all regions): $0.11 per GB/hour

Customers who signed up prior to August 2016 may belong to a legacy Galaxy plan where pricing varies by plan, support tier selected, containers used, and container size. Please note there is no free tier on Galaxy.

Pricing is impacted by:
- Type of running containers
- Number of running containers
- Size of running containers

Pricing is **not** impacted by:

- Memory or CPU usage of your app
- Number of connected clients/traffic
- Number of deploys or users

If you'd like to economize, consider using a prepaid pricing plan, or stopping your app during low volume or low traffic periods throughout the month.

<h2 id="galaxy-professional">Galaxy Professional</h2>

Galaxy Professional includes Meteor APM, IP whitelisting, and prioritized support to help developers deploy and manage production apps with confidence. You can turn on Galaxy Professional containers with a single click for any of your apps on Galaxy.

You can select Essentials or Professional containers to run specific apps in your Galaxy account.

<h2 id="reserved-pricing">Prepaid Pricing</h2>

Galaxy Prepaid Pricing guarantees a specific amount of container capacity at a discounted price compared to pay-as-you-go pricing.

By paying upfront for container capacity, you’ll receive ~20% off the equivalent pay-as-you-go rates. Galaxy Prepaid Pricing is available for Galaxy Essentials and Professional container types (available in 1 GB increments only, billed annually). Prepaid capacity is not transferable between container types.

Any usage during the month beyond the prepaid capacity will be billed at normal metered rates for that container type. To add Prepaid Pricing to your account, simply log a support ticket from within Galaxy and let us know which container type (Essentials or Pro) and how many GB's you need.

Contact <a href="mailto:galaxysales@meteor.com">galaxysales@meteor.com</a> if you'd like to add prepaid capacity to your account.

<h2 id="billing-update">Payment and statements</h2>

Galaxy accepts PayPal and major credit cards: Visa, MasterCard, American Express, and Discover. You may view and change payment details in your account settings page.

Every month a statement is emailed for your total monthly usage. Statements show metered usage broken out by app. You may view and download past statements in your Galaxy account settings.

<h2 id="stopping-charges">Stopping Charges</h2>

While you can't stop charges for resources used in the past, you can stop charges, going forward, by stopping or deleting your apps. Please note that, if you stop your app during the month, you won't be charged for usage until after the end of the billing period, typically the end of the month.

At a minimum, you must stop your containers in every region where they are running. To check your regions, add your account name to the end of https://galaxy.meteor.com/, https://eu-west-1.galaxy.meteor.com/ and https://ap-southeast-2.galaxy.meteor.com/ and make sure you have no running apps.

Every app listed in your account will have a full gray circle next to it, if its containers have been stopped.  If you're sure that you'll never reuse the containers in an app, you can delete the app to permanently remove it. There is no cost difference between deleting or stopping your app.

There is no charge to maintain an account on Galaxy, if none of your containers are running. If you leave your account open, you can return at any time.
