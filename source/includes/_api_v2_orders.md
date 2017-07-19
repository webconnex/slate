## Orders

### Search Orders
```shell
curl "https://api.webconnex.com/v2/public/search/orders?product=redpodium.com&pretty=true" \
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
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/search/orders?product=redpodium.com", nil)

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
            url="https://api.webconnex.com/v2/public/search/orders",
            params={
                "product": "redpodium.com",
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
        path: '/v2/public/search/orders?product=redpodium.com',
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
        "product":"redpodium.com",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/search/orders", method: .get, parameters: urlParams, headers: headers)
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
Parameter			                                      |	Description
----------------------------------------------------|---------------------------
**product**<br>*string*<br>(required)		        	  | Product url to search
**formId**<br>*integer*<br>(optional) 			        | Return results with matching registration form Id
**status**<br>*string*<br>(optional) 				        | Return matching statuses
**sort**<br>*string*<br>(optional) 			          	|
**limit**<br>*string*<br>(optional) 				        | Limit number of results returned
**greaterThanId**<br>*integer*<br>(optional) 		 		| Return results greater than provided id
**formId**<br>*integer*<br>(optional) 			       	| Return results matching the form id
**customerId**<br>*integer*<br>(optional) 			    | Return results matching the customer id
**orderEmail**<br>*string*<br>(optional) 			      | Return results matching provided email
**orderNumber**<br>*string*<br>(optional) 		      | Return results matching provided order number
**lessThanId**<br>*integer*<br>(optional) 		     	| Return results less than provided id
**startingAfter**<br>*integer*<br>(optional) 			  | Return results with id's after value
**dateCreatedBefore**<br>*timestamp*<br>(optional)  | Return results created before date
**dateCreatedAfter**<br>*timestamp*<br>(optional) 	| Return results created before date
**dateUpdatedBefore**<br>*timestamp*<br>(optional) 	| Return results updated before date
**dateUpdatedAfter**<br>*timestamp*<br>(optional) 	| Return results updated after date

#### Response Object
Attribute			                  |	Description
--------------------------------|-----------------------------------------------------
**id**<br>*integer* 				    | Unique id of the order
**displayId**<br>*string*				| Unique hash used as civilian facing id
**customerId**<br>*integer*			| Unique id of the associated customer
**customerEmail**<br>*string*		| Email of the associated customer
**billing**<br>*object*					| Billing object containing name and address details associated with order
**formId**<br>*integer*					| Id of the form that associated with the order
**formName**<br>*string*				| Name of the form that created order
**formAccRef**<br>*string*  		| Accounting reference of the form that created order
**status**<br>*string*					| Status of the order
**orderNumber**<br>*string*     | Order number
**total**<br>*float*				    | Total amount of the order
**currency**<br>*string*        | Currency of the order
**dateCreated**<br>*timestamp*  | Timestamp of the creation of the order
**dateUpdated**<br>*timestamp*  | Timestamp the order was last updated (optional)

### View Order by Id
```shell
curl "https://api.webconnex.com/v2/public/search/orders/11623?pretty=true&product=redpodium.com" \
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
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/search/orders/11623?product=redpodium.com", nil)

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
            url="https://api.webconnex.com/v2/public/search/orders/11623",
            params={
                "product": "redpodium.com",
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
        path: '/v2/public/search/orders/11623?product=redpodium.com',
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
        "product":"redpodium.com",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/search/orders/11623", method: .get, parameters: urlParams, headers: headers)
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
`GET /v2/public/search/orders/{id}?product=`

#### Request Params
Parameter		           	                |	Description
----------------------------------------|----------------------------------------
**id**<br>*string*<br>(required)			  | Id of the requested order
**product**<br>*string*<br>(required)   | Product url to search
**[]expand**<br>*string*<br>(optional)  | Return additional children (registrants, tickets, subscriptions)

#### Response Object
Attribute			                  |	Description
--------------------------------|-----------------------------------------------
**id**<br>*integer* 				    | Unique id of the order
**displayId**<br>*string*				| Unique hash used as civilian facing id
**customerId**<br>*integer*		  | Unique id of the associated customer
**customerEmail**<br>*string*		| Email of the associated customer
**billing**<br>*object*					| Billing object containing name and address details associated with order
**formId**<br>*integer*					| Id of the form that associated with the order
**formName**<br>*string*				| Name of the form that created order
**formAccRef**<br>*string*			| Accounting reference string of the form that created order
**status**<br>*string*					| Status of the order
**orderNumber**<br>*string*     | Order number
**total**<br>*float*            | Total amount of the order
**currency**<br>*string*        | Currency of the order
**dateCreated**<br>*timestamp*  | Timestamp of the creation of the order
**dateUpdated**<br>*timestamp*  | Timestamp the order was last updated (optional)
