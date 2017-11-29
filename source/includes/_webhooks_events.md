## Webhooks Events

These are the system events that are available as webhook triggers.

### Registration

> Example Payload:

```json
{
  "eventType": "registration",
  "accountId": 1,
  "formId": 432,
  "customerId": 8210,
  "eventId": 112,
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
        "accountNumber": "VISA-4111",
        "routingNumber": "123456789"
      },
      "email": "no-reply@webconnex.com",
      "name": {
        "first": "Robert",
        "last": "Jones"
      },
      "paymentMethod": "card",
      "phone": "1530306026"
    },
    "id": "01BPYMJZHFJF34CZJJR",
    "lookupId": 112,
    "customerId": 8210,
    "currency": "USD",
    "deductibleTotal": 0,
    "orderNumber": "NWBGBY-AWS123",
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
        "id": "01BPYMJZHFJF34CZJJR"
      }
    ],
    "registrationTimestamp": "2015-12-22T17:26:29Z",
    "total": 100,
    "transactionId": 13313,
    "transactionReference": "TESTERCHARGE"
  },
  "meta": {
    "appKey": "Optional App Key",
    "name": "Optional Webconnex Name"
  }
}
```

The registration event is fired whenever a successful registration has occurred on a form that you have set up a webhook for. The payload will resemble the fields in the form tied to the webhook event.

#### Payload

Parameter  | Default | Description
---------- | ------- | ---------------------------------------------------------
eventType  | string  | registration
accountId  | integer | Id of the account
formId     | integer | Id of the form
customerId | integer | Id of the customer
eventId    | integer | Id of the registration webhook event.
data       | object  | Object contains the complete payload for the registration
meta       | object  | Object contains information about the webhook

#### Data Object

Parameter             | Default   | Description
--------------------- | --------- | ---------------------------------------------------------------
billing               | object    | Object contains the billing information
id                    | string    | Unique hash for the registration
lookupId              | Integer   | Internal id of the registration
customerId            | Integer   | Id of the purchasing customer
currency              | string    | The string representation of the order's currency
deductibleTotal       | float     | The total deductible amount of the order
orderNumber           | string    | Unique order number built from accounting reference in the form
orderStatus           | string    | Status of the order
registrants           | object    | Object contains all the fields for the registrant(s)
tickets               | object    | Object contains all the fields for the ticket(s)
total                 | float     | The total value of the registration
transactionReference  | string    | Transaction reference of the registration
transactionId         | Integer   | Transaction Id of the registration
registrationTimestamp | timestamp | UTC date and time

#### Meta Object

Parameter | Default | Description
--------- | ------- | ----------------------------------------
name      | string  | The name of the webhook
appKey    | string  | Self assigned application key (optional)

### Form Publish

> Example Payload:

```json
{
  "eventType": "publish",
  "accountId": 14,
  "formId": 14280,
  "eventId": 234,
  "data": {
    "accRef": "MMBRSHPTST",
    "currency": "USD",
    "datePublished": "2016-08-31T17:03:08Z",
    "eventStart": "2016-05-31T07:00:00Z",
    "eventEnd": "2016-07-31T07:00:00Z",
    "id": 14280,
    "name": "Example Form",
    "product": "regfox.com",
    "publishedPath": "help.regfox.com/membership-test-ek",
    "registrationEnd": "2016-08-19T07:00:00Z",
    "registrationStart": "2016-08-19T07:00:00Z",
    "status": "open",
    "timeZone": "America/Regina"
  },
  "meta": {
    "appKey": "Optional App Key",
    "name": "Your webhook name"
  }
}
```

The publish event is fired whenever a successful form has been published on a form that you have set up a webhook for.

#### Payload

Parameter | Default | Description
--------- | ------- | ----------------------------------------------------------
eventType | string  | The event type - "publish"
accountId | integer | Id of the account
formId    | integer | Id of the form
eventId   | integer | Id of the publish webhook event
data      | object  | Object contains the complete payload for the publish event
meta      | object  | Object contains information about the webhook

#### Data Object

Parameter         | Default   | Description
----------------- | --------- | ----------------------------------------
accRef            | string    | Form accounting reference
currency          | string    | Currency of the campaign
datePublished     | timestamp | Date form was last published
eventEnd          | timestamp | Event end date (optional)
eventStart        | timestamp | Event start date (optional)
id                | Integer   | Id of the form
name              | string    | Name of the form
product           | string    | Product of the form
publishedPath     | string    | Name of the form
registrationEnd   | timestamp | Ending date for registration (optional)
registrationStart | timestamp | Opening date for registration (optional)
status            | string    | Status of the form
timeZone          | string    | Timezone of the form

#### Meta Object

Parameter | Default | Description
--------- | ------- | ----------------------------------------
name      | string  | The name of the webhook
appKey    | string  | Self assigned application key (optional)


### Subscription / Reoccurring Notification

> Example Payload:

