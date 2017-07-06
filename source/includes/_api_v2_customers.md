##Customer

### Search Customers

#### HTTP Request
`GET /v2/public/search/customers`

> Example Response:

```json
{
  "responseCode": 200,
  "data": [
    {
      "id": 8233,
      "email": "help@webconnex.com",
      "amount": "0",
      "address": {
        "firstName": "John",
        "lastName": "Doe",
        "address": {
          "city": "Sacramento",
          "country": "US",
          "phone": "",
          "postalCode": "97008",
          "state": "CA",
          "street1": "123 main street",
          "street2": ""
        }
      },
      "dateCreated": "2016-09-12T20:39:08Z",
      "dateUpdated": "2016-10-06T04:25:10Z"
    },
    {
      "id": 8228,
      "email": "jack@awesomeco.co",
      "amount": "0",
      "billing": {
        "firstName": "Jack",
        "lastName": "Bauer",
        "address": {
          "city": "Sacramento",
          "country": "US",
          "phone": "",
          "postalCode": "95814",
          "state": "CA",
          "street1": "123 main street",
          "street2": ""
        }
      },
      "dateCreated": "2016-06-07T17:53:50Z",
      "dateUpdated": "2016-10-06T04:25:10Z"
    }
  ],
  "totalResults": 2,
}
```

####  Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**product**<br>*string*<br>required 			| Name of the product you to search for customers on
**email**<br>*string*<br>optional 				| Billing email you want to search on
**sort**<br>*string*<br>optional 			            	|
**limit**<br>*string*<br>optional 				          | limits the number of results returned
**greaterThanId**<br>*integer*<br>optional 		   		| filter customers to only show results greater than provided id
**lessThanId**<br>*integer*<br>optional 		       	| filter customers to only show results less than provided id
**startingAfter**<br>*integer*<br>optional 			    | filter customers to only show results with IDs after value
**dateCreatedBefore**<br>*timestamp*<br>optional 		| filter customers to only show results created before date
**dateCreatedAfter**<br>*timestamp*<br>optional 		| filter customers to only show results created before date
**dateUpdatedBefore**<br>*timestamp*<br>optional 		| filter customers to only show results updated before date
**dateUpdatedAfter**<br>*timestamp*<br>optional 		| filter customers to only show results updated after date


####  Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique ID of the customer
**email**<br>*string*					| Email of the associated customer
**billing**<br>*object*					| Billing object containing name and address details associated with customer
**amount**<br>*float*					| Total of customer transactions
**dateCreated**<br>*timestamp* | Date and time of the creation of the customer
**dateUpdated**<br>*timestamp* | Date and time the customer was last updated (optional)

### View Customers by ID

#### HTTP Request
`GET /v2/public/search/customers/{id}`

> Example Response:

```json
{
  "responseCode": 200,
  "data": [
    {
      "id": 8228,
      "email": "jack@awesomeco.co",
      "amount": "0",
      "billing": {
        "firstName": "Jack",
        "lastName": "Bauer",
        "address": {
          "city": "Sacramento",
          "country": "US",
          "phone": "",
          "postalCode": "95814",
          "state": "CA",
          "street1": "123 main street",
          "street2": ""
        }
      },
      "dateCreated": "2016-06-07T17:53:50Z",
      "dateUpdated": "2016-10-06T04:25:10Z"
    }
  ]
}
```

####  Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*string*<br>required 				| ID of the requested customer

####  Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique ID of the customer
**email**<br>*string*					| Email of the associated customer
**billing**<br>*object*					| Billing object containing name and address details associated with customer
**amount**<br>*float*					| Total of customer transactions
**dateCreated**<br>*timestamp* | Date and time of the creation of the customer
**dateUpdated**<br>*timestamp* | Date and time the customer was last updated (optional)
