---
title: DNS
order: 21
description: Learn how to configure DNS to point to Galaxy
---

Before users can access your application, you must configure your DNS records to point to Galaxy. While the process will be specific to your DNS provider, the general method is the same. Please note that Galaxy is not a DNS provider and you’ll need to use your existing DNS provider to set DNS records.

<h2 id="meteorapp">Included *.meteorapp.com</h2>

You are free to use Galaxy's built-in domain names. SSL is enabled on these domains by default.

If you're in the US region (galaxy.meteor.com), deploy your example app to example.meteorapp.com.

If you're in the EU region (eu-west-1.galaxy.meteor.com), deploy your example app to example.eu.meteorapp.com.

If you're in the Asia-Pacific region (ap-southeast-2.galaxy.meteor.com), deploy your example app to example.au.meteorapp.com.

Substitute in the actual name of your app for 'example'. Beyond that, no DNS configuration is necessary; Galaxy handles all of this for you.

*Note:* example.meteor.com is not available. You cannot deploy to meteor.com domains.

<h2 id="subdomain">Hosting on a subdomain with CNAME</h2>

If your app is deployed at a subdomain such as `www.mycompany.com` or `app.mycompany.com`, simply add a CNAME record to your DNS provider pointing to:

- `us-east-1.galaxy-ingress.meteor.com` for applications in the US East region.

- `eu-west-1.galaxy-ingress.meteor.com` for applications in the EU West region.

- `ap-southeast-2.galaxy-ingress.meteor.com` for applications in the Asia-Pacific region.  

Ensure the hostname you [deployed to](deploy-quickstart.html) matches the [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) of your app (i.e `app.mycompany.com`).

[We recommend you use SSL](encryption.html) as a best practice. You can either enable LetsEncrypt using our integration or upload your own certificate.

<h2 id="root-domain-redirect">Redirecting the root domain</h2>

The root domain is also called the naked or apex domain. A common scenario is when your app is hosted at `www.mycompany.com` and you'd like `mycompany.com` to redirect to the same app. In this scenario, you don't want to emphasize the shorter URL of mycompany.com.

This is done by setting up URL redirection from `mycompany.com` to `www.mycompany.com`. While the way to do this varies by DNS provider, these are common methods we recommend:

* [URL Record at DNSimple](https://support.dnsimple.com/articles/url-record/)
* [Free redirect service from wwwizer](http://wwwizer.com/naked-domain-redirect)

Because another service is hosting the redirect page, you'll need to set up SSL using their methods, which will most likely involve a certificate upload.

<h2 id="hosting-root-domain">Hosting on a root domain using ALIAS</h2>

In this scenario, you do want to emphasize a short URL like mycompany.com. While hosting on a root domain [can introduce complications](http://www.yes-www.org/why-use-www/), it's possible to do by using an ALIAS (also called an ANAME record).

First, you'll need to either deploy your app to the root domain (e.g `myapp.com`) or add the root domain as an [additional domain for your app](custom-domains.html#add-domain). Next, you will need to add an ALIAS record to your DNS provider that points your root domain to `galaxy-ingress.meteor.com`.

Not all DNS providers support this feature and the implementation is usually very specific to each provider. Providers we know and recommend are:

* [ALIAS Record at DNSimple](https://support.dnsimple.com/articles/alias-record/)

*Note:* If you decide to host directly on a root domain, you will likely want to forward `www` to your root domain by setting up URL redirection (see above).

[We recommend you use SSL](encryption.html) as a best practice. You can either enable LetsEncrypt using our integration or upload your own certificate.

<h2 id="dns-propagation">DNS propagation</h2>

DNS is distributed and cooperative, and it takes time for the world to see your changes.  In many countries, it usually updates within about 30 minutes, but it can take up to 24 hours or even longer in some circumstances (depending on the record's TTL).

You can check if your ALIAS or ANAME or CNAME setting was successful in the terminal by typing `dig +show www.mycompany.com`. If your `ANSWER SECTION` includes a record like this, you are in good shape:

```
www.mycompany.com.    1800   IN    CNAME        galaxy-ingress.meteor.com.
```

<h2 id="testing">Testing your DNS changes</h2>

A quick way to test that your app is working is by modifying the `/etc/hosts` file to resolve your app's hostname to the Galaxy load balancer's IP address directly. Note that this will only affect your local machine.

To find out which IP address to use, type `dig +short galaxy-ingress.meteor.com` and choose any of the ones shown. The IP addresses used by Galaxy's load balancer are likely to change, so you may need to do this process more than once.

Add a line to `/etc/hosts` (Windows: `c:\windows\system32\drivers\etc\hosts`) that contains:

```
[Galaxy's current ip address]   [Your app's hostname, e.g app.mycompany.com]
```

To ensure your changes take effect, you can reset your computer's local DNS cache with `sudo dscacheutil -flushcache` (Mac; see [other OSes](https://www.whatsmydns.net/flush-dns.html)) after making your changes.

<h2 id="other-issues">Other issues</h2>

Galaxy is not a DNS record provider. Our support is focused on configuring your settings to work with Galaxy apps, as described in the sections above.

If you have additional issues which reach beyond the scope of this article, you may need to contact your DNS record provider to resolve them. 