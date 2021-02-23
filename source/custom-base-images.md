---
title: Custom base images
order: 17
description: Learn how to customize your app's environment
---

Most Galaxy users run their app with the [default base image](/base-image-packages.html).  This provides a basic environment for running most Meteor apps.

For full control over your app's environment, you can provide a custom base image instead.  This allows you to precisely control the set of system packages available to your app, customize exactly what happens when Galaxy builds your app's image at deploy time and when Galaxy runs your app, and even allows you to run non-Meteor software on Galaxy.

A base image is a [Docker](https://www.docker.com/) image.  Base images must live on [Docker Hub](https://hub.docker.com/) and be publicly readable.  (This means they should not contain any secrets.)

You build your base image using a Dockerfile.  You should use the Dockerfile to choose an operating system for your base image (such as `ubuntu:16.04`) and install packages.  You can look at the [source of the Galaxy default base image](https://github.com/meteor/galaxy-images) for inspiration.  The Dockerfile should also add a file called `/app/setup.sh` and specify a command to run with the `CMD` or `ENTRYPOINT` directives.  For more details, see the [Docker documentation](https://docs.docker.com/).

Once you've built your base image and pushed it to Docker Hub, specify it in your settings.json file under `baseImage` inside `galaxy.meteor.com` (next to `env`).  You need to specify both the Docker repository (which generally includes your username) and the tag you want to use.  For example, your settings file may look like:

```
{
  "galaxy.meteor.com": {
    "env": { "MONGO_URL": "mongodb://..." },
    "baseImage": {
      "repository": "username/my-galaxy-base-image",
      "tag": "v23"
    }
  }
}
```

Docker allows you to push a new image to an existing tag. Currently, if you do this, Galaxy will not rebuild your app until you perform another `meteor deploy`.  We may change this policy in the future.  We recommend that you use a new tag each time your change your base image, and specify that tag rather than a mutable tag like `latest` in your `baseImage` specification.

<h2 id="build">Build time behavior</h2>

When you run `meteor deploy`, your local `meteor` command-line tool builds your app, bundles it into a [tarball](https://en.wikipedia.org/wiki/Tar_(computing%29), and uploads it to Galaxy.

Galaxy then builds a Docker image for your app based on the default base image by running the `/app/setup.sh` script inside the image using `/bin/bash`. Every custom base image must contain `/bin/bash` and `/app/setup.sh`.  (We may relax this requirement in the future to allow `/app/setup.sh` to work with any shell, so you must make sure that `/app/setup.sh` has the executable bit set and that it has a proper [shebang line](https://en.wikipedia.org/wiki/Shebang_(Unix%29).)

Galaxy provides a single argument to your setup script: an URL to your app's tarball.  Note that this URL is not guaranteed to work forever: your setup script should download the tarball during the build phase rather than storing the URL for the run phase.  We suggest you download and expand the tarball with a command like

```
cd /app && curl -sS "$1" | tar xz -m
```

(The `-m` flag ignores timestamps from the computer used to run `meteor deploy`; if that computer has clock skew, some build systems can get confused, so it's safer to just set timestamps inside the image builder.)

The script should do whatever other build-time behavior is required, such as invoking `npm install` or other build systems.


<h2 id="run">Run time behavior</h2>

To run your app, Galaxy invokes whatever command is specified in your Dockerfile via the [`CMD` or `ENTRYPOINT` directive](https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact).  It does not provide any additional arguments to the command.  Galaxy sets the environment variables documented under [container environment](/container-environment.html).

Your command is expected to run a server that listens on the port specified by the `$PORT` environment variable.  Even if you are using Galaxy to run code that isn't a traditional web server (for example, some sort of helper process for your main app), Galaxy expects to see a functioning web server in order to consider your app to be healthy.  If you choose to deploy software on Galaxy which does not have a web server, you should disable unhealthy container replacement on your app's settings page.  However, we recommend you expose a web server so that you can tell if your container is healthy or not.

Your container continues to run until its specified command completes or Galaxy stops it.


<h2 id="build">Puppeteer [(meteor/galaxy-puppeteer)](https://github.com/meteor/galaxy-images/tree/master/galaxy-puppeteer) </h2>

This image bundles every library puppeteer needs to be able to run. You can use it by doing the follow on your settings.json:

```json
{
  "galaxy.meteor.com": {
    "env": { "MONGO_URL": "mongodb://..." },
    "baseImage": {
      "repository": "meteor/galaxy-puppeteer",
      "tag": "latest"
    }
  }
}
```
It's also expected that your usage of puppeteer uses the following flags:

```js
const browser = await puppeteer.launch({
    args: [
    '--no-sandbox',
    '--disable-setuid-sandbox',
    '--disable-dev-shm-usage'
    ]
});
const page = await browser.newPage();
await page.goto("https://www.google.com");
```
