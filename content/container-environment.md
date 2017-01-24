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

Galaxy runs your app containers in a firewalled network environment.  Only one port is exposed for external connections.  Galaxy tells your app what port to listen on via the `$PORT` environment variable, which contains a number such as `3000`.

Galaxy forwards HTTP connections (port 80) on your app's configured [domains](/custom-domains.html) to this port, as well as HTTPS connections (port 443) if you've [configured encryption](/encryption.html).  You cannot serve connections on any other ports.

When your app connects to other services like your database, its connections will always appear to come from one of a fixed set of IP addresses.  (These IP addresses are not the IPs of the individual machines your container runs on, so don't be surprised if they don't match.  These addresses are also distinct from the addresses that our "ingress" DNS address points to --- don't point your DNS at these IP addresses!)

Some services can be configured to only allow access from a list of IP addresses, so for an extra layer of security you can use these IPs in a "whitelist" on that service.  Note that these IP addresses are shared between all Galaxy customers, so you should still control access to your services by other means; whitelisting is just a defense-in-depth approach that can protect your app from non-targeted attacks.

Here are the IP addresses to add to your whitelist:

- For the us-east-1 cluster: 34.197.187.203, 34.197.229.75, 34.197.156.92, 34.197.222.74
- For the eu-west-1 cluster: 34.248.186.245, 34.248.14.239, 34.248.124.59
