### Transactions

#### Search Transactions
```shell
curl "https://api.webconnex.com/v2/public/search/transactions?product=regfox.com&pretty=true" \
     -H "apiKey: <YOUR API KEY>"
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func search() {

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/search/transactions?product=regfox.com", nil)

	// Headers
	req.Header.Add("apiKey", "<YOUR API KEY>")

	parseFormErr := req.ParseForm()
	if parseFormErr != nil {
	  fmt.Println(parseFormErr)    
	}

	// Fetch Request
	resp, err := client.Do(req)

	if err != nil {
		fmt.Println("Failure : ", err)
	}

	// Read Response Body
	respBody, _ := ioutil.ReadAll(resp.Body)

	// Display Results
	fmt.Println("response Status : ", resp.Status)
	fmt.Println("response Headers : ", resp.Header)
	fmt.Println("response Body : ", string(respBody))
}
```
```python
# Install the Python Requests library:
# `pip install requests`

import requests

def send_request():
    try:
        response = requests.get(
            url="https://api.webconnex.com/v2/public/search/transactions",
            params={
                "product": "regfox.com",
            },
            headers={
                "apiKey": "<YOUR API KEY>",
            },
        )
        print('Response HTTP Status Code: {status_code}'.format(
            status_code=response.status_code))
        print('Response HTTP Response Body: {content}'.format(
            content=response.content))
    except requests.exceptions.RequestException:
        print('HTTP Request failed')
```
```javascript
(function(callback) {
    'use strict';

    const httpTransport = require('https');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'api.webconnex.com',
        port: '443',
        path: '/v2/public/search/transactions?product=regfox.com',
        method: 'GET',
        headers: {"apiKey":"<YOUR API KEY>"}
    };
    httpOptions.headers['User-Agent'] = 'node ' + process.version;

    const request = httpTransport.request(httpOptions, (res) => {
        let responseBufs = [];
        let responseStr = '';

        res.on('data', (chunk) => {
            if (Buffer.isBuffer(chunk)) {
                responseBufs.push(chunk);
            }
            else {
                responseStr = responseStr + chunk;            
            }
        }).on('end', () => {
            responseStr = responseBufs.length > 0 ?
                Buffer.concat(responseBufs).toString(responseEncoding) : responseStr;

            callback(null, res.statusCode, res.headers, responseStr);
        });

    })
    .setTimeout(0)
    .on('error', (error) => {
        callback(error);
    });
    request.write("")
    request.end();

})((error, statusCode, headers, body) => {
    console.log('ERROR:', error);
    console.log('STATUS:', statusCode);
    console.log('HEADERS:', JSON.stringify(headers));
    console.log('BODY:', body);
});
```
```swift
func searchRequest() {

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Add URL parameters
    let urlParams = [
        "product":"regfox.com",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/search/transactions", method: .get, parameters: urlParams, headers: headers)
        .validate(statusCode: 200..<300)
        .responseJSON { response in
            if (response.result.error == nil) {
                debugPrint("HTTP Response Body: \(response.data)")
            }
            else {
                debugPrint("HTTP Request failed: \(response.result.error)")
            }
        }
}
```

> API returns JSON structured like this:

```json
{
  "responseCode": 200,
  "data": [
    {
      "id": 15665,
      "displayId": "15665",
      "formId": 1440,
      "formName": "test campaign",
      "formAccRef": "DPSTTST",
      "customerId": 8302,
      "orderId": 13429,
      "orderDisplayId": "01BTB7W4K8E9TZM6BFR",
      "orderNumber": "DPSTTST-0010005",
      "orderEmail": "Job.Bluth@webconnex.com",
      "billing": {
        "firstName": "Job",
        "lastName": "Bluth",
        "address": {
          "city": "Sacramento",
          "country": "US",
          "postalCode": "95814",
          "state": "CA",
          "street1": "455 Capitol Mall STE 604"
        }
      },
      "transactionType": "charge",
      "total": "50.00",
      "deductible": "0.00",
      "currency": "USD",
      "paymentMethod": "card",
      "paymentType": "MAST",
      "paymentMask": "MAST-2424",
      "gatewayReference": "TESTERCHARGE",
      "gatewayMessage": "Approved",
      "status": "completed",
      "dateCreated": "2017-09-18T19:36:38Z",
      "dateUpdated": "2017-09-18T19:36:39Z"
    }, {
     "id": 14854,
     "displayId": "14854",
     "formId": 1440,
     "formName": "deposit test",
     "formAccRef": "DPSTTST",
     "customerId": 1179,
     "orderId": 13112,
     "orderDisplayId": "1494519032659439046",
     "orderNumber": "DPSTTST-0010004",
     "orderEmail": "george.Micheal@webconnex.com",
     "billing": {
       "firstName": "George",
       "lastName": "Micheal",
       "address": {
         "city": "Sacramento",
         "country": "US",
         "postalCode": "95814",
         "state": "CA",
         "street1": "455 Capitol Mall"
       }
     },
     "transactionType": "charge",
     "total": "500.00",
     "deductible": "0.00",
     "currency": "USD",
     "paymentMethod": "card",
     "paymentType": "VISA",
     "paymentMask": "VISA-3112",
     "gatewayReference": "TESTERCHARGE",
     "gatewayMessage": "Approved",
     "status": "completed",
     "dateCreated": "2017-05-11T16:10:33Z",
     "dateUpdated": "2017-05-11T16:10:33Z"
   }
  ],
  "totalResults": 2
}
```
##### HTTP Request
`GET /v2/public/search/transactions?product=`

