---
title: API
order: 35
description: Learn how to use Galaxy's public API
---

Galaxy's public API is a GraphQL endpoint that enables you to monitor your apps running on Galaxy and change their configurations.

<h2 id="endpoint">Access</h2>

Each Galaxy region has a different URL and so each region also has a different endpoint.

- US East: `https://us-east-1.api.meteor.com/`.

- EU West: `https://eu-west-1.api.meteor.com/`.

- Asia-Pacific: `https://ap-southeast-2.api.meteor.com/`.  

To access the GraphQL HTTP endpoint you need to append `/graphql` to these URLs, for example, US East GraphQL endpoint is `https://us-east-1.api.meteor.com/graphql`.

You can also access the Explorer (GraphiQL) appending `/explorer`, for example, US East Explorer endpoint is `https://us-east-1.api.meteor.com/explorer`. Last but not least you can also connect Apollo DevTools if you open your browser in the API base URL.

<h2 id="endpoint">Authorization</h2>

To authorize your requests you need to provide a header in your HTTP post requests to these endpoints. Each Galaxy region is independent and so you will have a different API Key for each region.

Each account (organization or individual) can have one API Key to access the API.

You can generate your API Key from your Account Settings tab in the Galaxy Dashboard by going to `https://galaxy.meteor.com/{username}/settings` and clicking on `Generate Key`.

<img src="/images/galaxy-api-key.png" alt="Galaxy API Key" style="width: 680px"/>

> API access is only available for professional apps.

Once you generate your API Key you use our API providing this key in the header `galaxy-api-key`. See one example using cURL and Galaxy US.

Replace `YOUR_API_KEY` with your key and `YOUR_USERNAME` with your username.

```shell script
curl \
    -X POST \
    -H "Content-Type: application/json" \
    -H "galaxy-api-key: YOUR_API_KEY" \
    --data '{ "query": "{ user(username:\"YOUR_USERNAME\"){ _id username runningAppCount }}" }' \
    https://us-east-1.api.meteor.com/graphql
```

You can set your API Key in the bottom right of Explorer.

You can also provide your key as a variable called `galaxyApiKey` in your GraphQL requests, this can be useful in DevTools or if you have limitations in how to set a header in your http requests.

<h2 id="endpoint">Examples</h2>

Check this open-source version of interaction with Galaxy public API to see a few examples of usage:

[@quave/galaxy-bot](https://github.com/quavedev/galaxy-bot/)

