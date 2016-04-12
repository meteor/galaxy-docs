---
title: meteorapp.com subdomain
order: 5
description: Learn how to use the provided .meteorapp.com subdomain
---

<h3 id="meteorapp-subdomain">.meteorapp.com</h3>

Galaxy provides subdomains on .meteorapp.com for use by any application deployed to Galaxy. You can deploy applications to `<custom.subdomain>.meteorapp.com` as the host.

Specify this host name during `meteor deploy`:
```
DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy <custom.subdomain>.meteorapp.com --settings path-to-settings.json
```