##### Request Params
Parameter			                                |	Description
----------------------------------------------|---------------------------------------
**product**<br>*string*<br>(required)	       	| Name of the product you to search for transactions against
**formId**<br>*integer*<br>(optional) 	     	| Id of the form you want to filter transactions by
**status**<br>*string*<br>(optional) 	  			| Status string of the transaction you want to filter on
**sort**<br>*string*<br>(optional) 	         	|
**limit**<br>*string*<br>(optional) 				  | Limits the number of results returned
**orderId**<br>*integer*<br>(optional) 		   	| Filter transactions to only show results matching a provided order id
**type**<br>*string*<br>(optional) 		   		  | Filter transactions to only show results matching a provided type (types include: charge, refund, voucher)
**orderDisplayId**<br>*string*<br>(optional)  | Filter transactions to only show results matching a provided order display id
**greaterThanId**<br>*integer*<br>(optional)  | Filter transactions to only show results greater than provided id
**formId**<br>*integer*<br>(optional) 		   	| Filter transactions to only show results matching the form id
**customerId**<br>*integer*<br>(optional) 	  | Filter transactions to only show results matching the customer id
**orderEmail**<br>*string*<br>(optional) 			| Filter transactions to only show results matching the email
**orderNumber**<br>*string*<br>(optional) 		      | Filter transactions to only show results matching the order number
**txReference**<br>*string*<br>(optional) 			    | Filter transactions to only show results matching the transaction reference
**lessThanId**<br>*integer*<br>(optional) 		     	| Filter transactions to only show results less than provided id
**startingAfter**<br>*integer*<br>(optional) 			  | Filter transactions to only show results with id's after value
**dateCreatedBefore**<br>*timestamp*<br>(optional)  | Filter transactions to only show results created before date
**dateCreatedAfter**<br>*timestamp*<br>(optional) 	| Filter transactions to only show results created before date
**dateUpdatedBefore**<br>*timestamp*<br>(optional) 	| Filter transactions to only show results updated before date
**dateUpdatedAfter**<br>*timestamp*<br>(optional) 	| Filter transactions to only show results updated after date

##### Response Object
Attribute			                 |	Description
-------------------------------|------------------------------------------------------
**id**<br>*integer* 				    | Unique Id
**displayId**<br>*string*				| Unique hash used as civilian facing id
**formId**<br>*integer*					| Id of the form that created transaction
**formName**<br>*string*				| Name of the form that created transaction
**formAccRef**<br>*string*			| Accounting reference string of the form that created transaction
**customerId**<br>*integer*			| Unique id of the associated customer
**orderId**<br>*integer*				| Unique id of the order
**orderDisplayId**<br>*string*	| Unique hash used as civilian facing id
**orderNumber**<br>*string*			| Order number
**orderEmail**<br>*string*			| Email of the associated order
**billing**<br>*object*					| Billing object containing name and address details associated with transaction
**transactionType**<br>*string*	| Type of transaction
**total**<br>*float*					  | Total cost of the transaction
**deductible**<br>*float*			  | Total tax deductible amount
**currency**<br>*string*        | Currency code
**paymentMethod**<br>*string*   | Payment method used
**paymentType**<br>*string*     | Payment type used
**paymentMask**<br>*string*     | Payment Mask
**gatewayReference**<br>*string*  | Transaction Reference provided by gateway
**gatewayMessage**<br>*string*  | Message returned by the the gateway
**parentTransactionId**<br>*string*  | Transaction to which a refund was applied (optional)
**status**<br>*string*				 | Status of the transaction
**dateCreated**<br>*timestamp* | Timestamp of the creation of the transaction
**dateUpdated**<br>*timestamp* | Timestamp the transaction was last updated (optional)

