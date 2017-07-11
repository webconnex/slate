## Customers

### Search Customers
```shell
curl "https://api.webconnex.com/v2/public/search/customers?product=redpodium.com&pretty=true" \
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
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/search/customers?product=redpodium.com", nil)

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
            url="https://api.webconnex.com/v2/public/search/customers",
            params={
                "product": "redpodium.com",
                "pretty": "true",
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
        path: '/v2/public/search/customers?product=redpodium.com',
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
        "pretty":"true",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/search/customers", method: .get, parameters: urlParams, headers: headers)
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
  "totalResults": 2
}
```

#### HTTP Request
`GET /v2/public/search/customers?product=`

#### Request Params
Parameter		             	                          |	Description
----------------------------------------------------|---------------------------
**product**<br>*string*<br>required                 | Name of the product you to search for customers on
**email**<br>*string*<br>(optional)                 | Billing email you want to search on
**sort**<br>*string*<br>(optional)                  |
**limit**<br>*string*<br>(optional)                 | limits the number of results returned
**greaterThanId**<br>*integer*<br>(optional)        | filter customers to only show results greater than provided id
**lessThanId**<br>*integer*<br>(optional)           | filter customers to only show results less than provided id
**startingAfter**<br>*integer*<br>(optional)        | filter customers to only show results with id's after value
**dateCreatedBefore**<br>*timestamp*<br>(optional)  | filter customers to only show results created before date
**dateCreatedAfter**<br>*timestamp*<br>(optional)   | filter customers to only show results created before date
**dateUpdatedBefore**<br>*timestamp*<br>(optional)  | filter customers to only show results updated before date
**dateUpdatedAfter**<br>*timestamp*<br>(optional)   | filter customers to only show results updated after date

#### Response Object
Attribute			                 |	Description
-------------------------------|-----------------------------------------------------
**id**<br>*integer* 			     | Unique id of the customer
**email**<br>*string*					 | Email of the associated customer
**billing**<br>*object*				 | Billing object containing name and address details associated with customer
**amount**<br>*float*					 | Total of customer transactions
**dateCreated**<br>*timestamp* | Date and time of the creation of the customer
**dateUpdated**<br>*timestamp* | Date and time the customer was last updated (optional)

### View Customers by Id
```shell
curl "https://api.webconnex.com/v2/public/search/customers/1155061?product=redpodium.com&pretty=true" \
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
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/search/customers/1155061?product=redpodium.com", nil)

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
            url="https://api.webconnex.com/v2/public/search/customers/1155061",
            params={
                "pretty": "true",
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
// request View
(function(callback) {
    'use strict';

    const httpTransport = require('https');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'api.webconnex.com',
        port: '443',
        path: '/v2/public/search/customers/1155061?product=redpodium.com',
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
        "pretty":"true",
        "product":"redpodium.com",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/search/customers/1155061", method: .get, parameters: urlParams, headers: headers)
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

#### HTTP Request
`GET /v2/public/search/customers/{id}?product=`

#### Request Params
Parameter			                      |	Description
------------------------------------|-------------------------------------------
**id**<br>*string*<br>required      | Id of the requested customer
**product**<br>*string*<br>required | Product to search against

#### Response Object
Parameter		   	                |	Description
--------------------------------|-----------------------------------------------
**id**<br>*integer*             | Unique id of the customer
**email**<br>*string*           | Email of the associated customer
**billing**<br>*object*         | Billing object containing name and address details associated with customer
**amount**<br>*float*           | Total of customer transactions
**dateCreated**<br>*timestamp*  | Date and time of the creation of the customer
**dateUpdated**<br>*timestamp*  | Date and time the customer was last updated (optional)
