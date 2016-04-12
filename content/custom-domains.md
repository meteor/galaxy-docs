---
title: Custom Domains
order: 13
description: Learn how to make an application accessible via a custom domain name
---

Todo:
- Custom domains via UI



To make an application accessible via a custom domain name, you must specify the hostname while deploying the application.

Specify the hostname through the command line:

`DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy [hostname] --settings path-to-settings.json`

To change the hostname, use the CLI to deploy the same application to a new hostname:

`DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy [new_hostname] --settings path-to-settings.json`

Ensure that you have configured DNS for the domain:

https://galaxy.meteor.com/help/configuring-dns

Note: There is no longer a need to specify domains up front as part of a whitelist. To utilize a new hostname for your application, just specify that hostname while deploying the application.

*Troubleshooting issues with Domains*

_Error: "This host domain is already in use on Galaxy"_

The specified domain is being utilized by another application on Galaxy. Deploy your application to a different domain name.

_Error: "hostname: Requested domain contains invalid characters."_

The specified domain name has invalid characters. Domain names need to consist of lowercase letters & numbers. The top level domain can only be lowercase letters.