```json
{
  "eventType": "subscription",
  "accountId": 14,
  "formId": 1293,
  "customerId": 2,
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
        "accountNumber": "4111",
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
    "id": "01BPYMJZHFJF34CZJJR",
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
    "currency": "USD",
    "deductibleTotal": 100,
    "total": 100,
    "transactionId": 2423,
    "transactionReference": "TESTERCHARGE"
  },
  "meta": {
    "appKey": "Optional App Key",
    "name": "Subscription Webhooks"
  }
}
```

The subscription / reoccurring event is fired whenever a successful subscription or deposit has been completed on a form that you have set up a webhook for.

#### Payload

Parameter  | Default | Description
---------- | ------- | ---------------------------------------------------------------
eventType  | string  | The event type - "subscription"
accountId  | integer | Id of the account
formId     | integer | Id of the form
customerId | integer | Id of the purchasing customer
eventId    | integer | Id of the subscription webhook event
data       | object  | Object contains the complete payload for the subscription event
meta       | object  | Object contains information about the webhook

#### Data Object

Parameter            | Default | Description
-------------------- | ------- | ------------------------------------------------
id                   | string  | Internal Id of the subscription
lookupId             | string  | Id of the subscription
customerId           | integer | Id of the customer
billing              | object  | Object contains the billing information
orderNumber          | string  | Unique order number built from the form accounting reference
orderStatus          | string  | Status of the order
currency             | string  | The currency of campaign
deductibleTotal      | float   | The total deductible amount of the order
subscription         | object  | Object contains the subscription/reoccurring information
transactionReference | string  | The transaction reference of processed transaction
transactionId        | integer | Transaction Id of the subscription
total                | float   | The total value processed

#### Subscription Object

Parameter      | Default   | Description
-------------- | --------- | ----------------------------------------------------------
amount         | float     | The amount value of the subscription/reoccurring payment
category       | string    | Designated fund
dateCreated    | timestamp | Date of creation
dateUpdated    | timestamp | Date last updated (optional)
dateLast       | timestamp | Date of last processed
dateNext       | timestamp | Date of next process attempt
email          | string    | Email address of the subscription/reoccurring payment
id             | Integer   | Internal id of the subscription/reoccurring payment
schedule       | string    | Cron formatted string detailing the schedule
scheduleString | string    | Human readable schedule
status         | string    | The current status of the subscription/reoccurring payment

#### Meta Object

Parameter | Default | Description
--------- | ------- | ----------------------------------------
name      | string  | The name of the webhook
appKey    | string  | Self assigned application key (optional)


### Reoccurring SMS Donation Notification (Beta)

> Example Payload:

```json
{
	"eventType": "sms",
	"accountId": 14,
	"formId": 40556,
	"customerId": 15,
	"eventId": 15722,
	"data": {
		"id": "01BV2JNE10AGKDQSQF1",
		"lookupId": 13457,
		"customerId": 15,
		"transactionReference": "TESTERCHARGE",
		"orderStatus": "completed",
		"orderNumber": "TXTMTSD-AWE000K",
		"total": 25,
		"currency": "USD",
		"deductibleTotal": 25,
		"email": "gracious+donnor@webconnex.com",
		"category": "New Campus",
		"donorNumber": "+19160000000",
		"text2GiveNumber": "+19164356496",
		"billing": {
			"address": {
				"city": "Sacramento",
				"country": "US",
				"postalCode": "95814",
				"state": "CA",
				"street1": "455 Capitol Mall - Sixth Floor"
			},
			"card": {
				"cardNumber": "VISA-1111",
				"expMonth": 6,
				"expYear": 2019
			},
      "check": {
				"accountType": "checking",
				"accountNumber": "XXXXX6789",
				"routingNumber": "021000021",
				"bankName": "Acme"
			},
			"email": "gracious+donnor@webconnex.com",
			"phone": "19160000000",
			"fullName": "Alex Sherry",
			"name": {
				"first": "Alex",
				"last": "Sherry"
			},
			"paymentMethod": "card"
		}
	},
	"meta": {
		"name": "SMS"
	}
}
```

The sms event is fired whenever followup sms donation is created. Please contact support if you are interested in joining the "Reoccurring SMS Donation Notification" Beta test program.

Note: This only includes followup donations, the initial text 2 give donation is sent though the `New Registrations/Orders` webhook.

#### Payload

Parameter  | Default | Description
---------- | ------- | ---------------------------------------------------------------
eventType  | string  | The event type - "sms"
accountId  | integer | Id of the account
formId     | integer | Id of the form
customerId | integer | Id of the purchasing customer
eventId    | integer | Id of the subscription webhook event
data       | object  | Object contains the complete payload for the subscription event
meta       | object  | Object contains information about the webhook

#### Data Object

