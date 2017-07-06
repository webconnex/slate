##Coupons

### Global coupons

#### HTTP Request
`GET /v2/public/coupons/global`

```shell
curl "https://api.webconnex.com/v2/public/coupons/global?product=redpodium.com" \
     -H "apiKey: XXXXXXXXXXXXXX"
```

> Example Response:

```json
{
  "responseCode": 200,
  "data": [{
    "id": 1109,
    "name": "100% off",
    "redeemed": 1,
    "currency": "USD",
    "available": 1,
    "discounts": [{
      "value": "100",
      "valueType": "percent"
    }],
    "codes": [
      {
        "code": "free",
        "redeemed": 1,
        "dateCreated": "2016-01-27T00:13:35Z"
      }
    ],
    "dateCreated": "2016-01-27T00:13:35Z"
  },{
    "id": 1199,
    "name": "HALF OFF",
    "redeemed": 4,
    "currency": "USD",
    "available": -1,
    "discounts": [{
      "value": "50",
      "valueType": "percent"
    }],
    "codes": [
      {
        "code": "half",
        "redeemed": 4,
        "dateCreated": "2016-01-27T00:13:35Z"
      }
    ],
    "dateCreated": "2016-01-27T00:13:35Z"
  }],
  "totalResults": 2
}
```

####  Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**Product**<br>*string*<br>required 				| Name of the product you to search for coupons on

####  Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique ID of the coupon
**name**<br>*string*					| The name of the coupon
**redeemed**<br>*integer*					| Number of coupons redeemed
**available**<br>*integer*  | Number of coupons available ([-1] means unlimited)
**currency**<br>*string*  | Currency of the coupon
**discounts**<br>*array*					| Discount associated with coupon
**codes**<br>*array*					| Codes associated with coupon
**dateCreated**<br>*timestamp* | Date and time of the creation of the order
**dateUpdated**<br>*timestamp* | Date and time the order was last updated (optional)

### View Coupon by form

#### HTTP Request
`GET /v2/public/coupons/forms/{formId}`

> Example Response:

```json
{
  "responseCode": 200,
  "data": [{
    "id": 1109,
    "name": "Free",
    "redeemed": 1,
    "currency": "USD",
    "available": 1,
    "discounts": [{
      "value": "100",
      "valueType": "percent"
    }],
    "codes": [
      {
        "code": "free",
        "redeemed": 1,
        "dateCreated": "2016-01-27T00:13:35Z"
      }
    ],
    "dateCreated": "2016-01-27T00:13:35Z"
  },{
    "id": 1199,
    "name": "HALF OFF",
    "redeemed": 4,
    "currency": "USD",
    "available": -1,
    "discounts": [{
      "value": "50",
      "valueType": "percent"
    }],
    "codes": [
      {
        "code": "half",
        "redeemed": 4,
        "dateCreated": "2016-01-27T00:13:35Z"
      }
    ],
    "dateCreated": "2016-01-27T00:13:35Z"
  }],
  "totalResults": 2
}
```

####  Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer*<br>required 				| Form ID to list coupons associated with

####  Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique ID of the coupon
**name**<br>*string*					| The name of the coupon
**redeemed**<br>*integer*					| Number of coupons redeemed
**available**<br>*integer*  | Number of coupons available ([-1] means unlimited)
**currency**<br>*string*  | Currency of the coupon
**discounts**<br>*array*					| Discount associated with coupon
**codes**<br>*array*					| Codes associated with coupon
**dateCreated**<br>*timestamp* | Date and time of the creation of the order
**dateUpdated**<br>*timestamp* | Date and time the order was last updated (optional)

### View Coupon by ID

#### HTTP Request
`GET /v2/public/coupons/{id}`

> Example Response:

```json
{
  "responseCode": 200,
  "data": {
    "id": 1222,
    "formId": 901,
    "name": "Series",
    "available": -1,
    "redeemed": 1,
    "currency": "USD",
    "discounts": [{
      "perTicket": false,
      "value": "100",
      "valueType": "percent"
    }],
    "codes": [{
      "code": "free1",
      "redeemed": 1,
      "dateCreated": "2016-08-15T21:25:23Z"
    }, {
      "code": "free2",
      "redeemed": 0,
      "dateCreated": "2016-08-15T21:25:23Z"
    }, {
      "code": "free3",
      "redeemed": 0,
      "dateCreated": "2016-08-15T21:25:23Z"
    }],
    "dateCreated": "2016-08-15T21:25:23Z"
  },
  "totalResults": 1
}
```

####  Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer*<br>required 				| ID of the requested coupon

####  Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique ID of the coupon
**name**<br>*string*					| The name of the coupon
**redeemed**<br>*integer*					| Number of coupons redeemed
**available**<br>*integer*  | Number of coupons available (-1 means unlimited)
**currency**<br>*string*  | Currency of the coupon
**discounts**<br>*array*					| Discount associated with coupon
**codes**<br>*array*					| Codes associated with coupon
**dateCreated**<br>*timestamp* | Date and time of the creation of the order
**dateUpdated**<br>*timestamp* | Date and time the order was last updated (optional)
