## Webhooks Events

These are the system events that are available as webhook triggers.

### Registration

> Example Payload:

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
        "accountNumber": "<YOUR API KEY>4111",
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
    "orderNumber": "NWBGBY-<YOUR API KEY>",
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
            "value": "help@webconnex.com"
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

#### Payload
Parameter | Default | Description
--------- | ------- | -----------
eventId | Integer | Id of the registration webhook event.
eventType | string | registration
accountId | Integer | Id of the account
formId | Integer | Id of the form
data | object | Object contains the complete payload for the registration
meta | object | Object contains information about the webhook.

#### Data Object
Parameter | Default | Description
--------- | ------- | -----------
total | float | The total value of the registration
billing | object | Object contains the billing information
registrants | object | Object contains all the fields for the registrant(s)
tickets | object | Object contains all the fields for the ticket(s)
id | string | Unique hash for the registration
lookupId | Integer | Internal id of the registration
customerId | Integer | Id of the purchasing customer
metrics | object | Contains certain metrics from the registration
orderNumber | string | Unique order number built from accounting reference in the form
orderStatus | string | Status of the order
transactionReference  | string  | Transaction reference of the registration
registrationTimestamp | timestamp | UTC date and time

#### Meta Object
Parameter | Default | Description
--------- | ------- | -----------
name | string | The name of the webhook
appKey | string | Self assigned application key (optional)

### Form Publish

> Example Payload:

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

#### Payload
Parameter | Default | Description
--------- | ------- | -----------
eventId | Integer | Id of the publish webhook event.
eventType | string | publish
formId | Integer | Id of the form
accountId | Integer | Id of the account
data | object | Object contains the complete payload for the publish event
meta | object | Object contains information about the webhook.

#### Data Object
Parameter | Default | Description
--------- | ------- | -----------
id | Integer | Id of the form
lookupId | Integer | Id of the form
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

#### Meta Object
Parameter | Default | Description
--------- | ------- | -----------
name | string | The name of the webhook
appKey | string | Self assigned application key (optional)

### Subscription

