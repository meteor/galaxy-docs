---
title: Encryption
order: 22
description: Learn how to enable SSL encryption to secure sensitive data
---

SSL encryption is a security protocol to encrypted connections between servers and clients. We highly recommend that you enable SSL encryption to secure your app's sensitive data and to avoid issues with websockets connecting from behind certain firewalls. Galaxy provides two ways to enable encryption: generating a Let's Encrypt certificate or uploading your own custom certificate. Additionally, a "Force HTTPS" option can be enabled on each domain to ensure connections over HTTP are redirected to HTTPS.

<h2 id="custom-domain">Before you begin</h2>

Encryption is automatically enabled for all apps deployed to the .meteorapp.com subdomain. To enable encryption for custom domains, you must first [add a custom domain](/custom-domains.html) on your app settings page and [configure your DNS](/dns.html) to point at Galaxy's DNS. Once added, click on your custom domain to see SSL encryption options.

<h2 id="lets-encrypt">Let's Encrypt</h2>

To enable encryption painlessly, we recommend generating a free [Let's Encrypt](https://letsencrypt.org/) certificate via Galaxy. In just one click Galaxy generates an SSL certificate and configures it for your custom domain.

In order for Galaxy to generate a certificate for your site, we need to be able to convince the LetsEncrypt certificate authority that we are the legitimate host for that site. We do that by serving up special data in response to special URLs under your domain. This works great if you configure your domain's DNS to point directly to Galaxy via a CNAME but can get more complex if you put another proxy layer like Cloudflare in front.

Specifically, we expect to be able to fetch the URL `http://example.com/.well-known/acme-challenge/_g_selfcheck_` and get a 200 with a certain random-looking body. You can see this working by looking at `http://www.meteor.com/.well-known/acme-challenge/_g_selfcheck_`. Galaxy serves this special URL automatically for you, so you need to ensure that any proxy layer you put in front of Galaxy passes requests starting with `/.well-known/acme-challenge` through to Galaxy.
We do follow redirects. You can test that your site will pass the test by running `curl -i -L http://example.com/.well-known/acme-challenge/_g_selfcheck_` (substituting the name of your domain for `example.com`).

<img src="images/email-enable-ssl.png" style="width: 780px;">

Galaxy does not support auto-renewing Let's Encrypt certificates for wildcard (\*.) domains, because the mechanism for obtaining those certificates would require you to delegate DNS management for your domain to Galaxy.

<h2 id="Custom certificate">Custom certificate</h2>

You can also upload a custom key and certificate. Private keys and certificates should be in the PEM format (this is the same format used by nginx). If intermediate certificates are used in addition to the primary certificate, they should be placed in the same file as the primary certificate. The primary certificate should come first, followed by the intermediate certificates.
