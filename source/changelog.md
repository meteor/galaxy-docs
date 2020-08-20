---
title: Changelog
description: List of changes on Galaxy
---

# 2020/07/13
- API:
  - Adds a new mutation to Galaxy GraphQL API that enables the upsert of domains with automatic certificate generation. For more details, please refer to the graphql docs API on [API Explorer](https://us-east-1.api.meteor.com/explorer) - saveDomain(domain: DomainInput!): Domain. 

# 2020/07/07
- Logs:
  - Adds option to go back in date with a date picker
  - Improves performance for long logs listing by virtualization
  - Adds a shortcut on the timestamp of a log to quickly jump to a date
  - More details on the video below:
  
  [![](http://img.youtube.com/vi/WPYyHeWM21Q/0.jpg)](http://www.youtube.com/watch?v=WPYyHeWM21Q "")

  
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
