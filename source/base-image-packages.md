---
title: Default base image
order: 16
description: Learn about the default Galaxy base image
---

Most Galaxy users run their app with the default base image.  (For full control over the system libraries available to your app and its precise runtime environment, you can create a [custom base image](/custom-base-images.html) instead.)

A base image is a [Docker](https://www.docker.com/) image.  The default base image is stored in the repository [`meteor/galaxy-app`](https://hub.docker.com/r/meteor/galaxy-app/) on Docker Hub and is itself based on the repository [`meteor/ubuntu`](https://hub.docker.com/r/meteor/ubuntu/).  The source for these packages can be found in the [`galaxy-images` GitHub repository](https://github.com/meteor/galaxy-images).

<h2 id="update">Base image Updates</h2>

<h3 id="v2.0">Ubuntu Upgrade</h3>

Galaxy base Docker image is going to be upgraded by default in all new deploys starting on April 30th, 2021.

It includes a <b>major update to `Ubuntu 20.04 Focal`</b>, with a lot of security patches and improvements on stability and performance. 

If you can't update your app, check out the next section for a how to, but we recommend that you plan to do it soon!

#### Breaking Changes

If you don't use the libraries below in your code you don't need to worry about these breaking changes.

- `wkhtmltox` was upgraded to `v0.12.6-1`
  

- `PhantomJS` and `poppler` were both removed from the base image. If you depend on it, you have two options:
    1. Use the previous fixed base image (`20180509T213223Z_b6ad5bc`) by changing your settings.json with this:
        ```json
        "galaxy.meteor.com": {
            "baseImage": {
                "repository": "meteor/galaxy-app",
                    "tag":"20180509T213223Z_b6ad5bc"
            }
        }
        ```
        Be careful, as you are opting out from new updates!
    2. Create a new custom image including the dependencies you need. For more info, read the docs [here](./custom-base-images.html).

#### Migration Steps

- We recommend that you test first your app with the new base image in your staging environment on Galaxy first! Just change your settings.json to include the `baseImage` (`20210423T151822Z_93d0399`):
    ```json
    "galaxy.meteor.com": {
        "baseImage": {
            "repository": "meteor/galaxy-app",
                "tag":"20210423T151822Z_93d0399"
        }
    }
    ```
    After deploying, you will be using the same image we are going to use as default starting on 30/April/21.

- Don't change your baseImage property using Galaxy Edit Settings UI, it's not going to have any effect. It needs to be a new full deploy to force a new image creation.

- If you don't deploy a new version of your app you will continue to use the previous base image.

- After testing in a staging environment you have two options to apply this change to your production environment:
  1. Keep this setting in your app and you are ready to go, this base image will be always used.
  2. Starting from April 30th, 2021 you can remove this part of your settings as this base image is going to be the default.
    
<h2 id="packages">Installed packages</h2>

The current Galaxy default base image runs Ubuntu 20.04 LTS and comes with a set of packages pre-installed. Please note that in theory the package versions are not frozen and may be updated at any time. However, in practice, we know that many of our users may implicitly rely on the (increasingly outdated) versions of packages in the default base image. As of now, we plan to continue our implicit policy of never upgrading the Ubuntu packages on the default base image. Users who want newer versions of these packages should create a [custom base image](/custom-base-images.html) instead.

Packages useful as part of the build process:
- [build-essential](http://packages.ubuntu.com/trusty/build-essential)
- [curl](http://packages.ubuntu.com/trusty/amd64/curl)
- [wget](http://packages.ubuntu.com/trusty/wget)
- [rsync](http://packages.ubuntu.com/trusty/rsync)
- [git](http://packages.ubuntu.com/trusty/git)
- [xz-utils](http://packages.ubuntu.com/trusty/xz-utils)
- [ca-certificates](http://packages.ubuntu.com/trusty/ca-certificates)

Packages useful for popular npm packages (primarily image rendering):
- [imagemagick](http://packages.ubuntu.com/trusty/imagemagick)
- [graphicsmagick](http://packages.ubuntu.com/trusty/graphicsmagick-dbg)
- [libcairo2-dev](http://packages.ubuntu.com/trusty/libcairo2-dev)
- [poppler-utils](http://packages.ubuntu.com/trusty/poppler-utils)
- [libjpeg-dev](http://packages.ubuntu.com/trusty/libjpeg-dev)
- [wkhtmltopdf](http://packages.ubuntu.com/trusty/wkhtmltopdf) (for HTML to PDF conversion including prerequisites)
- [libssl-dev](http://packages.ubuntu.com/trusty/libssl-dev)
- [xfonts-base](http://packages.ubuntu.com/trusty/xfonts-base)
- [xfonts-75dpi](http://packages.ubuntu.com/trusty/xfonts-75dpi)

In addition, the default base image contains several popular versions of Node preinstalled in directories with names like `/node-v12.22.0-linux-x64`. (Including these versions makes the container build and start process more efficient.)  Galaxy uses the official binary distribution of Node from nodejs.org, not the Ubuntu package.

<h2 id="build">Build time behavior</h2>

When you run `meteor deploy`, your local `meteor` command-line tool builds your app, bundles it into a [tarball](https://en.wikipedia.org/wiki/Tar_(computing%29), and uploads it to Galaxy.  Galaxy then builds a Docker image for your app based on the default base image by running the `/app/setup.sh` script inside the image.  This section describes exactly what the default base image's `/app/setup.sh` script does.

First, it extracts your uploaded tarball into the `/app` directory.  The tarball's contents are all nested under a directory called `bundle`, so this puts your built app into the `/app/bundle` directory.

Next, it figures out which version of Node your app was built with.  If that version isn't already part of the image, it downloads and installs it.  In either case, it sets the `$PATH` environment variable to ensure that the correct version of Node is used for the rest of the build process.

Next, it figures out which version of npm your app was built with, and installs that version of npm.

Next, it runs `npm install --unsafe-perm` inside `/app/bundle/programs/server`.  When building your app, the `meteor` tool includes the contents of most npm packages in the tarball, but if those packages contain binary code, they may need to be rebuilt for the 64-bit Linux server environment, which is what this command does.

Finally, if the scripts `/app/bundle/programs/server/setup.sh` or `/app/bundle/setup.sh` exist, they are executed. (Current versions of Meteor do not make it easy to include these files in your bundle.)

After running all these commands, the Galaxy image builder saves the state of the image to an internal Docker registry.

<h2 id="run">Run time behavior</h2>

When Galaxy runs an app image based on the default base image, it executes a script called `/app/run.sh`.

This script adds the proper version of Node to `$PATH`, just like at [build time](#build).  It also makes the version of Node available in `$NODE_VERSION`.

If the script `/app/bundle/run.sh` exists, then this script is executed with `bash`.  (Current versions of Meteor do not make it easy to include this file in your bundle.)

Otherwise, the script runs `node $GALAXY_NODE_OPTIONS main.js` inside the `/app/bundle` directory. You can set `$GALAXY_NODE_OPTIONS` to a flag or space-separated series of flags [in your settings.json file](/environment-variables.html) if you need fine-grained control over how Node runs your server, such as setting [garbage collection flags](/scaling.html#garbage-collection).
