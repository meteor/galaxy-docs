---
title: Changelog
description: List of changes on Meteor Cloud
---

## New Changelog for Meteor Cloud (2022/11/21)

Now you can follow our updates closely and stay informed about everything Meteor Cloud related!

Subscribe to our new Changelog on https://cloud-news.meteor.com and receive all the Meteor Cloud news by email.

*This Changelog page will not receive new updates.*

## v3.2.1

- Updated Whitelisting IPs. To find out more, go to your app settings.

## v3.2

- Updated Override Meteor Settings (previously Next auto deploy settings)

## v3.1

- One Time Password on Meteor Accounts
  - [Read more](https://forums.meteor.com/t/2fa-otp-support-in-meteor-accounts-meteor-cloud/57248)

## v3.0 (2021/12/16)

- Push to Deploy
  - [Read more](https://blog.meteor.com/introducing-push-to-deploy-6ea464ee5f33).
- Improvements to Apps List page
- Improvements to App Details page

## v2.5 (2021/11/12)

- Logs
  - Download logs button now exports all the logs from your app. As we store 7 days of logs you can download them all in a single click. Before the same button was limited to download 10,000 lines of logs.

## v2.4 (2021/08/19)

- Security
  - Always forcing HTTPs and generating LetsEncrypt certificate to a domain, by default, when deploying an app for the first time.

## v2.3 (2021/07/23)

- Triggers
  - Improve the triggers to avoid scaling down during deploys.

## v2.2 (2021/06/18)

- Free deploys
  - Increase Cold Start timeout to 30 minutes

## v2.1 (2021/05/09)

- Security
  - Update PEM package for new openssl executable on Ubuntu 20.04

## v2.0 (2021/04/23)

- Deploy
  - new Docker default base image. [read more](./base-image-packages.html#v2.0)

## v1.22 (2021/04/23)

- API
  - new `startApp` and `stopApp` mutations.

## v1.21 (2021/02/17)

- Logs
  - Filter logs between two dates.

## v1.20 (2021/01/16)

- Cloud UI Update

## v1.19 (2020/11/12)

- Security:
  - New app protection features, fine tune how many requests do you want to accept and control each block individually.

## v1.18 (2020/11/04)

- API:
  - new `createdAt` field on Container type.

## v1.17 (2020/11/03)

- Core:
  - Free deploy with Cold start (meteor deploy --free).
  - MongoDB included (meteor deploy --mongo).

## v1.16 (2020/10/27)

- UI:
  - It's now possible to set the minimum supported version of TLS on each app by going to:
    Settings -> Security -> SSL TLS Protocol support
- Proxy:
  - The proxy layer now blocks requests based on TLS app security configuration.

## v1.15 (2020/09/30)

- UI:

  - Search by container id on containers tab inside your app
    <img src="/images/galaxy-container-filter.png" />

  - See your app ID in the tooltip of app status green circle

- Containers:
  - New container sizes: Octa (8 ECUs and 8 GBs of RAM) and Dozen (12 ECUs and 12 GBs of RAM)

## v1.14 (2020/09/27)

- API:
  - Support custom certificates

## v1.13 (2020/09/17)

- UI:
  - Bug fix on loops with notifications resulting in a better performance in the UI as well.
- Deploys:
  - Better performance
  - Timeouts were increased as well
  - Build cache support (Meteor 1.11)

## v1.12 (2020/09/08)

- UI:
  - Support for private cluster in the UI, now clients with private clusters can move their apps back and forth to the public clusters using the UI

## v1.11 (2020/08/26)

- Logs:
  - Better performance when loading the logs

## v1.10 (2020/08/20)

- Domains:
  - Enable unicode domains on galaxy - change regexp for turkish characters

## v1.9 (2020/08/13)

- API:
  - Domains: Adds a new mutation to Galaxy GraphQL API that enables the upsert of domains with automatic certificate generation. For more details, please refer to the graphql docs API on [API Explorer](https://us-east-1.api.meteor.com/explorer) - saveDomain(domain: DomainInput!): Domain.

## v1.8 (2020/08/07)

- Logs:

  - Adds option to go back in date with a date picker
  - Improves performance for long logs listing by virtualization
  - Adds a shortcut on the timestamp of a log to quickly jump to a date
  - More details on the video below:

  [![](https://img.youtube.com/vi/WPYyHeWM21Q/0.jpg)](http://www.youtube.com/watch?v=WPYyHeWM21Q)

## v1.7 (2020/07/30)

- Security:
  - 2FA
  - App Protection

## v1.6 (2020/07/16)

- Triggers:
  - Kill container trigger

## v1.5 (2020/07/02)

- Activities:
  - Hides app unavailable activities from the right side bar

## v1.4 (2020/06/29)

- Activities:
  - Hides container unhealthy activities from the right side bar

## v1.3 (2020/06/25)

- Notifications:
  - Fixes link to Notifications doc
  - Fixes the state of Notifications settings after save
- Misc:
  - Exposes all the states on invoices list in the account settings page

## v1.2 (2020/06/05)

- Triggers:
  - Labels changed: Series to Sample duration, Metrics quantity to Sample quantity and Seconds interval to Run every (seconds).
  - Fixed alignments and spacing.
  - Fixed validation between min and max containers.

## v1.1 (2020/06/04)

- Triggers:
  - Changed the color to indicate when a day of week is enabled.
  - Fixed validations on Advanced Settings and Rules.

## v1.0 (2020/06/03)

- Released [Triggers (Autoscaling)](./triggers.html)

## v0.0

- We started to use this change log at 2020/06/03.
