---
title: API
order: 35
description: Learn how to use Galaxy's public API
---

Galaxy's public API is a GraphQL endpoint that enables you to monitor your apps running on Galaxy and change their configurations.

<h2 id="endpoint">Configuration</h2>

Each Galaxy region has a different URL and so each region also has a different endpoint.

They are the same as the dashboard URL appending `/graphql` in the end.

- US East: `https://galaxy.meteor.com/graphql`.

- EU West: `https://eu-west-1.galaxy.meteor.com/graphql`.

- Asia-Pacific: `https://ap-southeast-2.galaxy.meteor.com/graphql`.  

To authorize your requests you need to provide a header in your HTTP post requests to these endpoints. Each Galaxy region is independent and so you will have a different API Key for each region.

Each account (organization or individual) can have one API Key to access the API.

You can generate your key in the Settings tab of your account on Galaxy dashboard.

> You need to have at least one professional app running on Galaxy to be able to access our public API

Once you generate your API Key you use our API providing this key in the header `galaxy-api-key`. See one example using cURL and Galaxy US.

Replace `YOUR_API_KEY` with your key and `YOUR_USERNAME` with your username.

```shell script
curl \
    -X POST \
    -H "Content-Type: application/json" \
    -H "galaxy-api-key: YOUR_API_KEY" \
    --data '{ "query": "{ user(username:\"YOUR_USERNAME\"){ _id username runningAppCount }}" }' \
    https://galaxy.meteor.com/graphql
```
