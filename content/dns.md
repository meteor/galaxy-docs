---
title: DNS
order: 10
description: Learn how to configure DNS to point to Galaxy
---

Before users can access your application, you must configure your DNS records to point to Galaxy. While the process will be specific to your DNS provider, the general method is the same.

<h2 id="subdomain">Hosting on a subdomain</h2>

If your app is deployed at a subdomain such as `www.mycompany.com` or `app.mycompany.com`, simply add a CNAME record to your DNS provider pointing to:

- `us-east-1.galaxy-ingress.meteor.com` for applications in the us-east-1 region. 

- `eu-west-1.galaxy-ingress.meteor.com` for applications in the eu-west-1 region.  

Ensure the hostname you [deployed to](deploying-to-galaxy) matches the [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) of your app (i.e `app.mycompany.com`).

<h2 id="root-domain-redirect">Redirecting the root domain</h2>

The root domain is also called the naked or apex domain. A common scenario is when your app is hosted at `www.mycompany.com` and you'd like `mycompany.com` to redirect to the same app. This is done by setting up URL redirection from `mycompany.com` to `www.mycompany.com`. While the way to do this varies by DNS provider, these are common methods we recommend:

* [URL Record at DNSimple](https://support.dnsimple.com/articles/url-record/)
* [Free redirect service from wwwizer](http://wwwizer.com/naked-domain-redirect)

<h2 id="hosting-root-domain">Hosting on a root domain (advanced)</h2>

In general, hosting your app directly on a root domain is not recommended (see [yes-www](http://www.yes-www.org/why-use-www/)). If you must do so, it's possible by using an ALIAS (also called an ANAME record).

First, you'll need to either deploy your app to the root domain (e.g `myapp.com`) or add the root domain as an [additional domain for your app](custom-domains.html#add-domain). Next, you will need to add an ALIAS record to your DNS provider that points your root domain to `galaxy-ingress.meteor.com`. 

Not all DNS providers support this feature and the implementation is usually very specific to each provider. Providers we know and recommend are:

* [ALIAS Record at DNSimple](https://support.dnsimple.com/articles/alias-record/)

*Note:* If you decide to host directly on a root domain, you will likely want to forward `www` to your root domain by setting up URL redirection (see above).

<h2 id="root-domain-redirect-https">Setting up the root domain when HTTPS is enabled</h2>

There are two options for configuring a redirect of https://example.com to https://www.example.com. The first option is usually easier to implement.

**Option 1**

- Step 1) Point the root domain (example.com) DNS to Galaxy. You can do this with an [ALIAS record](http://galaxy-guide.meteor.com/dns.html#hosting-root-domain).

- Step 2) Add example.com as an additional domain to the app on the Settings page.
For www.example.com, that would be: [https://galaxy.meteor.com/app/www.example.com/settings](https://galaxy.meteor.com/app/www.example.com/settings) (not a real app).

- Step 3) Enable Force HTTPS for the app on the Settings page.

**Option 2**

Use a redirection service to redirect example.com to www.example.com. The redirection service needs to support both root domains as well as SSL. A good example is [Amazon’s S3 redirection](http://docs.aws.amazon.com/AmazonS3/latest/dev/how-to-page-redirect.html), which supports both.

<h2 id="dns-propagation">DNS propagation</h2>

DNS is distributed and cooperative, and it takes time for the world to see your changes.  In many countries, it usually updates within about 30 minutes, but it can take up to 24 hours or even longer in some circumstances (depending on the record's TTL). You can check your ALIAS (or ANAME or CNAME) independently of your app in the terminal by typing `dig +show www.mycompany.com`. If your `ANSWER SECTION` includes a record like this, you are in good shape:

```
www.mycompany.com.    1800   IN    CNAME        galaxy-ingress.meteor.com.
```

<h2 id="testing">Testing locally</h2>

A quick way to test that your app is working is by modifying the `/etc/hosts` file to resolve your app's hostname to the Galaxy load balancer's IP address directly. Note that this will only affect your local machine.

To find out which IP address to use, type `dig +short galaxy-ingress.meteor.com` and choose any of the ones shown. The IP addresses used by Galaxy's load balancer are likely to change, so you may need to do this process more than once.

Add a line to `/etc/hosts` (Windows: `c:\windows\system32\drivers\etc\hosts`) that contains:

```
[Galaxy's current ip address]   [Your app's hostname, e.g app.mycompany.com]
```

To ensure your changes take effect, you can reset your computer's local DNS cache with `sudo dscacheutil -flushcache` (Mac; see [other OSes](https://www.whatsmydns.net/flush-dns.html)) after making your changes.

