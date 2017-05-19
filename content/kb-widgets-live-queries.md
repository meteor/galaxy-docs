---
title: Widgets for Live Queries
order: 63
---

## Fetched Documents

<img src="/images/apm-fetched-documents.png" style="width: 500px"/>

This is the number of documents fetched from MongoDB via [observers](apm-glossary). Meteor fetches documents from MongoDB in a few different cases. Here are some of them:

- When a new observer is created (for the initial dataset)
- Every 10 seconds, if this observer is not using the oplog
- When the observer’s internal buffer becomes empty (with oplog observers only)

## Observer Changes

<img src="/images/apm-observer-changes.png" style="width: 500px"/>

Once an observer is created, it’ll trigger events in a few different scenarios. Here a list of those event types:

- Added (Initially) - When an observer is created for the first time, it’ll fetch the initial set of documents from MongoDB and trigger this event for each document.
- Added - If a new document satisfies the query, then the observer will trigger this event with that document.
- Updated - If there is a change to an already added document, then the observer will trigger this event with the changes.
- Removed - If an existing document does not satisfy the query, then the observer will trigger this event with that document’s ID.

## Total/Reused Observer Handlers

<img src="/images/apm-total-reused-observer-handles.png" style="width: 500px"/>

When a new Live Query is created, it’ll create a new observer that watches the DB for changes. If there is an observer already created for the query, Live Query won’t create a new observer. Instead, it’ll reuse an existing observer.

There is always a handler that sits between the Live Query and the observer.

- Total Observer Handlers refer to the total number of handlers.
- Reused Observer Handlers refer to handler sites between the Live Query and an already created observer.

If the reused count is close to total count, that means Live Queries have created a fewer number of actual observers, which is the ideal case.

## Oplog Notifications

<img src="/images/apm-oplog-notifications.png" style="width: 500px"/>

Meteor watches the MongoDB oplog to observe changes happening in the MongoDB. If something happens in the DB, Meteor will receive it as a notification. The notification is attached to a collection. Then, Meteor will forward this notification to most of the observers created for that collection.

There are few different types of oplog notifications. They are:

- Inserted - When a new document is added to the collection
- Updated - When a document is updated in the collection
- Removed - When a document is removed from the collection

Meteor will receive all these notification regardless of whether it has a related observer or not.

## Live Query Publication Breakdown

<img src="/images/apm-livequery-publication.png" style="width: 500px"/>

This is a breakdown of publications sorted by the different metrics related to Live Queries. They include:

- Fetched Documents
- Observer Reuse: Descending
- Observer Reuse: Ascending
- Observer Changes: Total
- Observer Changes: Live Updates
- Observer Changes: Added (Initially)
- Observer Changes: Added
- Observer Changes: Changed
- Observer Changes: Removed
- Oplog Notifications: Low

## Live Queries summary

<img src="/images/apm-livequeries-summary.png" style="width: 500px"/>

This is a set of important metrics of your app's Live Queries. It includes following metrics:

- Fetched Documents
- Live Updates
- Observer Reuse Ratio
- Observe Lifetime
