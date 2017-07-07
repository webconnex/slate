## Webhook

### List Webhooks

> The above command returns JSON structured like this:

```json
{
  "responseCode": 200,
  "data": [
		{
      "id": 28,
      "accountId": 1,
      "forms": [{
        "formId": -1,
      }],
      "token": "b4148448406443eda7bc5c44d11c9cd3",
      "events": [
        "registration",
        "subscription"
      ],
      "method": "POST",
      "url": "https://webhook-endpoint.your-url.com",
      "typeId": 1,
      "status": 1,
      "meta": {
        "name": "Registration Capture"
      },
      "dateCreated": "2015-11-10T06:09:11Z",
      "dateUpdated": "2015-11-23T19:14:16Z"
    },
    {
      "id": 29,
      "accountId": 1,
      "forms": [{
        "formId": 376,
      },{
        "formId": 19234,
      }],
      "token": "64fca5a66a8945b3958905b320f72adb",
      "events": [
        "registration",
        "coupon"
      ],
      "method": "POST",
      "url": "https://webhook-endpoint.your-url.com",
      "typeId": 1,
      "status": 1,
      "meta": {
        "name": "Internal CRM integration"
      },
      "dateCreated": "2015-11-10T16:54:20Z",
      "dateUpdated": "2015-11-23T19:14:27Z"
    }
  ],
  "totalResults": 2
}
```
#### HTTP Request
`GET /v2/public/webhooks/`

#### Request Params
No filtering implemented on this object.

#### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique ID of the webhook
**accountId**<br>*integer*					| ID of the associated account
**forms**<br>*array*<br>required					| Array of objects containing the form IDs associated with the webhook. (send [{"formID":-1}] to subscribe to all forms)
**token**<br>*string*					| Unique token for the webhook
**events**<br>*array*					| List of events assigned to the webhook
**method**<br>*integer*					| HTTP method used for the webhook delivery request
**url**<br>*string*					| Endpoint URL used for the webhook delivery request
**typeId**<br>*string*					| Webhook Type ID
**status**<br>*string*					| Status of the webhook (enabled/disabled)
**meta**<br>*object*					| Contains webhook name and app key if required by the endpoint
**dateCreated**<br>*timestamp* | Date and time of the creation of the webhook
**dateUpdated**<br>*timestamp* | Date and time the webhook was last updated

### View Webhook

> The above command returns JSON structured like this:

```json
{
  "responseCode": 200,
  "data": [
		{
      "id": 28,
      "accountId": 1,
      "forms": [{
        "formId": 19234,
      }],
      "token": "b4148448406443eda7bc5c44d11c9cd3",
      "events": [
        "registration"
      ],
      "method": "POST",
      "url": "https://webhook-endpoint.your-url.com",
      "typeId": 1,
      "status": 1,
      "meta": {
        "name": "Registration Capture"
      },
      "dateCreated": "2015-11-10T06:09:11Z",
      "dateUpdated": "2015-11-23T19:14:16Z"
    }],
  "totalResults": 1
}
```
#### HTTP Request
`GET /v2/public/webhooks/{id}`

#### Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*string*<br>required 				| ID of the requested webhook

#### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique ID of the webhook
**accountId**<br>*integer*					| ID of the associated account
**forms**<br>*array*<br>required					| Array of objects containing the form IDs associated with the webhook. (send [{"formID":-1}] to subscribe to all forms)
**token**<br>*string*					| Unique token for the webhook
**events**<br>*array*					| List of events assigned to the webhook
**method**<br>*integer*					| HTTP method used for the webhook delivery request
**url**<br>*string*					| Endpoint URL used for the webhook delivery request
**typeId**<br>*string*					| Webhook Type ID
**status**<br>*string*					| Status of the webhook (enabled/disabled)
**meta**<br>*object*					| Contains webhook name and app key if required by the endpoint
**dateCreated**<br>*timestamp* | Date and time of the creation of the webhook
**dateUpdated**<br>*timestamp* | Date and time the webhook was last updated

### Create Webhook

> The above command returns JSON structured like this:

```json
{}
```
#### HTTP Request
`POST /v2/public/webhooks`

