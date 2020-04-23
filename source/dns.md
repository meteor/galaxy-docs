---
title: DNS
order: 21
description: Learn how to configure DNS to point to Galaxy
---

Before users can access your application, you must configure your DNS records to point to Galaxy. Galaxy is not a DNS provider and you’ll need to use your existing DNS provider to set DNS records. While the process will be specific to your DNS provider, the general method is the same. 

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

<h2 id="root-domain">Redirecting the root domain</h2>

The root domain is also called the naked or apex domain. A common scenario is when your app is hosted at `www.mycompany.com` and you'd like `mycompany.com` to redirect to the same app. 

Galaxy does not support A record configuration using an IP but you can redirect your root domain (mycompany.com) to your app subdomain and the result will be the same.

Here we are going to explain step-by-step how to do it using AWS S3 and AWS Route53 services but you can do it in the DNS provider of your choice.

<h3 id="aws-setup">AWS Setup</h3>

<h4 id="aws-route-53">AWS Route 53</h4>

You need to set your DNS to be controlled by AWS Route 53.

Go to your AWS Console and go to the service called [Route 53](https://console.aws.amazon.com/route53/home). If you don't have an account on AWS can create one [here](https://portal.aws.amazon.com/billing/signup).

In the Route 53 Dashboard click on `Create Hosted Zone`, fill your `Domain Name` (mycompany.com) and click on `Create`.

You are going to see a list of records, you can want to copy the value from `NS` (Name server) and paste in the service you bought your domain.

The values will be like 
```
ns-1623.awsdns-10.co.uk.
ns-492.awsdns-61.com.
ns-709.awsdns-24.net.
ns-1485.awsdns-57.org.
```
but don't copy these values from here, copy from your AWS Route 53 record.

Go to the service where you bought your domain and change your Name Server to use Route 53 pasting the name servers that you have copied from AWS Route 53. Every service that sells domains, like GoDaddy, have a different way to set the Name Server but it is usually very easy to do this, if you have any questions about this contact your domain service support.

Now that you are using AWS Route 53 as your Name Server you can point your subdomain (you must use a subdomain, app.mycompany.com or www.mycompany.com) to Galaxy following the steps [here](#subdomain). After you complete your subdomain setup return to the next step.


<h4 id="aws-s3">AWS S3</h4>

Now we are ready to start the setup to make your root domain to redirect automatically to your subdomain. Go to [S3](https://s3.console.aws.amazon.com/s3/home) Dashboard. Click on `Create bucket`, fill your bucket name with your root domain (mycompany.com), uncheck `Block all public access`, check `I acknowledge that the current settings might result in this bucket and the objects within becoming public.` and click on `Create bucket`.

Access your newly created bucket (mycompany.com) and go to `Properties` tab, click on `Static website hosting` box, check `Redirect requests` in the field `Target bucket or domain` fill your subdomain (www.mycompany.com or app.mycompany.com) and fill protocol as `https`, click on `Save`

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

<h2 id="other-options-redirect">Other options for redirecting the root domain</h2>
While the way to do this varies by DNS provider, these are common methods:

* [URL Record at DNSimple](https://support.dnsimple.com/articles/url-record/)
* [Free redirect service from wwwizer](http://wwwizer.com/naked-domain-redirect)

Because another service is hosting the redirect page, you'll need to set up SSL using their methods, which will most likely involve a certificate upload.

If you'd like to host on Galaxy on the naked domain with HTTPS, or would like to serve a redirect from Amazon S3 via Amazon CloudFront (which supports custom certs), [this guide](https://simonecarletti.com/blog/2016/08/redirect-domain-https-amazon-cloudfront/), from a member of the DNSimple team, may be helpful.

<h2 id="hosting-root-domain">Hosting on a root domain using ALIAS</h2>

In this scenario, you do want to emphasize a short URL like mycompany.com. While hosting on a root domain [can introduce complications](http://www.yes-www.org/why-use-www/), it's possible to do by using an ALIAS (also called an ANAME record).

First, you'll need to either deploy your app to the root domain (e.g `myapp.com`) or add the root domain as an [additional domain for your app](custom-domains.html#add-domain). Next, you will need to add an ALIAS record to your DNS provider that points your root domain to `galaxy-ingress.meteor.com`.

Not all DNS providers support this feature and the implementation is usually very specific to each provider. Providers we know and recommend are:

* [ALIAS Record at DNSimple](https://support.dnsimple.com/articles/alias-record/)

*Note:* If you decide to host directly on a root domain, you will likely want to forward `www` to your root domain by setting up URL redirection (see above).

[We recommend you use SSL](encryption.html) as a best practice. You can either enable LetsEncrypt using our integration or upload your own certificate.

<h2 id="other-issues">Other issues</h2>

Galaxy is not a DNS record provider. Our support is focused on configuring your settings to work with Galaxy apps, as described in the sections above.

If you have additional issues which reach beyond the scope of this article, you may need to contact your DNS record provider to resolve them. 
