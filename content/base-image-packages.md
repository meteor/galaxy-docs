---
title: Base image
order: 16
description: Learn which packages are on the Galaxy base image
---

The Galaxy base image runs Ubuntu 14.04 and comes with a set of packages pre-installed. Please note that package versions are not frozen and may be updated at any time.

- [build-essential](http://packages.ubuntu.com/trusty/build-essential)
- [wget](http://packages.ubuntu.com/trusty/wget)
- [curl](http://packages.ubuntu.com/trusty/amd64/curl)
- [rsync](http://packages.ubuntu.com/trusty/rsync)
- [phantomjs](http://packages.ubuntu.com/trusty/phantomjs)
- [ca-certificates](http://packages.ubuntu.com/trusty/ca-certificates)
- [imagemagick](http://packages.ubuntu.com/trusty/imagemagick)
- [graphicsmagick](http://packages.ubuntu.com/trusty/graphicsmagick-dbg)
- [libcairo2-dev](http://packages.ubuntu.com/trusty/libcairo2-dev)
- [poppler-utils](http://packages.ubuntu.com/trusty/poppler-utils)
- [libjpeg-dev](http://packages.ubuntu.com/trusty/libjpeg-dev)
- [wkhtmltopdf](http://packages.ubuntu.com/trusty/wkhtmltopdf) (for HTML to PDF conversion including prerequisites)
- [libssl-dev](http://packages.ubuntu.com/trusty/libssl-dev)
- [xfonts-base](http://packages.ubuntu.com/trusty/xfonts-base)
- [xfonts-75dpi](http://packages.ubuntu.com/trusty/xfonts-75dpi)
- [libpoppler-qt4-dev](http://packages.ubuntu.com/trusty/libpoppler-qt4-dev)
- [git](http://packages.ubuntu.com/trusty/git)

When Galaxy builds your deployed app into a Docker container, it installs the same version of Node used by the version of the `meteor` command-line tool that you used to deploy it.  (Currently, this uses the official binary distribution of Node from nodejs.org, not the Ubuntu package. It is installed into a non-standard directory which is prepended to the `$PATH` that your app sees.)
