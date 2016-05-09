---
title: Domains
order: 13
description: Learn how to make an application accessible via a custom domain name
---

You can specify one or more hostnames for an application. Galaxy will make the app be available on those hostnames. These hostnames can be on a custom domain, or can use the Galaxy provided .meteorapp.com domain.

<h3 id="command-line">When first deploying</h3>

When first deploying specify the hostname through the command line:

`DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy [hostname] --settings path-to-settings.json`

Once your app is successfully deployed to Galaxy make sure to [configure your DNS](/dns.html) to make that hostname  accessible.

If you want to change the primary hostname of your app then deploy a new app at the designated hostname. Once that's deployed, you can safely delete the old app.

`DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy [new_hostname] --settings path-to-settings.json`

<h3 id="meteorapp-subdomain">.meteorapp.com</h3>

Galaxy provides subdomains on .meteorapp.com for use by any app deployed to Galaxy. You can deploy apps to `<custom.subdomain>.meteorapp.com` as the host.

<h3 id="add-domain">Adding additional domains</h3>

You can access the same app from multiple domains by adding custom domains. Just navigate to the **Domains & Encryption** section of your app's settings page and add new domains via the user interface.

<img src="/images/email-add-domain.png"/>

<h3 id="troubleshooting">Troubleshooting</h3>

- `This host domain is already in use on Galaxy` The specified domain is being utilized by another application on Galaxy. Deploy your application to a different domain name.

- `hostname: Requested domain contains invalid characters.` The specified domain name has invalid characters. Domain names need to consist of lowercase letters & numbers. The top level domain can only be lowercase letters.
