---
title: Encryption
order: 22
description: Learn how to enable SSL encryption to secure sensitive data
---

SSL encryption is a security protocol to encrypted connections between servers and clients. We highly recommend that you enable SSL encryption to secure your app's sensitive data and to avoid issues with websockets connecting from behind certain firewalls. Galaxy provides two ways to enable encryption: generating a Let's Encrypt certificate or uploading your own custom certificate.  Additionally, a "Force HTTPS" option can be enabled on each domain to ensure connections over HTTP are redirected to HTTPS.

<h2 id="custom-domain">Before you begin</h2>

Encryption is automatically enabled for all apps deployed to the .meteorapp.com subdomain. To enable encryption for  custom domains, you must first [add a custom domain](/custom-domains.html) on your app settings page and [configure your DNS](/dns.html) to point at Galaxy's DNS. Once added, click on your custom domain to see SSL encryption options.

<h2 id="lets-encrypt">Let's Encrypt</h2>

To enable encryption painlessly, we recommend generating a free [Let's Encrypt](https://letsencrypt.org/) certificate via Galaxy. In just one click Galaxy generates an SSL certificate and configures it for your custom domain.

<img src="images/email-enable-ssl.png" style="width: 500px;">

Let's Encrypt certificates are not available for wildcard (*.) domains.

<h2 id="Custom certificate">Custom certificate</h2>

You can also upload a custom key and certificate. Private keys and certificates should be in the PEM format (this is the same format used by nginx). If intermediate certificates are used in addition to the primary certificate, they should be placed in the same file as the primary certificate. The primary certificate should come first, followed by the intermediate certificates.
