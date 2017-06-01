---
title: Container environment
order: 14
description: Learn in what environment Galaxy runs your app
---

<!-- Note: post logger2 release, we'll also document the environment variables
     that we set, entry point, etc.
-->

Galaxy runs your app in a set of containers using the [Docker](https://www.docker.com/) container platform.

<h2 id="network">Network environment</h2>

<h3 id="network-incoming">Incoming connections</h3>

Galaxy runs your app containers in a firewalled network environment.  Only one port is exposed for external connections.  Galaxy tells your app what port to listen on via the `$PORT` environment variable, which contains a number such as `3000`.

Galaxy forwards HTTP connections (port 80) on your app's configured [domains](/custom-domains.html) to the port exposed for external connections. HTTPS connections (port 443) are also forwarded to this port if you've [configured encryption](/encryption.html).  You cannot serve connections on any other ports.

<h3 id="network-outgoing">Outgoing connections and IP whitelisting</h3>

When your app connects to other services like your database, those services' connections will always appear to come from one of a fixed set of IP addresses.  These IP addresses are not the IP addresses of the individual machines your container runs on, so don't be surprised if they don't match.  (These addresses are distinct from the addresses that our "ingress" DNS address points to --- don't point your DNS there!)

Some services can be configured to only allow access from a list of IP addresses. For an extra layer of security, Galaxy Professional customers can use these IP addresses in a "whitelist" on that service. Whitelisting is especially common for databases, and may be required by your database provider.

Note that whitelisted IP addresses are shared between all Galaxy Professional customers. While whitelisting is meant to protect your app from non-targeted attacks, you should still control access to your services by other means. 

To find the IP addresses you should be using, go to your app's Settings page and copy down the IP addresses shown there (you may need to enable Galaxy Professional service at this point).

If your software wants you to specify your whitelist as a list of [CIDRs](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) rather than a list of IP addresses, just add the three characters `/32` to the end of each IP address.

If whitelisting should be available on your plan but cannot be found, email <a href="mailto:support@meteor.com"> support@meteor.com</a> for assistance.
