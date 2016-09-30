## Webhooks Events

These are the system events that are available as webhook triggers

### Registration

> Payload

```json
{
  "eventType": "registration",
  "accountId": 1,
  "formId": 432,
  "data": {
    "billing": {
      "address": {
        "city": "Sacramento",
        "country": "US",
        "postalCode": "95814",
        "state": "CA",
        "street1": "123 Any St."
      },
      "card": {
        "cardNumber": "VISA-1111",
        "expMonth": 4,
        "expYear": 2018
      },
      "check": {
        "accountType": "Bank Name",
        "accountNumber": "XXXX4111",
        "routingNumber": "123456789"
      },
      "email": "no-reply@webconnex.com",
      "name": {
        "first": "Robert",
        "last": "Jones"
      },
      "paymentMethod": "card"
    },
    "id": "14508051894641200000",
    "customerId": 8210,
    "orderNumber": "NWBGBY-xxx-xxx",
    "orderStatus": "completed",
    "registrants": [
      {
        "amount": 100,
        "data": [
          {
            "first": {
              "label": "First Name",
              "type": "nameField",
              "value": "Robert"
            },
            "key": "name",
            "label": "Name",
            "last": {
              "label": "Last Name",
              "type": "nameField",
              "value": "Jones"
            },
            "type": "name"
          },
          {
            "key": "registrationOptions",
            "label": "Registration Options",
            "options": [
              {
                "amount": "100",
                "discount": "0",
                "key": "option1",
                "label": "Option 1",
                "price": "100",
                "type": "regOption",
                "value": true
              }
            ],
            "type": "regOptions",
            "value": "option1"
          },
          {
            "city": {
              "label": "City",
              "type": "textField",
              "value": "Sacramento"
            },
            "country": {
              "label": "Country",
              "type": "textField",
              "value": "US"
            },
            "key": "address",
            "label": "Address",
            "postalCode": {
              "label": "ZIP/Postal Code",
              "type": "textField",
              "value": "95814"
            },
            "state": {
              "label": "State",
              "type": "textField",
              "value": "CA"
            },
            "street1": {
              "label": "Street Address",
              "type": "textField",
              "value": "1233 Any St."
            },
            "type": "address"
          },
          {
            "key": "email",
            "label": "Email",
            "type": "email",
            "value": "nathanael@wearebunker.com"
          }
        ],
        "id": "145080518947020000"
      }
    ],
    "registrationTimestamp": "2015-12-22T17:26:29Z",
    "total": 100
  }
}
```

The registration event is fired whenever a successful registration has occurred on a form that you have set up a webhook for. The payload will resemble the fields in the form tied to the webhook event.

#### Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
eventId | integer | ID of the registration webhook event.
eventType | string | registration
accountId | integer | ID of the account
formId | integer | ID of the form
data | object | Object contains the complete payload for the registration
meta | object | Object contains information about the webhook.

#### Data values

Parameter | Default | Description
--------- | ------- | -----------
total | float | The total value of the registration
billing | object | Object contains the billing information
registrants | object | Object contains all the fields for the registrant(s)
tickets | object | Object contains all the fields for the ticket(s)
id | string | Unique hash for the registration
lookupId | integer | Internal ID of the registration
customerId | integer | ID of the purchasing customer
metrics | object | Contains certain metrics from the registration
orderNumber | string | Unique order number built from accounting reference in the form
orderStatus | string | Status of the order
transactionReference  | string  | Transaction reference of the registration
registrationTimestamp | timestamp | UTC date and time

#### Meta values
Parameter | Default | Description
--------- | ------- | -----------
name | string | The name of the webhook
appKey | string | Self assigned application key (optional)

### Form Published

> Payload

```json
{
  "eventType": "publish",
  "accountId": 14,
  "formId": 14280,
  "data": {
    "accRef": "MMBRSHPTST",
    "currency": "USD",
    "datePublished": "2016-08-31T17:03:08Z",
    "eventStart": "2016-05-31T07:00:00Z",
    "id": 14280,
    "name": "Example Form",
    "product": "regfox.com",
    "publishedPath": "help.regfox.com/membership-test-ek",
    "status": "open",
    "timeZone": "America/Regina"
  },
  "meta": {
    "name": "Your webhook name"
  }
}
```

The publish event is fired whenever a successful form has been published on a form that you have set up a webhook for.

#### Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
eventId | integer | ID of the publish webhook event.
eventType | string | publish
formId | integer | ID of the form
accountId | integer | ID of the account
data | object | Object contains the complete payload for the publish event
meta | object | Object contains information about the webhook.

