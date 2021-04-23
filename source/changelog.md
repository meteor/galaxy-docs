---
title: Changelog
description: List of changes on Galaxy
---

# 2021/04/23

- API:
  - new `startApp` and `stopApp` mutations.
  
# 2021/02/17

- Logs
  - Filter logs between two dates

# 2021/01/16

- Cloud UI Update

# 2020/11/12

- Security:
  - New app protection features, fine tune how many requests do you want to accept and control each block individually.

# 2020/11/04

- API:
  - new `createdAt` field on Container type.

# 2020/11/03

- Core:
  - Free deploy with Cold start (meteor deploy --free).
  - MongoDB included (meteor deploy --mongo).

# 2020/10/27

- UI:
  - It's now possible to set the minimum supported version of TLS on each app by going to:
  Settings -> Security -> SSL TLS Protocol support
- Proxy:
  - The proxy layer now blocks requests based on TLS app security configuration.


# 2020/09/30

- UI:
  - Search by container id on containers tab inside your app
  <img src="/images/galaxy-container-filter.png" />
  
  - See your app ID in the tooltip of app status green circle
- Containers:
  - New container sizes: Octa (8 ECUs and 8 GBs of RAM) and Dozen (12 ECUs and 12 GBs of RAM)

# 2020/09/27

- API:
  - Support custom certificates

# 2020/09/17

- UI:
  - Bug fix on loops with notifications resulting in a better performance in the UI as well.
- Deploys:
  - Better performance
  - Timeouts were increased as well
  - Build cache support (Meteor 1.11)
  
# 2020/09/08

- UI:
  - Support for private cluster in the UI, now clients with private clusters can move their apps back and forth to the public clusters using the UI
  
# 2020/08/26

- Logs:
  - Better performance when loading the logs

# 2020/08/20

- Domains:
  - Enable unicode domains on galaxy - change regexp for turkish characters
  
# 2020/08/13

- API:
  - Domains: Adds a new mutation to Galaxy GraphQL API that enables the upsert of domains with automatic certificate generation. For more details, please refer to the graphql docs API on [API Explorer](https://us-east-1.api.meteor.com/explorer) - saveDomain(domain: DomainInput!): Domain. 

# 2020/08/07

- Logs:
  - Adds option to go back in date with a date picker
  - Improves performance for long logs listing by virtualization
  - Adds a shortcut on the timestamp of a log to quickly jump to a date
  - More details on the video below:
  
  [![](http://img.youtube.com/vi/WPYyHeWM21Q/0.jpg)](http://www.youtube.com/watch?v=WPYyHeWM21Q "")

# 2020/07/30

- Security:
  - 2FA
  - App Protection

# 2020/07/16

- Triggers:
  - Kill container trigger
  
# 2020/07/02

- Activities:
  - Hides app unavailable activities from the right side bar
  
# 2020/06/29

- Activities:
  - Hides container unhealthy activities from the right side bar
  
# 2020/06/25

- Notifications:
  - Fixes link to Notifications doc
  - Fixes the state of Notifications settings after save
- Misc:
  - Exposes all the states on invoices list in the account settings page


# 2020/06/05

- Triggers:
  - Labels changed: Series to Sample duration, Metrics quantity to Sample quantity and Seconds interval to Run every (seconds).
  - Fixed alignments and spacing.
  - Fixed validation between min and max containers.

# 2020/06/04

- Triggers:
  - Changed the color to indicate when a day of week is enabled.
  - Fixed validations on Advanced Settings and Rules.

# 2020/06/03

- Released [Triggers (Autoscaling)](./triggers.html)
