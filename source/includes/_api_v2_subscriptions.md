### Subscriptions

#### Search Subscriptions
```shell
curl "https://api.webconnex.com/v2/public/search/subscriptions?product=givingfuel.com&pretty=true" \
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
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/search/subscriptions?product=givingfuel.com", nil)

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
            url="https://api.webconnex.com/v2/public/search/subscriptions",
            params={
                "product": "givingfuel.com",
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
// request Search
(function(callback) {
    'use strict';

    const httpTransport = require('https');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'api.webconnex.com',
        port: '443',
        path: '/v2/public/search/subscriptions?product=givingfuel.com',
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
        "product":"givingfuel.com",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/search/subscriptions", method: .get, parameters: urlParams, headers: headers)
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
      "id": 1,
      "displayId": "1",
      "formId": 213213,
      "formName": "Wizard Form",
      "formAccRef": "WZRDFRM",
      "customerId": 4623,
      "orderId": 212431,
      "orderDisplayId": "01BXQDE87DF34643DS",
      "orderNumber": "FRM-001040F",
      "orderEmail": "help@webconnex.com",
      "status": "active",
      "amount": "10.00",
      "deductible": "10.00",
      "adjustment": "0.00",
      "currency": "USD",
      "category": " fund name",
      "schedule": "16th of every month",
      "dateLast": "2017-09-16T00:00:14.202655988Z",
      "dateNext": "2017-10-16T10:00:00Z",
      "paymentsRemaining": "unlimited",
      "dateCreated": "2017-08-16T14:40:57Z",
      "dateUpdated": "2017-09-16T00:00:14.292478947Z"
    },
		{
      "id": 2,
      "displayId": "2",
      "formId": 243243,
      "formName": "My Form",
      "formAccRef": "FRMPRTII",
      "customerId": 2234,
      "orderId": 2234,
      "orderDisplayId": "01BXQDEDKY1TFNQ40BZ",
      "orderNumber": "FRMPRTII-001040F",
      "orderEmail": "help@webconnex.com",
      "status": "active",
      "amount": "20.00",
      "deductible": "20.00",
      "adjustment": "0.00",
      "currency": "USD",
      "category": " fund name",
      "schedule": "16th of every month",
      "dateLast": "2017-09-16T00:00:14.202655988Z",
      "dateNext": "2017-10-16T10:00:00Z",
      "paymentsRemaining": "56",
      "dateCreated": "2017-08-16T14:40:57Z",
      "dateUpdated": "2017-09-16T00:00:14.292478947Z"
    }
  ],
  "totalResults": 2
}
```
##### HTTP Request
`GET /v2/public/search/subscriptions?product=`

##### Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**product**<br>*string*<br>(required)		| Name of the product you to search for subscriptions against
**formId**<br>*integer*<br>(optional) 			         	| Filter subscriptions to only show results matching the form id
**status**<br>*string*<br>(optional) 				| Status string of the subscription you want to filter on
**sort**<br>*string*<br>(optional) 			            |
**limit**<br>*string*<br>(optional) 				        | Limits the number of results returned
**orderId**<br>*integer*<br>(optional) 		   		    | Filter subscriptions to only show results matching a provided order id
**orderDisplayId**<br>*string*<br>(optional) 		    | Filter subscriptions to only show results matching a provided order display id
**orderEmail**<br>*string*<br>(optional) 				    | Filter subscriptions to only show results matching the email
**orderNumber**<br>*string*<br>(optional) 				  | Filter subscriptions to only show results matching the order number
**greaterThanId**<br>*integer*<br>(optional) 		    | Filter subscriptions to only show results greater than provided id
**customerId**<br>*integer*<br>(optional) 				  | Filter subscriptions to only show results matching the customer id
**lessThanId**<br>*integer*<br>(optional) 		      | Filter subscriptions to only show results less than provided id
**startingAfter**<br>*integer*<br>(optional) 			  | Filter subscriptions to only show results with id's after value
**dateCreatedBefore**<br>*timestamp*<br>(optional) 	| Filter subscriptions to only show results created before date
**dateCreatedAfter**<br>*timestamp*<br>(optional) 	| Filter subscriptions to only show results created before date
**dateUpdatedBefore**<br>*timestamp*<br>(optional) 	| Filter subscriptions to only show results updated before date
**dateUpdatedAfter**<br>*timestamp*<br>(optional) 	| Filter subscriptions to only show results updated after date
**dateNextAfter**<br>*timestamp*<br>(optional) 		| Filter subscriptions to only show results scheduled to run after date
**dateLastAfter**<br>*timestamp*<br>(optional) 		| Filter subscriptions to only show results processed after date

##### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				      | Unique id of the subscription
**displayId**<br>*string*					| Unique hash used as civilian facing id
**customerId**<br>*integer*			| Unique id of the associated customer
**orderId**<br>*integer*				| Unique id of the order
**orderDisplayId**<br>*string*	| Unique hash used as civilian facing id
**orderNumber**<br>*string*			| Order number
**orderEmail**<br>*string*			| Email of the associated order
**formId**<br>*integer*					  | Id of the form that associated with the order
**formName**<br>*string*					| Name of the form that created subscription
**formAccRef**<br>*string*				| Accounting reference string of the form that created order
**status**<br>*string*					  | Status of the subscription
**amount**<br>*float*					    | Total amount of the subscription
**deductible**<br>*float*					| Deductible amount
**adjustment**<br>*float*					| Adjustment to be applied to next payment
**currency**<br>*string*          | Currency of the subscription
**category**<br>*string*          | Fund designated
**schedule**<br>*string*          | Human readable schedule
**dateLast**<br>*timestamp*       | Timestamp of the last successful payment
**dateNext**<br>*timestamp*       | Timestamp of the next schedule payment
**paymentsRemaining**<br>*string* | String representation of the number of remaining payments
**dateCreated**<br>*timestamp*    | Timestamp object was created
**dateUpdated**<br>*timestamp*    | Timestamp object was last updated (optional)

#### View Subscription by Id
```shell
curl "https://api.webconnex.com/v2/public/search/subscriptions/49675?pretty=true&product=givingfuel.com" \
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
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/search/subscriptions/49675?product=givingfuel.com", nil)

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
            url="https://api.webconnex.com/v2/public/search/subscriptions/49675",
            params={
                "product": "givingfuel.com",
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
        path: '/v2/public/search/subscriptions/49675?product=givingfuel.com',
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
        "product":"givingfuel.com",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/search/subscriptions/49675", method: .get, parameters: urlParams, headers: headers)
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
      "id": 23432,
      "displayId": "23432",
      "formId": 123,
      "formName": "Wizard Form",
      "formAccRef": "WZRDFRM",
      "customerId": 123,
      "orderId": 231,
      "orderDisplayId": "234FDSDGDF234123",
      "orderNumber": "FRM-001040F",
      "orderEmail": "help@webconnex.com",
      "status": "active",
      "amount": "10.00",
      "deductible": "10.00",
      "adjustment": "0.00",
      "currency": "USD",
      "category": " fund name",
      "schedule": "16th of every month",
      "dateLast": "2017-09-16T00:00:14.202655988Z",
      "dateNext": "2017-10-16T10:00:00Z",
      "paymentsRemaining": "unlimited",
      "dateCreated": "2017-08-16T14:40:57Z",
      "dateUpdated": "2017-09-16T00:00:14.292478947Z"
    }
  ]
}
```

##### HTTP Request
`GET /v2/public/search/subscriptions/{id}?product=`

##### Request Params
Parameter			                          |	Description
----------------------------------------|---------------------------------------------
**id**<br>*string*<br>(required)				| Id of the requested order
**product**<br>*string*<br>(required)		| Product to search against

##### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				      | Unique id of the subscription
**displayId**<br>*string*					| Unique hash used as civilian facing id
**customerId**<br>*integer*			| Unique id of the associated customer
**orderId**<br>*integer*				| Unique id of the order
**orderDisplayId**<br>*string*	| Unique hash used as civilian facing id
**orderNumber**<br>*string*			| Order number
**orderEmail**<br>*string*			| Email of the associated order
**formId**<br>*integer*					  | Id of the form that associated with the order
**formName**<br>*string*					| Name of the form that created subscription
**formAccRef**<br>*string*				| Accounting reference string of the form that created order
**status**<br>*string*					  | Status of the subscription
**amount**<br>*float*					    | Total amount of the subscription
**deductible**<br>*float*					| Deductible amount
**adjustment**<br>*float*					| Adjustment to be applied to next payment
**currency**<br>*string*          | Currency of the subscription
**category**<br>*string*          | Fund designated
**schedule**<br>*string*          | Human readable schedule
**dateLast**<br>*timestamp*       | Timestamp of the last successful payment
**dateNext**<br>*timestamp*       | Timestamp of the next schedule payment
**paymentsRemaining**<br>*string* | String representation of the number of remaining payments
**dateCreated**<br>*timestamp*    | Timestamp object was created
**dateUpdated**<br>*timestamp*    | Timestamp object was last updated (optional)
