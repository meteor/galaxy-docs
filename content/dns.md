---
title: DNS
order: 10
description: Learn how to configure DNS to point to Galaxy
---

Before users can access your application, you must configure your DNS records to point to Galaxy. The exact process is specific to your DNS provider, however the general method is the same.

<h3 id="subdomain">Hosting on a subdomain</h3>

If your app is deployed at a subdomain such as `app.mycompany.com` or `www.mycompany.com`, simply add a CNAME record to your DNS provider pointing to `galaxy-ingress.meteor.com`. Ensure the hostname you [deployed to](deploying-to-galaxy) matches the [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) of your app (i.e `app.mycompany.com`).

<h3 id="root-domain-redirect">Redirecting the root domain</h3>

The root domain is also called the naked or apex domain. A common scenario is one where your app is hosted at `www.mycompany.com` and you would like `mycompany.com` to redirect to the same app. This is done by setting up URL redirection from `mycompany.com` to `www.mycompany.com`. The way to do this varies greatly based on your DNS provider, common methods we recommend are:

* [URL Record at DNSimple](https://support.dnsimple.com/articles/url-record/)
* [Using S3 redirects with Amazon's Route53](https://aws.amazon.com/blogs/aws/root-domain-website-hosting-for-amazon-s3/)

<h3 id="testing">Testing locally</h3>

A quick way to test that your app is working (this will only affect your local machine) is by modifying the `/etc/hosts` file to resolve your app's hostname to the Galaxy load balancer's IP address directly.

To find out which IP address to use, type `dig +short galaxy-ingress.meteor.com` and choose any of the ones shown. *Note:* The IP addresses used by Galaxy's load balancer are likely to change, in which case you'll need to do this process again.

Add a line to `/etc/hosts` (Windows: `c:\windows\system32\drivers\etc\hosts`) that contains:

```
[Galaxy's current ip address]   [Your app's hostname, e.g app.mycompany.com]
```

To ensure your changes take effect, you can reset your computer's local DNS cache with `sudo dscacheutil -flushcache` (on a mac, or see [these instructions](https://www.whatsmydns.net/flush-dns.html) for other OSes) after making your changes.

<h3 id="dns-propagation">DNS propagation</h3>

DNS is distributed and cooperative, and it takes time for the world to see your changes.  In many countries, it usually updates within about 30 minutes, but it can take up to 24 hours or even longer in some circumstances (depending on the record's TTL). You can check your ALIAS (or ANAME or CNAME) independently of your app in the terminal by typing `dig +show www.mycompany.com`. If it returns an `ANSWER SECTION` including something like the following, you are in good shape:

```
www.mycompany.com.    1800   IN    CNAME        galaxy-ingress.meteor.com.
```

<h3 id="root-domain-redirect">Hosting on a root domain (advanced)</h3>

In general, hosting your app directly on a root domain is not recommended (see [yes-www](http://www.yes-www.org/why-use-www/)). If you must do so, it's possible by using an ALIAS (also called an ANAME) record. First, you'll need to deploy your app to the root domain (e.g `myapp.com`). Next, you will need to add an ALIAS record to your DNS provider that points your root domain to `galaxy-ingress.meteor.com`. Not all DNS providers support this feature and the implementation is usually verify specific to each provider, ones we know and recommend are:

* [ALIAS Record at DNSimple](https://support.dnsimple.com/articles/alias-record/)
* [Free redirect service from wwwizer](http://wwwizer.com/naked-domain-redirect)

*Note:* If you decide to host directly on a root domain, you will likely want to forward `www` to your root domain by setting up URL redirection (see above).
