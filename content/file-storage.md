---
title: File storage
order: 44
description: File storage for application containers 
---
Galaxy provides temporary file storage for application containers to use. Galaxy does not provide persistent file storage for application containers to use.

If you need persistent file storage for your application, you should use a robust cloud storage solution like Amazon S3.

With each container, you should be able to use up to 512 MB of disk space for temporary local file storage.

Application containers are given read/write access to the /tmp directory and /tmp sub-directories. Application containers do not have read/write access to the `/root` directory or to the `$HOME` directory.

In your application, when deploying to Galaxy, ensure that no package or application code tries to write to the `/root` directory on the local filesystem.

