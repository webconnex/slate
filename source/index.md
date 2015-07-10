---
title: Divvy Webhook Reference

language_tabs:
  - json
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Divvy Introduction

Divvy 2 is a system for registering webhooks to use for external integration with the Webconnex eco-system that allows for people to post form data to an endpoint of their choosing.

System needs to handle high volume registrations which will require the use of queues
and a scheduler.

Needs to track the following things:
- connection errors:  should log failed attempts to post, should retry
- time of submission:
- end point of submission:
- account:
- payload submitted:

# Authentication

For the initial build we will just allow the API server to connect to the webhook server.
If we need to pass data we can proxy it through the api server for now.

# Workflow

## Registration
Consists of accountID, URL, secret, method, events, payload type, unique hash
to possibly be used as a api key.

Inital limit of 5 webhooks for each account.

## Processing

API decides if an event was triggered and if there is a registered webhook for that event

If a match was found the API sends the data to the webhook queue

The webhook working takes the items off the queue that contain the following data:
- Destination URL
- Method (optional, default=POST)
- API Key (optional)
- Payload (defined as all data, or event message)
- AccountID
- Campaign Name
- Campaign URL

The webhook submits a structured JSON payload to the URL that contains the following:

### Headers
-X-Webconnex-Event
-X-Webconnex-Delivery: (some UUID)
-X-Webconnex-Signature: HMAC hex digest of the payload, using hooks secret as the key (if configured).
-User-Agent: Webconnex-Divvy

### JSON:
- WebhookId
- URLs (test, ping, pull)?
- last response
- Data (Possibly have an object for each event, transaction, registration, etc.)
  - Campaign Name
  - Campaign URL
  - Timestamp
  - Event Payload data

### Log the response from the Webhook URL:
	- Code: (200, 400, 500, etc.)
  - Status (optional):
  - Message (optional):
 	- Full headers
 	- Full Response body
 	- Full payload
 	- Full config for the response
 	- Webhook ID
 	- Webhook Delivery ID (primary key)
 	- Signature
 	- Event


### UI:
The UI should allow for the following functionality.
Allow for account admins to set-up up 5 web hooks
Allow users to view a log of requests made to the webhook
Allow for a user to resend a particular Webhook response


# Architecture
Use Go as the language
Utilize Redis for the Queue
MySQL/MariaDB for data persistence
Maybe ES for the querying of data

## Event Registration
What is the most efficient way to figure out if an event as been triggered?

### Option 1
Use logging to monitor for events. Watching the log files we could set up cues to an event being
fired and append the data of the event. Divvy could check to see if the event matches a
registered webhook and perform work on that. This option has the added benefit of each data payload
would "backed up" in a log file.

### Option2
Have the API send events and payloads directly to Divvy and Divvy would decide whether or not to
perform work on it.

# Trigger Events

These are the system events that are available as webhook triggers

## Registration

```json
{ "registrationID": 1}
```

## Transaction

```json
{ "registrationID": 1}
```

## Registrant Modification

```json
{ "registrationID": 1}
```

## Transfers

```json
{ "registrationID": 1}
```

## Subscription

```json
{ "registrationID": 1}
```

## Decline

```json
{ "registrationID": 1}
```

## Settlement

```json
{ "registrationID": 1}
```

## Ping

Used for testing.

```json
{ "registrationID": 1}
```

# EndPoints

## Create

`/create POST`

```json
{

}
```


## View

`/view/:hook_id GET`

```json
{

}
```


## History

`/history/:hook_id GET`

```json
{

}
```


## Resend

`/resend/:hook_id/delivery/:history_id POST`

```json
{

}
```


## Delivery Status

`/resend/:hook_id/delivery/:history_id GET`

```json
{

}
```

```shell
curl "http://example.com/divvy/resend/:hook_id/delivery/:history_id"
  -H "Authorization: sessionID"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name" : "something here"
  },
  {
    "id": 2,
    "name": "something here"
  }
]
```

### HTTP Request

`GET http://example.com/api/divvy/`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
sort | "asc" | Will sort by either time processed ascending or descending
errors | true | Will show only failed requests

<aside class="success">
Remember — This is a success message.
</aside>


```shell
curl "http://example.com/api/divvy"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "something to go here"
}
```


<aside class="warning">If you're not using an administrator API key, note that some errors 403 Forbidden if they are hidden for admins only.</aside>
