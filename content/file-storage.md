---
title: File storage
order: 11
description: File storage for application containers 
---
Galaxy provides temporary file storage for application containers to use. Galaxy does not provide persistant file storage for application containers to use.

If you need persistant file storage for your application, you should use a robust cloud storage solution like Amazon S3.

With each container, you should be able to use up to 512 MB of disk space for temporary local file storage.

Application containers have read/write access to /tmp directory and sub-directories. If there is application code or packages that try to writ to `/root` or to the $HOME directories, these will fail, as those directories do not allow read/write access. 
