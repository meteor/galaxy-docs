---
title: Enabling SSL encryption
order: 9
description: Learn how to enable SSL encryption to secure sensitive data
---

Todo:
Let's encrypt
Custom cert



It is highly recommended that you use SSL both for security reasons and to avoid issues with websockets connecting from behind certain firewalls. You should add the `force-ssl` package to your application to ensure connections over http are redirected to https.

Private keys and certificates should be in the PEM format (this is the same format used by nginx). If intermediate certificates are used in addition to the primary certificate, they should be placed in the same file as the primary certificate. The primary certificate should come first, followed by the intermediate certificates.


### Adding your certificate and private key

1. Navigate to the settings tab for your app.
2. Click 'add certificate'.
3. Choose the file containing your private key and the file containing your certificate(s).
4. Click 'enable ssl'.
