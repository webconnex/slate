##Order

### Search Orders

> The above command returns JSON structured like this:

```json
{
  "responseCode": 200,
  "data": {
    "id": 11465,
    "displayId": "1457539197636702399",
    "customerId": 22,
    "customerEmail": "help@webconnex.com",
    "registrants": [
      {
        "id": 16163,
        "displayId": "1457539197644569641",
        "formId": 874,
        "formName": "Your Form",
        "formAccRef": "MMBRCTNS",
        "customerId": 22,
        "orderId": 11465,
        "orderDisplayId": "1457539197636702399",
        "orderNumber": "MMBRCTNS-001-1",
        "status": "completed",
        "total": "2.65",
        "amount": "2.65",
        "dateCreated": "2016-03-09T15:59:57Z",
        "dateUpdated": "2016-03-09T15:59:57Z"
      }
    ],
    "billing": {
      "firstName": "John",
      "lastName": "Doe",
      "address": {
        "city": "Sacramento",
        "country": "US",
        "postalCode": "95814",
        "state": "CA",
        "street1": "455 Capital Mall, Suite 604"
      }
    },
    "formId": 874,
    "formName": "Your Form",
    "formAccRef": "MMBRCTNS",
    "status": "3",
    "orderNumber": "MMBRCTNS-001-1",
    "total": "2.65",
    "currency": "USD",
    "dateCreated": "2016-03-09T15:59:57Z",
    "dateUpdated": "2016-05-02T22:32:22Z"
  },
  "totalResults": 1
}
```

#### HTTP Request
`GET /v2/public/search/orders`

#### Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**product**<br>*string*<br>required 			| Name of the product you to search for orders on
**formId**<br>*integer*<br>optional 			| ID of the form you want to filter orders by
**status**<br>*string*<br>optional 				| Status string of the order you want to filter on
**sort**<br>*string*<br>optional 			            	|
**limit**<br>*string*<br>optional 				          | limits the number of results returned
**greaterThanId**<br>*integer*<br>optional 		   		| filter orders to only show results greater than provided id
**formId**<br>*integer*<br>optional 			         	| filter orders to only show results matching the form id
**customerId**<br>*integer*<br>optional 				    | filter orders to only show results matching the customer id
**orderEmail**<br>*string*<br>optional 				      | filter orders to only show results matching the email
**orderNumber**<br>*string*<br>optional 				    | filter orders to only show results matching the order number
**lessThanId**<br>*integer*<br>optional 		       	| filter orders to only show results less than provided id
**startingAfter**<br>*integer*<br>optional 			    | filter orders to only show results with IDs after value
**dateCreatedBefore**<br>*timestamp*<br>optional 		| filter orders to only show results created before date
**dateCreatedAfter**<br>*timestamp*<br>optional 		| filter orders to only show results created before date
**dateUpdatedBefore**<br>*timestamp*<br>optional 		| filter orders to only show results updated before date
**dateUpdatedAfter**<br>*timestamp*<br>optional 		| filter orders to only show results updated after date

#### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique ID of the order
**displayId**<br>*string*					| ID string used as customer facing ID
**customerId**<br>*integer*					| ID of the associated customer
**customerEmail**<br>*string*					| Email of the associated customer
**billing**<br>*object*					| Billing object containing name and address details associated with order
**formId**<br>*integer*					| ID of the form that associated with the order
**formName**<br>*string*					| Name of the form that created order
**formAccRef**<br>*string*					| Accounting reference string of the form that created order
**status**<br>*string*					| Status of the order
**orderNumber**<br>*string*					| Order number
**total**<br>*float*					| Total cost of the order
**dateCreated**<br>*timestamp* | Date and time of the creation of the order
**dateUpdated**<br>*timestamp* | Date and time the order was last updated (optional)

### View Order by ID

> The above command returns JSON structured like this:

```json
{
  "responseCode": 200,
  "data": {
    "id": 11465,
    "displayId": "1457539197636702399",
    "customerId": 22,
    "customerEmail": "help@webconnex.com",
    "billing": {
      "firstName": "John",
      "lastName": "Doe",
      "address": {
        "city": "Sacramento",
        "country": "US",
        "postalCode": "95814",
        "state": "CA",
        "street1": "455 Capital Mall, Suite 604"
      }
    },
    "formId": 874,
    "formName": "Your Form",
    "formAccRef": "MMBRCTNS",
    "status": "3",
    "orderNumber": "MMBRCTNS-001-1",
    "total": "2.65",
    "currency": "USD",
    "dateCreated": "2016-03-09T15:59:57Z",
    "dateUpdated": "2016-05-02T22:32:22Z"
  },
  "totalResults": 1
}
```

#### HTTP Request
`GET /v2/public/search/orders/{id}`

#### Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*string*<br>required 				| ID of the requested order

#### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique ID of the order
**displayId**<br>*string*					| ID string used as customer facing ID
**customerId**<br>*integer*					| ID of the associated customer
**customerEmail**<br>*string*					| Email of the associated customer
**billing**<br>*object*					| Billing object containing name and address details associated with order
**formId**<br>*integer*					| ID of the form that associated with the order
**formName**<br>*string*					| Name of the form that created order
**formAccRef**<br>*string*					| Accounting reference string of the form that created order
**status**<br>*string*					| Status of the order
**orderNumber**<br>*string*					| Order number
**total**<br>*float*					| Total cost of the order
**dateCreated**<br>*timestamp* | Date and time of the creation of the order
**dateUpdated**<br>*timestamp* | Date and time the order was last updated (optional)
