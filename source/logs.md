---
title: Logs
order: 32
description: How to use your logs
---

The logs should be your first stop when troubleshooting any Galaxy issue. When working with Galaxy support, an agent will usually begin by consulting your logs. If a clearly noted issue has been marked there, you can save time by reading the logs and iterating on your code until the error goes away.

You can reach the logs dashboard by clicking on your app, then clicking the "Logs" tab.

<img src="/images/galaxy-app-logs.png" style="margin: 1em 0;"/>

<h3 id="tabs">Tabs</h3>

There are several logging tabs you can click, below the "Logs" tab itself. These are:

- All: for the combined view.
- App: for application-specific messages and errors.
- Service: for messages generated during the build process, and messages saying that a container is starting or stopping.
- Errors: exclusively for errors, which are flagged in red in other tab views.

Breakdown by tab will be especially useful if you have multiple containers running, and are regularly deploying.

There is also a button where you can download all the logs that are still available (we retain logs for 7 days).

<h4 id="all">All</h4>

Every message and error will be shown here.

If your containers are working correctly and have been up for a while, this may be the most convenient tab to check. If you have multiple containers and builds succeeding and failing, this view may be too crowded.

<h4 id="app">App</h4>

Any messages or errors thrown by your app will be shown here, assuming our image builder was able to build your app and successfully launch it.

Check this to see what your app is doing during normal operations. You can always add lines to your code to print what your app is doing for added visibility.

<h4 id="service">Service</h4>

If your app isn't successfully deploying, this is the tab you'll want to check. Our image builder tries to build your app into a container; if it fails, the failure will be noted here.

One type of error (example <a href="https://github.com/meteor/meteor/issues/8136">here</a>) is that a particular version of a package wasn't able to be built by our image builder. If this happens to your app, the output will frequently include a line like this, after the package install line:

`node-pre-gyp install --fallback-to-build`

A working solution in such cases is usually to revert to an earlier version of the package. 

<h4 id="errors">Errors</h4>

Errors will be shown in this tab. Check to see if there are any outstanding errors if your app is malfunctioning.

<h3 id="storage">Storage</h3>

If any errors or messages thrown by your app are older than 1 week, they won't appear in your logs. For more permanent log storage options, contact <a href="mailto:support@meteor.com">support@meteor.com</a>.

<h3 id="custom-storage">Custom log storage</h3>

If you would like access to older logs and more flexibility in how you access your logs, you can run your own [Elasticsearch](https://www.elastic.co/products/elasticsearch) server and configure Galaxy to send your app's logs to your own server.  You can then use any tools that support Elasticsearch to search and process your logs.  Several companies provide hosted Elasticsearch systems, including [Elastic Cloud](https://www.elastic.co/cloud) and [Amazon Web Services](https://aws.amazon.com/elasticsearch-service/).

To use Galaxy's custom log storage support, set up your Elasticsearch server, and provide its URL as the `USER_LOG_DESTINATION` [environment variables](/deploy-setup.html#env-variables) in your app's `settings.json`.  Galaxy will send your app's standard output and standard error, as well as notifications of container start and exit events, to your Elasticsearch server.  Note that logs from building containers, as well as some other service logs from the Galaxy scheduler, are not at this time sent to your Elasticsearch server.

You will still be able to view your last week of logs in the Galaxy dashboard.

Logs are written to Elasticsearch indices with names that look like `app_logs-2018-01-29`. A new index is created for each day (in the UTC time zone). This lets you reclaim space on your server easily by deleting old indices.

We recommend you create an [index template](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-templates.html) to define the fields used by Galaxy's Elasticsearch integration. The index template tells Elasticsearch that the `@timestamp` field contains a date and time, and that several other fields which contain IDs such as container ID not be "analyzed": ie, they should be treated literally instead of broken into strings and lower-cased.

Elasticsearch has changed some of its APIs in recent versions, so the exact index template depends on your version of Elasticsearch.

<h4 id="index-template-es5">Setting up index templates for Elasticsearch 5 and earlier</h4>

For versions of Elasticsearch earlier than v6, run the following code at your shell (substituting in your Elasticsearch server's credentials and address) to create the index template:

```sh
curl -X PUT 'https://username:password@your-elasticsearch-server.com/_template/app_logs?pretty' -H 'Content-Type: application/json' -d '
{
  "template": "app_logs-*",
  "mappings": {
    "line": {
      "properties": {
        "@timestamp": {
          "type": "date",
          "format": "dateOptionalTime"
        },
        "appId": {
          "type": "string",
          "index": "not_analyzed"
        },
        "containerId": {
          "type": "string",
          "index": "not_analyzed"
        },
        "stack": {
          "type": "string",
          "index": "not_analyzed"
        },
        "log": {
          "type": "string"
        },
        "stream": {
          "type": "string",
          "index": "not_analyzed"
        },
        "rootUrl": {
          "type": "string",
          "index": "not_analyzed"
        },
        "appVersionId": {
          "type": "string",
          "index": "not_analyzed"
        }
      }
    }
  }
}
'
```

<h4 id="index-template-es6">Setting up index templates for Elasticsearch 6</h4>

For Elasticsearch v6, run the following code at your shell (substituting in your Elasticsearch server's credentials and address) to create the index template:

```sh
curl -X PUT 'https://username:password@your-elasticsearch-server.com/_template/app_logs?pretty' -H 'Content-Type: application/json' -d '
{
  "index_patterns": ["app_logs-*"],
  "mappings": {
    "line": {
      "properties": {
        "@timestamp": {
          "type": "date",
          "format": "dateOptionalTime"
        },
        "appId": {
          "type": "keyword",
          "index": true
        },
        "containerId": {
          "type": "keyword",
          "index": true
        },
        "stack": {
          "type": "keyword",
          "index": true
        },
        "log": {
          "type": "text",
          "index": true
        },
        "stream": {
          "type": "keyword",
          "index": true
        },
        "rootUrl": {
          "type": "keyword",
          "index": true
        },
        "appVersionId": {
          "type": "keyword",
          "index": true
        }
      }
    }
  }
}
'
```

In Elasticsearch 6, the `string` type is removed, and is replaced with `text` or `keyword` depending on whether or not you analyze it. (The new types were introduced in Elasticsearch 5, and `string` was removed in Elasticsearch 6.) Elasticsearch 6 also renames `template` to `index_patterns`.

<h4 id="index-template-es7">Setting up index templates for Elasticsearch 7 and later</h4>

For Elasticsearch v7, run the following command to create the index pattern:

```sh
curl -X PUT 'https://username:password@your-elasticsearch-server.com/_template/app_logs?pretty' -H 'Content-Type: application/json' -d '
{
  "index_patterns": ["app_logs-*"],
  "template": {
    "mappings": {
        "line": {
            "properties": {
                "@timestamp": {
                  "type": "date"
                },
                "appId": {
                  "type": "text"
                },
                "containerId": {
                  "type": "text"
                },
                "stack": {
                  "type": "text"
                },
                "log": {
                  "type": "text"
                },
                "stream": {
                  "type": "text"
                },
                "rootUrl": {
                  "type": "text"
                },
                "appVersionId": {
                  "type": "text"
                }
            }
        }
    }
  }
}
'
```