> Example Payload:

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
        "postalCode": "95814",
        "state": "CA",
        "street1": "455 Capital Mall"
      },
      "card": {
        "cardNumber": "VISA-1111",
        "expMonth": 9,
        "expYear": 2022
      },
      "check": {
        "accountType": "Bank Name",
        "accountNumber": "<YOUR API KEY>4111",
        "routingNumber": "123456789"
      },
      "email": "help@webconnex.com",
      "name": {
        "first": "John",
        "last": "Doe"
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
      "email": "help@webconnex.com",
      "id": 346,
      "paymentsLeft": -1,
      "paymentsLeftString": "unlimited",
      "schedule": "0 0 0 12 * *",
      "scheduleString": "12th of every month",
      "status": "active",
    },
    "total": 100,
    "transactionReference": "TESTERCHARGE"
  },
  "meta": {
    "name": "Subscription Webhooks"
  }
}
```

The subscription / reoccurring event is fired whenever a successful subscription or deposit has been completed on a form that you have set up a webhook for.

#### Payload
Parameter | Default | Description
--------- | ------- | -----------
eventId | Integer | Id of the subscription webhook event.
eventType | string | subscription
formId | Integer | Id of the form
accountId | Integer | Id of the account
data | object | Object contains the complete payload for the subscription event
meta | object | Object contains information about the webhook.

#### Data Object
Parameter | Default | Description
--------- | ------- | -----------
id | string | Internal id of the subscription
lookupId | string | Id of the subscription
customerId | Integer | Id of the customer
billing | object | Object contains the billing information
orderNumber | string | Unique order number built from the form accounting reference
orderStatus | string | Status of the order
subscription | object | Object contains the subscription information
transactionReference  | string  | The transaction reference of processed transaction
total | float | The total value processed

#### Subscription Object
Parameter | Default | Description
--------- | ------- | -----------
amount | float | The total value processed
category | string | Designated fund
dateCreated | date | Date of creation
dateUpdated | date | Date last updated (optional)
dateLast | date | Date of last processed
dateNext | date | Date of next process attempt
email | string | Email address of the subscription
id | Integer | Internal id of the subscription
schedule | string | Cron formatted string detailing the schedule
scheduleString | string | Human readable schedule
status | string | The current status of the subscription

#### Meta Object
Parameter | Default | Description
--------- | ------- | -----------
name | string | The name of the webhook
appKey | string | Self assigned application key (optional)

### Inventory

> Example Payload:

```json
{
  "eventType": "inventory_100",
  "accountId": 1,
  "formId": 25673,
  "data": {
    "dateCreated": "2016-11-04T16:28:00Z",
    "dateUpdated": "2016-11-04T16:55:39Z",
    "formLookupId": 25673,
    "formName": "Example 5k Campaign",
    "id": 33764,
    "inventory": {
      "quantity": 4000,
      "sold": 4000
    },
    "itemName": "Fun 5K",
    "itemPath": "registrants.registrationOptions.option1",
    "lookupId": 33764
  },
  "meta": {
    "name": "Inventory Webhook Test"
  }
}
```

The inventory event is fired whenever an inventory item reaches 80%, 90% and 100% sold capacity on a form that you have set up a webhook for.

#### Payload
Parameter | Default | Description
--------- | ------- | -----------
eventType | string | Inventory_80, inventory_90, inventory_100
formId | Integer | Id of the form
accountId | Integer | Id of the account
data | object | The object contains the complete payload for the inventory event
meta | object | Object contains information about the webhook

#### Data Object
Parameter | Default | Description
--------- | ------- | -----------
dateCreated |  date  | Date the inventory item was created
dateUpdated |  date  | Date the inventory item was updated  (optional)
formLookupId |  int  | Id of the form used for requesting when calling from the public api
formName |  string  | The name of the form campaign
id | string | Id of the inventory item
inventory | object | An object containing the inventory supply data
itemName | string | The name of the inventory item
itemPath | string | The path of the inventory item
lookupId | Int | Id of the inventory item used for requesting when calling from the public api

#### Inventory Object
Parameter | Default | Description
--------- | ------- | -----------
quantity |  int  | The inventory limit
sold |  int  | The amount inventory sold

#### Meta Object
Parameter | Default | Description
--------- | ------- | -----------
name | string | The name of the webhook
appKey | string | Self assigned application key (optional)


### Coupons

> Example Payload:

```json
{
  "eventType": "coupon",
  "accountId": 1,
  "data": {
    "available": -1,
    "codes": [
      {
        "code": "half_off",
        "couponId": 343,
        "id": 3345,
        "redeemed": 3
      }
    ],
    "couponId": 343,
    "currency": "USD",
    "dateCreated": "2016-12-29T06:14:28Z",
    "dateUpdated": "2017-03-03T20:38:48Z",
    "discounts": [
      {
        "paths": [
          "registrants.registrationOptions.option1"
        ],
        "perTicket": false,
        "value": "50",
        "valueType": "percent"
      }
    ],
    "formId": 29815,
    "name": "Social Media Campaign",
    "redeemed": 3,
    "voucher": false
  },
  "meta": {
    "name": "Push Notifications"
  }
}
```

The coupon event is fired whenever coupon is created, updated or redeemed. Only global and forms that you have enabled will be delivered by the webhook.

#### Payload

Parameter | Default | Description
----------|---------|-----------------------------------------------------------
eventType | string  | coupon
formId    | Integer | Id of the form
accountId | Integer | Id of the account
data      | object  | The object contains the complete payload for the coupon event
meta      | object  | Object contains information about the webhook

#### Data Object
Parameter   | Default | Description
------------|---------|--------------------------------------------------------
couponId    |  int    | Id of the coupon
available   |  int    | Number of available redemptions  ([-1] means unlimited)
redeemed    |  int    | Number of redemptions
codes       | object  | The object container of all the coupon code objects
currency    | string  | The currency of coupon
codes       | object  | The object container of all the coupon code objects
name        | string  | The name of the coupon
formId      | string  | Id of the associated form (optional) [null] if coupon is global)
voucher     | bool   | Specifies if coupon is a voucher or not
dateCreated |  date  | Date the inventory item was created
dateUpdated |  date  | Date the inventory item was updated  (optional)

#### Codes Object
Parameter | Default | Description
----------|---------|--------------------------------
id        |  int    | Id of the code
couponId  |  int    | Id of the parent coupon
code      |  string | Code used for coupon redemption
redeemed  |  int    | Number of redemptions

#### Discounts Object
Parameter | Default   | Description
----------|-----------|---------------------------------------------------------
paths     | [] string | An array of paths the coupon can be applied to
perTicket | bool      | Specifies weather discount should apply to each ticket (ticketspice.com Only)
valueType | string    | Specifies the discount type (Percent or Fixed)
value     | string    | Value amount to apply

### Test

> Example Payload:

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

#### Payload
Parameter | Default | Description
--------- | ------- | -----------
eventType | string  | test
eventId   | Integer | Random number used as event id
formId    | Integer | Random number used as form id
accountId | Integer | Id of the account
data      | object  | Object contains the complete payload for the test event

#### Data Object
Parameter | Default | Description
--------- | ------- | -----------
data      |  string | Random string to use as data payload
eventType | string  | test
eventId   | Integer | Random number used as event id
formId    | Integer | Random number used as form id
