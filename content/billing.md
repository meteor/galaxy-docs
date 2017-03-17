---
title: Billing
order: 50
description: Learn how Galaxy bills per container
---

<h2 id="billing-usage">Pay for what you use</h2>

Billing is based on Galaxy container usage, pro-rated to the second. Your metered pricing varies with the quantity and size of containers used to run your apps.

Billing begins when you deploy and stops when you stop or delete your app. With the current pricing, it will cost you less than $0.17 to run a compact container for 4 hours.

If you want to stop billing, stop your app; billing will stop from that point onwards, even though the app is still visible in the UI and can be restarted at any time.

Billing from the beginning to the end of the month will be billed at the beginning of the following month. If you stopped or deleted your app during the month, you'll only be billed for your usage until the point when you stopped or deleted your app.

Container usage pricing:

- Galaxy (all regions): $0.08 per GB/hour

Customers who signed up prior to August 2016 may belong to a legacy Galaxy plan where pricing varies by plan, support tier selected, containers used, and container size. 

Pricing is impacted by:
- Number of running containers
- Size of running containers

Pricing is **not** impacted by:

- Memory or CPU usage of your app
- Number of connected clients/traffic
- Number of deploys or users

<h2 id="reserved-pricing">Prepaid Pricing</h2>

Galaxy Prepaid Pricing guarantees a specific amount of container capacity at a discounted price compared to pay-as-you-go pricing. 

By paying upfront for container capacity, you’ll receive ~20% off the equivalent pay-as-you-go rates. Galaxy Prepaid Pricing currently costs $45 USD per GB RAM month (available in 1 GB increments only, billed annually). 

Any usage during the month beyond the reserved base capacity will be billed at normal metered rates. To add Prepaid Pricing to your account, simply log a support ticket from within Galaxy and let us know how many GB's you want to reserve.

Contact <a href="mailto:galaxysales@meteor.com">galaxysales@meteor.com</a> if you'd like to add this to your account.

<h2 id="billing-update">Payment and statements</h2>

Galaxy accepts PayPal and major credit cards: Visa, MasterCard, American Express, and Discover. You may view and change payment details in your account settings page.

Every month a statement is emailed for your total monthly usage. Statements show metered usage broken out by app. You may view and download past statements in your Galaxy account settings.

<h2 id="stopping-charges">Stopping Charges</h2>

While you can't stop charges for resources used in the past, you can stop charges, going forward, by stopping or deleting your apps.

At a minimum, you must stop your containers in every region where they are running. To check both regions, add your account name to the end of https://galaxy.meteor.com/ and https://eu-west-1.galaxy.meteor.com/.

Every app listed in your account will have a gray circle next to it, if its containers have been stopped.  If you're sure that you'll never reuse the containers in an app, you can delete the app to permanently remove it. There is no cost difference between deleting or stopping your app.

There is no charge to maintain an account on Galaxy, if none of your containers are running. If you leave your account open, you can return at any time.