#### View Transaction by Id
```shell
curl "https://api.webconnex.com/v2/public/search/transactions/14291?pretty=true&product=regfox.com" \
     -H "apiKey: <YOUR API KEY>"
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func view() {

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/search/transactions/14291?product=regfox.com", nil)

	// Headers
	req.Header.Add("apiKey", "<YOUR API KEY>")

	parseFormErr := req.ParseForm()
	if parseFormErr != nil {
	  fmt.Println(parseFormErr)    
	}

	// Fetch Request
	resp, err := client.Do(req)

	if err != nil {
		fmt.Println("Failure : ", err)
	}

	// Read Response Body
	respBody, _ := ioutil.ReadAll(resp.Body)

	// Display Results
	fmt.Println("response Status : ", resp.Status)
	fmt.Println("response Headers : ", resp.Header)
	fmt.Println("response Body : ", string(respBody))
}
```
```python
# Install the Python Requests library:
# `pip install requests`

import requests

def send_request():
    try:
        response = requests.get(
            url="https://api.webconnex.com/v2/public/search/transactions/14291",
            params={
                "product": "regfox.com",
            },
            headers={
                "apiKey": "<YOUR API KEY>",
            },
        )
        print('Response HTTP Status Code: {status_code}'.format(
            status_code=response.status_code))
        print('Response HTTP Response Body: {content}'.format(
            content=response.content))
    except requests.exceptions.RequestException:
        print('HTTP Request failed')
```
```javascript
(function(callback) {
    'use strict';

    const httpTransport = require('https');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'api.webconnex.com',
        port: '443',
        path: '/v2/public/search/transactions/14291?product=regfox.com',
        method: 'GET',
        headers: {"apiKey":"<YOUR API KEY>"}
    };
    httpOptions.headers['User-Agent'] = 'node ' + process.version;

    const request = httpTransport.request(httpOptions, (res) => {
        let responseBufs = [];
        let responseStr = '';

        res.on('data', (chunk) => {
            if (Buffer.isBuffer(chunk)) {
                responseBufs.push(chunk);
            }
            else {
                responseStr = responseStr + chunk;            
            }
        }).on('end', () => {
            responseStr = responseBufs.length > 0 ?
                Buffer.concat(responseBufs).toString(responseEncoding) : responseStr;

            callback(null, res.statusCode, res.headers, responseStr);
        });

    })
    .setTimeout(0)
    .on('error', (error) => {
        callback(error);
    });
    request.write("")
    request.end();

})((error, statusCode, headers, body) => {
    console.log('ERROR:', error);
    console.log('STATUS:', statusCode);
    console.log('HEADERS:', JSON.stringify(headers));
    console.log('BODY:', body);
});
```
```swift
func viewRequest() {

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Add URL parameters
    let urlParams = [
        "product":"regfox.com",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/search/transactions/14291", method: .get, parameters: urlParams, headers: headers)
        .validate(statusCode: 200..<300)
        .responseJSON { response in
            if (response.result.error == nil) {
                debugPrint("HTTP Response Body: \(response.data)")
            }
            else {
                debugPrint("HTTP Request failed: \(response.result.error)")
            }
        }
}
```

> API returns JSON structured like this:

```json
{
  "responseCode": 200,
  "data": [
    {
     "id": 14854,
     "displayId": "14854",
     "formId": 1440,
     "formName": "deposit test",
     "formAccRef": "DPSTTST",
     "customerId": 1179,
     "orderId": 13112,
     "orderDisplayId": "1494519032659439046",
     "orderNumber": "DPSTTST-0010004",
     "orderEmail": "george.Micheal@webconnex.com",
     "billing": {
       "firstName": "George",
       "lastName": "Micheal",
       "address": {
         "city": "Sacramento",
         "country": "US",
         "postalCode": "95814",
         "state": "CA",
         "street1": "455 Capitol Mall"
       }
     },
     "transactionType": "charge",
     "total": "500.00",
     "deductible": "0.00",
     "currency": "USD",
     "paymentMethod": "card",
     "paymentType": "VISA",
     "paymentMask": "VISA-3112",
     "gatewayReference": "TESTERCHARGE",
     "status": "completed",
     "dateCreated": "2017-05-11T16:10:33Z",
     "dateUpdated": "2017-05-11T16:10:33Z"
   }
  ]
}
```
##### HTTP Request
`GET /v2/public/search/transactions/{id}?product=`

##### Request Params
Parameter			                  |	Description
--------------------------------|-----------------------------------------------------
**id**<br>*string*<br>(required) | Id of the requested transaction

##### URI Params
Parameter			                      |	Description
------------------------------------|--------------------------------------------------
**product**<br>*string*<br>(required)| Product to search against

##### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				    | Unique Id
**displayId**<br>*string*				| Unique hash used as civilian facing id
**formId**<br>*integer*					| Id of the form that created transaction
**formName**<br>*string*				| Name of the form that created transaction
**formAccRef**<br>*string*			| Accounting reference string of the form that created transaction
**customerId**<br>*integer*			| Unique id of the associated customer
**orderId**<br>*integer*				| Unique id of the order
**orderDisplayId**<br>*string*	| Unique hash used as civilian facing id
**orderNumber**<br>*string*			| Order number
**orderEmail**<br>*string*			| Email of the associated order
**billing**<br>*object*					| Billing object containing name and address details associated with transaction
**transactionType**<br>*string*	| Type of transaction
**total**<br>*float*					  | Total cost of the transaction
**deductible**<br>*float*			  | Total tax deductible amount
**currency**<br>*string*        | Currency code
**paymentMethod**<br>*string*   | Payment method used
**paymentType**<br>*string*     | Payment type used
**paymentMask**<br>*string*     | Payment Mask
**gatewayReference**<br>*string*  | transaction Reference provided by gateway
**status**<br>*string*				 | Status of the transaction
**dateCreated**<br>*timestamp* | Timestamp of the creation of the transaction
**dateUpdated**<br>*timestamp* | Timestamp the transaction was last updated (optional)