#### Request Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**forms**<br>*array*<br>required					| Array of objects containing the form IDs associated with the webhook. (send [{"formID":-1}] to subscribe to all forms)
**events**<br>*array*<br>required					| List of events assigned to the webhook
**method**<br>*integer*					| HTTP method used for the webhook delivery request
**url**<br>*string*					| Endpoint URL used for the webhook delivery request
**typeId**<br>*string*					| Webhook Type ID (1 for user created)
**status**<br>*string*					| Status of the webhook (enabled/disabled)
**meta**<br>*object*					| Contains webhook name and app key if required by the endpoint

#### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique ID of the webhook
**accountId**<br>*integer*					| ID of the associated account
**forms**<br>*array*<br>required					| Array of objects containing the form IDs associated with the webhook. (send [{"formID":-1}] to subscribe to all forms)
**token**<br>*string*					| Unique token for the webhook
**events**<br>*array*					| List of events assigned to the webhook
**method**<br>*integer*					| HTTP method used for the webhook delivery request
**url**<br>*string*					| Endpoint URL used for the webhook delivery request
**typeId**<br>*string*					| Webhook Type ID
**status**<br>*string*					| Status of the webhook (enabled/disabled)
**meta**<br>*object*					| Contains webhook name and app key if required by the endpoint
**dateCreated**<br>*timestamp* | Date and time of the creation of the webhook
**dateUpdated**<br>*timestamp* | Date and time the webhook was last updated

### Update Webhook

> The above command returns JSON structured like this:

```json
{}
```

#### HTTP Request
`POST /v2/public/webhooks/{id}`

#### Request Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique ID of the webhook
**accountId**<br>*integer*					| ID of the associated account
**forms**<br>*array*<br>required					| Array of objects containing the form IDs associated with the webhook. (send [{"formID":-1}] to subscribe to all forms)
**events**<br>*array*<br>required					| List of events assigned to the webhook
**method**<br>*integer*					| HTTP method used for the webhook delivery request
**url**<br>*string*					| Endpoint URL used for the webhook delivery request
**typeId**<br>*string*					| Webhook Type ID (1 for user created)
**status**<br>*string*					| Status of the webhook (enabled/disabled)
**meta**<br>*object*					| Contains webhook name and app key if required by the endpoint

#### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique ID of the webhook
**accountId**<br>*integer*					| ID of the associated account
**forms**<br>*array*<br>required					| Array of objects containing the form IDs associated with the webhook. (send [{"formID":-1}] to subscribe to all forms)
**token**<br>*string*					| Unique token for the webhook
**events**<br>*array*					| List of events assigned to the webhook
**method**<br>*integer*					| HTTP method used for the webhook delivery request
**url**<br>*string*					| Endpoint URL used for the webhook delivery request
**typeId**<br>*string*					| Webhook Type ID
**status**<br>*string*					| Status of the webhook (enabled/disabled)
**meta**<br>*object*					| Contains webhook name and app key if required by the endpoint
**dateCreated**<br>*timestamp* | Date and time of the creation of the webhook
**dateUpdated**<br>*timestamp* | Date and time the webhook was last updated

### Delete Webhook

> The above command returns JSON structured like this:

```json
{}
```
#### HTTP Request
`POST /v2/public/webhooks/{id}`

#### Request Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| ID of the webhook

### List Logs for Webhook

Get all logs for a given webhook

#### HTTP Request
`POST /v2/public/webhooks/{id}/logs`

#### Request Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| ID of the webhook

### View Log by ID for Webhook

> The above command returns JSON structured like this:

```json
{}
```

View a specific webhook log

#### HTTP Request
`POST /v2/public/webhooks/{id}/logs/{logId}`

#### Request Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| ID of the webhook
**logId**<br>*integer* 				| ID of the webhook log

### Resend Webhook Request by Request ID

Request that a particular webhook attempt be resent.

#### HTTP Request
`POST /v2/public/webhooks/{id}/resend/{logId}`

#### Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*string*<br>required 				| ID of the webhook
**logId**<br>*string*<br>required 				| ID of the webhook log entry to be resent