#### Data values

Parameter | Default | Description
--------- | ------- | -----------
id | integer | ID of the form
lookupId | integer | ID of the form
accRef | string | Form accounting reference
currency | string | Currency of the campaign
datePublished | date | Date form was last published
eventStart | date | Event start date (optional)
eventEnd | date | Event end date (optional)
registrationStart | date | Opening date for registration (optional)
registrationEnd| date | Ending date for registration (optional)
name | string | Name of the form
product | string | Product of the form
publishedPath | string | Name of the form
status | string | Status of the form
timeZone | string | Timezone of the form

#### Meta values
Parameter | Default | Description
--------- | ------- | -----------
name | string | The name of the webhook
appKey | string | Self assigned application key (optional)

### Subscription

> Payload

```json
{
  "eventType": "subscription",
  "accountId": 14,
  "formId": 1293,
  "eventId": 13533,
  "data": {
    "billing": {
      "address": {
        "city": "Sacramento",
        "country": "US",
        "postalCode": "95819",
        "state": "CA",
        "street1": "1440 44th street"
      },
      "card": {
        "cardNumber": "VISA-1111",
        "expMonth": 9,
        "expYear": 2022
      },
      "check": {
        "accountType": "Bank Name",
        "accountNumber": "XXXX4111",
        "routingNumber": "123456789"
      },
      "email": "eric@webconnex.com",
      "name": {
        "first": "Eric",
        "last": "Knopf"
      },
      "paymentMethod": "card"
    },
    "customerId": 2,
    "id": "1471026990929548076",
    "orderNumber": "CNFRMTNPGF-AWE-2",
    "orderStatus": "completed",
    "subscription": {
      "amount": 100,
      "category": "Bacon",
      "dateCreated": "2016-08-12T18:36:31Z",
      "dateLast": "2016-09-12T00:00:07Z",
      "dateNext": "2016-10-12T10:00:00Z",
      "dateUpdated": "2016-09-12T00:00:07Z",
      "email": "eric@webconnex.com",
      "id": 346,
      "paymentsLeft": -1,
      "paymentsLeftString": "unlimited",
      "schedule": "0 0 0 12 * *",
      "scheduleString": "12th of every month"
    },
    "total": 100,
    "transactionReference": "TESTERCHARGE"
  },
  "meta": {
    "name": "Alex test fast"
  }
}
```

The subscription / reoccurring event is fired whenever a successful subscription or deposit has been completed on a form that you have set up a webhook for.

#### Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
eventId | integer | ID of the subscription webhook event.
eventType | string | subscription
formId | integer | ID of the form
accountId | integer | ID of the account
data | object | Object contains the complete payload for the subscription event
meta | object | Object contains information about the webhook.

#### Data values

Parameter | Default | Description
--------- | ------- | -----------
id | string | Internal ID of the subscription
lookupId | string | ID of the subscription
customerId | integer | ID of the customer
billing | object | Object contains the billing information
orderNumber | string | Unique order number built from the form accounting reference
orderStatus | string | Status of the order
subscription | object | Object contains the subscription information
transactionReference  | string  | The transaction reference of processed transaction
total | float | The total value processed

#### Subscription values

Parameter | Default | Description
--------- | ------- | -----------
amount | float | The total value processed
category | string | Designated fund
dateCreated | date | Date of creation
dateUpdated | date | Date last updated (optional)
dateLast | date | Date of last processed
dateNext | date | Date of next process attempt

<dates>
email | string | Email address of the subscription
id | integer | Internal ID of the subscription
schedule | string | Cron formatted string detailing the schedule
scheduleString | string | Human readable schedule

#### Meta values
Parameter | Default | Description
--------- | ------- | -----------
name | string | The name of the webhook
appKey | string | Self assigned application key (optional)

### Test

> Payload

```json
{
  "eventType": "test",
  "formId": 1234,
  "eventId": 1234,
  "accountId": 14,
  "data": {
    "data": "Additional documentation available at http://docs.webconnex.io/divvy/",
    "eventId": 1234,
    "eventType": "test",
    "formId": 1234
  }
}
```

Used for testing

#### Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
eventType | string | test
eventId | integer | 1234
formId | integer | 1234
accountId | integer | ID of the account
data | object | Object contains the complete payload for the test event

#### Data values

Parameter | Default | Description
--------- | ------- | -----------
data |  string  | Random string to use as data payload
eventType | string | test
eventId | integer | 1234
formId | integer | 1234
