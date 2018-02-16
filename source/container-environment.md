---
title: Container environment
order: 14
description: Learn in what environment Galaxy runs your app
---

<!-- Note: post logger2 release, we'll also document the environment variables
     that we set, entry point, etc.
-->

Galaxy runs your app in a set of containers using the [Docker](https://www.docker.com/) container platform.

The actual code that is run is determined by the "base image" --- either the [default base image](/base-image-packages.html) or a [custom base image](/custom-base-images.html).

Galaxy runs your app on 64-bit Linux machines in the UTC time zone.

<h2 id="stopping-containers">How containers stop</h2>

When Galaxy wants to shut down your container (because you have deployed a new version, because you are scaling down, because Galaxy is replacing the underlying machine, or other reasons), it first sends the `SIGTERM` signal to your container, waits a grace period of 30 seconds, and then sends the `SIGKILL` signal.  If you'd like to do some cleanup work before your container dies, you can catch the `SIGTERM` signal (eg, with [`process.on('SIGTERM')`](https://nodejs.org/api/process.html#process_signal_events) in Node).  The `SIGKILL` signal cannot be caught; containers receiving this signal immediately die.  You can adjust the grace period on your app's settings page. Galaxy informs your app of how long the grace period will be via the `METEOR_SIGTERM_GRACE_PERIOD_SECONDS` environment variable.  If your app has many users, one thing you may wish to do during this grace period is close incoming connections gradually.  You can use our [`@meteorjs/ddp-graceful-shutdown`](https://www.npmjs.com/package/@meteorjs/ddp-graceful-shutdown) npm package (as described in [this blog post](https://blog.meteor.com/new-in-galaxy-gradual-client-transitions-during-deploys-fa78f4505df6)) to do this easily.

<h2 id="env-vars">Environment variables</h2>

Galaxy runs your app with the following environment variables set:

| Environment variable | Default value | meaning |
| -------------------- | ------------- | ------- |
| `APM_*` | Various | Galaxy Pro apps with Meteor APM enabled have several environment variables starting with `APM_` to configure their APM agent. |
| `GALAXY_APP_ID` | App identifier like `Ss8o4Y6KrvFBKKkqM` | Internal identifier for your app. |
| `GALAXY_APP_VERSION_ID` | Integer like `123` | The container's app version. |
| `GALAXY_CONTAINER_ID` | Container ID including app ID, like `Ss8o4Y6KrvFBKKkqM-3n28` | Internal identifier for this container. |
| `GALAXY_LOGGER` | `system` | For historical reasons, indicates to your container that log collection is handled by Galaxy. |
| `HTTP_FORWARDED_COUNT` | `1` | Tells your app that it is running behind a proxy. |
| `KADIRA_OPTIONS_HOSTNAME` | Short container ID, like `3n28` | For historical reasons, used to configure the third-party Kadira service on which Meteor APM is based. |
| `METEOR_SETTINGS` | A JSON object, set [when you deploy your app](/deploy-guide.html#settings-create) | Available as [`Meteor.settings`](https://docs.meteor.com/api/core.html#Meteor-settings). Galaxy may add fields to your settings object to enable features such as [prerender](/seo.html), and may reformat the JSON object. |
| `METEOR_SIGTERM_GRACE_PERIOD_SECONDS` | `30` | The length of the [container termination grace period](#stopping-containers). |
| `PORT` | Integer like `3000` | [Port on which your app should listen](#network-incoming). |
| `ROOT_URL` | Your app's default hostname, prefixed with `http://` or `https://` depending on whether you use Force HTTPS | Used by [`Meteor.absoluteUrl()`](https://docs.meteor.com/api/core.html#Meteor-absoluteUrl) to generate links. |

You can add your own environment variables and override any of these except for the container-specific ones (`GALAXY_CONTAINER_ID` and `KADIRA_OPTIONS_HOSTNAME`) and `GALAXY_LOGGER` [via your settings.json file](/environment-variables.html).

<h2 id="network">Network environment</h2>

<h3 id="network-incoming">Incoming connections</h3>

Galaxy runs your app containers in a firewalled network environment.  Only one port is exposed for external connections.  Galaxy tells your app what port to listen on via the `$PORT` environment variable, which contains a number such as `3000`.

Galaxy forwards HTTP connections (port 80) on your app's configured [domains](/custom-domains.html) to the port exposed for external connections. HTTPS connections (port 443) are also forwarded to this port if you've [configured encryption](/encryption.html).  You cannot serve connections on any other ports.

<h3 id="network-outgoing">Outgoing connections and IP whitelisting</h3>

When your app connects to other services like your database, those services' connections will always appear to come from one of a fixed set of IP addresses.  These IP addresses are not the IP addresses of the individual machines your container runs on, so don't be surprised if they don't match.  (These addresses are distinct from the addresses that our "ingress" DNS address points to --- don't point your DNS there!)

Some services can be configured to only allow access from a list of IP addresses. Galaxy Professional customers can use these IP addresses in a "whitelist" on that service, for an extra layer of security. 

Whitelisting is especially common for databases and may be required by your database provider.

Note that whitelisted IP addresses are shared between all Galaxy Professional customers. While whitelisting is meant to protect your app from non-targeted attacks, you should still control access to your services by other means. 

To find the IP addresses you should be using, go to your app's Settings page and copy down the IP addresses shown there. If you haven't upgraded to Galaxy Professional containers yet, you'll need to at this point.

If your software wants you to specify your whitelist as a list of [CIDRs](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) rather than a list of IP addresses, just add the three characters `/32` to the end of each IP address.

<h2 id="load-balancing">Health checking and load balancing</h2>

Galaxy expects that your container will provide an HTTP server listening on the port given in the `$PORT` environment variable. Galaxy expects that the HTTP server will respond to a `GET /` request with a well-formed HTTP response within 5 seconds. The health check sets a `User-Agent` header containing the string `Galaxybot/`. (Galaxy currently only validates that the response is a well-formed HTTP response, but it is a good idea to ensure that this response does not have a 5xx status code, as we may refine our definition of "healthy" in the future.)  If your container does not have a functional HTTP server listening on the given port, Galaxy will consider that container to be "unhealthy".

New client connections are routed to "least loaded" healthy containers. "Least loaded" is defined as the container with the fewest existing client connections.

If a container grows its memory or CPU usage, the existing client connections won't be re-routed, unless that container is marked as unhealthy. That is to say: Galaxy currently does not actively rebalance existing clients between healthy containers. If a container crashes or is marked unhealthy, its users will be routed to a healthy container.

If a new container stays unhealthy for 10 minutes, or a container that was once healthy becomes unhealthy and stays in that state for 5 minutes, Galaxy will replace it with a new container. Additionally, Galaxy will wait at least 10 minutes (longer for apps with many containers) for all containers of a newly deployed app version to become healthy before declaring the deploy a success, and will return to the previous active version on failure. You may disable all of the behaviors in this paragraph under "Unhealthy container replacement" on your app's settings page.
