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
      "check": {},
      "email": "no-reply@webconnex.com",
      "name": {
        "first": "Robert",
        "last": "Jones"
      },
      "paymentMethod": "card"
    },
    "id": "14508051894641200000",
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

The registration event is fired whenever a successful registration has occured on a form that you have set up a webhook for. The payload will resemble the fields in the form tied to the webhook event.

#### Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
eventID | string | registration
formId | integer | ID of the form
accountId | integer | ID of the account
registrationTimestamp | timestamp | UTC date and time
total | float | the total value of the registration
data | object | the object container the complete payload for the registration

#### Data values

Parameter | Default | Description
--------- | ------- | -----------
billing | object | Object contains the billing information
registrants | object | Contains all the fields for the registrant(s)
tickets | object | Contains all the fields for the tickets
id | string | unique has for the registration
metrics | object | contains certain metrics from the registration (incomplete)
orderNumber | string | unique order number built from accounting reference in the form

### Form Published

> Payload
```json
{
  "eventType": "test",
  "formId": 0,
  "eventId": 1234,
  "data": {
    "data": "Additional documentation available at http://docs.webconnex.io/divvy/",
    "eventId": 1,
    "eventType": "test",
    "formId": 0
  }
}
```


### Subscription

> Payload

```json
{
  "eventType": "test",
  "formId": 0,
  "eventId": 1234,
  "data": {
    "data": "Additional documentation available at http://docs.webconnex.io/divvy/",
    "eventId": 1,
    "eventType": "test",
    "formId": 0
  }
}
```


### Test

> Payload

```json
{
  "eventType": "test",
  "formId": 0,
  "eventId": 1234,
  "data": {
    "data": "Additional documentation available at http://docs.webconnex.io/divvy/",
    "eventId": 1,
    "eventType": "test",
    "formId": 0
  }
}
```

Used for testing