Parameter            | Default | Description
-------------------- | ------- | ------------------------------------------------------------
id                   | string  | Id of the Order
lookupId             | string  | Internal Id of the Order
customerId           | integer | Id of the customer
transactionId        | integer | Id of the transaction
transactionReference | string  | The transaction reference of processed transaction
transactionStatus    | string  | The result of the transaction (See appendix for details)
orderStatus          | string  | Status of the order (See appendix for details)
orderNumber          | string  | Unique order number built from the form accounting reference
total                | float   | The total value processed
currency             | string  | The currency of campaign
deductibleTotal      | float   | The total deductible amount of the order
email                | string  | Email address of tied to the Order
category             | string  | Designated fund
donorNumber          | string  | The personal number of the donor used to text in
text2GiveNumber      | string  | The donation level tied to the campaign
billing              | object  | Object contains the billing information


### Inventory

> Example Payload:

```json
{
  "eventType": "inventory_100",
  "accountId": 1,
  "formId": 25673,
  "eventId": 33764,
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
    "appKey": "Optional App Key",
    "name": "Inventory Webhook Test"
  }
}
```

The inventory event is fired whenever an inventory item reaches 80%, 90% and 100% sold capacity on a form that you have set up a webhook for.

#### Payload

Parameter | Default | Description
--------- | ------- | ----------------------------------------------------------------
eventType | string  | The event type - "inventory_80", "inventory_90", "inventory_100"
formId    | integer | Id of the form
accountId | integer | Id of the account
eventId   | integer | Id of the inventory webhook event
data      | object  | The object contains the complete payload for the inventory event
meta      | object  | Object contains information about the webhook

#### Data Object

Parameter    | Default   | Description
------------ | --------- | -----------------------------------------------------------------------------
dateCreated  | timestamp | Date the inventory item was created
dateUpdated  | timestamp | Date the inventory item was updated (optional)
formLookupId | int       | Id of the form used for requesting when calling from the public api
formName     | string    | The name of the form campaign
id           | string    | Id of the inventory item
inventory    | object    | An object containing the inventory supply data
itemName     | string    | The name of the inventory item
itemPath     | string    | The path of the inventory item
lookupId     | Int       | Id of the inventory item used for requesting when calling from the public api

#### Inventory Object

Parameter | Default | Description
--------- | ------- | -------------------------
quantity  | int     | The inventory limit
sold      | int     | The amount inventory sold

#### Meta Object

Parameter | Default | Description
--------- | ------- | ----------------------------------------
name      | string  | The name of the webhook
appKey    | string  | Self assigned application key (optional)


### Coupons

> Example Payload:

```json
{
  "eventType": "coupon",
  "accountId": 1,
  "formId": 112,
  "eventId": 5675,
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
    "appKey": "Optional App Key",
    "name": "Push Notifications"
  }
}
```

The coupon event is fired whenever coupon is created, updated or redeemed. Only global and forms that you have enabled will be delivered by the webhook.

#### Payload

Parameter | Default | Description
--------- | ------- | -------------------------------------------------------------
eventType | string  | The event type - "coupon"
accountId | integer | Id of the account
formId    | integer | Id of the form
eventId   | integer | Id of the coupon webhook event
data      | object  | The object contains the complete payload for the coupon event
meta      | object  | Object contains information about the webhook

#### Data Object

Parameter   | Default   | Description
----------- | --------- | ----------------------------------------------------------------
couponId    | int       | Id of the coupon
available   | int       | Number of available redemptions ([-1] means unlimited)
redeemed    | int       | Number of redemptions
codes       | object    | The object container of all the coupon code objects
currency    | string    | The currency of coupon
codes       | object    | The object container of all the coupon code objects
name        | string    | The name of the coupon
formId      | string    | Id of the associated form (optional) [null] if coupon is global)
voucher     | bool      | Specifies if coupon is a voucher or not
dateCreated | timestamp | Date the inventory item was created
dateUpdated | timestamp | Date the inventory item was updated (optional)

#### Codes Object

Parameter | Default | Description
--------- | ------- | -------------------------------
id        | int     | Id of the code
couponId  | int     | Id of the parent coupon
code      | string  | Code used for coupon redemption
redeemed  | int     | Number of redemptions

#### Discounts Object

Parameter | Default   | Description
--------- | --------- | -----------------------------------------------------------------------------
paths     | [] string | An array of paths the coupon can be applied to
perTicket | bool      | Specifies weather discount should apply to each ticket (ticketspice.com only)
valueType | string    | Specifies the discount type - `Percent` or `Fixed`
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
    "data": "Additional documentation available at http://docs.webconnex.io/api/v2",
    "eventId": 1234,
    "eventType": "test",
    "formId": 1234
  }
}
```

Used for testing

#### Payload

Parameter | Default | Description
--------- | ------- | -------------------------------------------------------
eventType | string  | The event type - "test"
eventId   | integer | Random number used as event id
formId    | integer | Random number used as form id
accountId | integer | Id of the account
data      | object  | Object contains the complete payload for the test event

#### Data Object

Parameter | Default | Description
--------- | ------- | ------------------------------------
data      | string  | Random string to use as data payload
eventType | string  | The event type - "test"
eventId   | integer | Random number used as event id
formId    | integer | Random number used as form id