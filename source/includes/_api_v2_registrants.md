## Registrants

### Search Registrants
```shell
curl "https://api.webconnex.com/v2/public/search/registrants?product=redpodium.com2&pretty=true" \
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
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/search/registrants?product=redpodium.com2", nil)

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
            url="https://api.webconnex.com/v2/public/search/registrants",
            params={
                "product": "redpodium.com2",
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
        path: '/v2/public/search/registrants?product=redpodium.com2',
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
        "product":"redpodium.com2",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/search/registrants", method: .get, parameters: urlParams, headers: headers)
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
      "displayId": "1111111111111111111",
      "customerId": 1,
      "customerEmail": "someone@test.com",
      "billing": {
        "firstName": "John",
        "lastName": "Doe",
        "address": {
          "city": "Sacramento",
          "country": "US",
          "postalCode": "111111",
          "state": "CA",
          "street1": "1233 SW Any St."
        }
      },
      "formId": 1,
      "formName": "test",
      "formAccRef": "TST12",
      "status": "3",
      "orderNumber": "TST12-001-4",
      "total": "40.00",
      "currency": "USD",
      "dateCreated": "2016-01-28T00:11:10Z",
      "dateUpdated": "2016-05-02T22:32:22Z"
    },
		{
      "id": 2,
      "displayId": "1111111111111111112",
      "customerId": 1,
      "customerEmail": "someone@test.com",
      "billing": {
        "firstName": "John",
        "lastName": "Doe",
        "address": {
          "city": "Sacramento",
          "country": "US",
          "postalCode": "111111",
          "state": "CA",
          "street1": "1233 SW Any St."
        }
      },
      "formId": 1,
      "formName": "test",
      "formAccRef": "TST12",
      "status": "3",
      "orderNumber": "TST12-001-4",
      "total": "40.00",
      "currency": "USD",
      "dateCreated": "2016-01-28T00:11:10Z",
      "dateUpdated": "2016-05-02T22:32:22Z"
    }
  ],
  "totalResults": 2
}
```
#### HTTP Request
`GET /v2/public/search/registrants?product=`

#### Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**product**<br>*string*<br>required               | Name of the product you to search for registrants against
**formId**<br>*integer*<br>(optional) 		          | Id of the form you want to filter registrants by
**status**<br>*string*<br>(optional) 				        | Status string of the order you want to filter on
**sort**<br>*string*<br>(optional) 			            |
**limit**<br>*string*<br>(optional) 				        | limits the number of results returned
**orderId**<br>*integer*<br>(optional) 		   	     	| filter registrants to only show results matching a provided order id
**orderDisplayId**<br>*string*<br>(optional) 		    | filter registrants to only show results matching a provided order display id
**greaterThanId**<br>*integer*<br>(optional) 		   	| filter registrants to only show results greater than provided id
**formId**<br>*integer*<br>(optional) 			       	| filter registrants to only show results matching the form id
**customerId**<br>*integer*<br>(optional) 				  | filter registrants to only show results matching the customer id
**orderEmail**<br>*string*<br>(optional) 				    | filter registrants to only show results matching the email
**orderNumber**<br>*string*<br>(optional) 				  | filter registrants to only show results matching the order number
**lessThanId**<br>*integer*<br>(optional) 		     	| filter registrants to only show results less than provided id
**startingAfter**<br>*integer*<br>(optional) 			  | filter registrants to only show results with id's after value
**dateCreatedBefore**<br>*timestamp*<br>(optional)  | filter registrants to only show results created before date
**dateCreatedAfter**<br>*timestamp*<br>(optional) 	| filter registrants to only show results created before date
**dateUpdatedBefore**<br>*timestamp*<br>(optional) 	| filter registrants to only show results updated before date
**dateUpdatedAfter**<br>*timestamp*<br>(optional) 	| filter registrants to only show results updated after date

#### Response Object
Attribute			                  |	Description
--------------------------------|-----------------------------------------------------
**id**<br>*integer* 				    | Unique id of the registrant
**displayId**<br>*string*				| Unique hash used as civilian facing id
**customerId**<br>*integer*			| Unique id of the associated customer
**customerEmail**<br>*string*		| Email of the associated customer
**billing**<br>*object*					| Billing object containing name and address details associated with order
**formId**<br>*integer*					| Id of the form that associated with the order
**formName**<br>*string*				| Name of the form that created order
**formAccRef**<br>*string*			| Accounting reference string of the form that created order
**status**<br>*string*					| Status of the registrant
**orderNumber**<br>*string* 		| Order number
**total**<br>*float*            | Total cost of the registrant
**dateCreated**<br>*timestamp*  | Date and time of the creation of the registrant
**dateUpdated**<br>*timestamp*  | Date and time the registrant was last updated ((optional))

### View Registrant by Id
```shell
curl "https://api.webconnex.com/v2/public/search/registrants/2233110?pretty=true&product=redpodium.com" \
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
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/search/registrants/2233110?product=redpodium.com", nil)

	// Headers
	req.Header.Add("apiKey", "<YOUR API KEY>")

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
            url="https://api.webconnex.com/v2/public/search/registrants/2233110",
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
        path: '/v2/public/search/registrants/2233110?product=redpodium.com',
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

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/search/registrants/2233110?product=redpodium.com", method: .get, headers: headers)
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
      "displayId": "1111111111111111111",
      "customerId": 1,
      "customerEmail": "someone@test.com",
      "billing": {
        "firstName": "John",
        "lastName": "Doe",
        "address": {
          "city": "Sacramento",
          "country": "US",
          "postalCode": "111111",
          "state": "CA",
          "street1": "1233 SW Any St."
        }
      },
      "formId": 1,
      "formName": "test",
      "formAccRef": "TST12",
      "status": "3",
      "orderNumber": "TST12-001-4",
      "total": "40.00",
      "currency": "USD",
      "dateCreated": "2016-01-28T00:11:10Z",
      "dateUpdated": "2016-05-02T22:32:22Z"
    }
  ]
}
```

#### HTTP Request
`GET /v2/public/search/registrants/{id}?product=`

#### Request Params
Parameter			                        |	Description
--------------------------------------|------------------------------------------
**id**<br>*string*<br>required 				| Id of the requested order
**product**<br>*string*<br>required   | Product to search against
**[]expand**<br>*string*<br>(optional)  | Return requested children (subscriptions)

#### Response Object
Attribute			                  |	Description
--------------------------------|-----------------------------------------------
**id**<br>*integer* 				    | Unique id of the registrant
**displayId**<br>*string*				| Unique hash used as civilian facing id
**customerId**<br>*integer*			| Unique id of the associated customer
**customerEmail**<br>*string*		| Email of the associated customer
**billing**<br>*object*					| Billing object containing name and address details associated with order
**formId**<br>*integer*					| Id of the form that associated with the order
**formName**<br>*string*				| Name of the form that created order
**formAccRef**<br>*string*      | Accounting reference string of the form that created order
**status**<br>*string*          | Status of the registrant
**orderNumber**<br>*string*     | Order number
**total**<br>*float*            | Total cost of the order
**dateCreated**<br>*timestamp*  | Date and time of the creation of the registrant
**dateUpdated**<br>*timestamp*  | Date and time the registrant was last updated ((optional))

### Check In by Id
```shell
curl -X "POST" "https://api.webconnex.com/v2/public/registrant/check-in?pretty=true" \
     -H "apiKey: <YOUR API KEY>" \
     -d $'{
            "id": 17492,
            "date": "2016-05-02T22:32:22Z"
          }'
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
	"strings"
)

func sendRequest() {
	body := strings.NewReader(`{
  "id": 17553,
  "date": "2016-05-02T22:32:22Z"
}`)

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("POST", "https://api.webconnex.com/v2/public/registrant/check-in", body)

	// Headers
	req.Header.Add("apiKey", "<YOUR API KEY>")
	req.Header.Add("Content-Type", "text/plain; charset=utf-8")

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
        response = requests.post(
            url="https://api.webconnex.com/v2/public/registrant/check-in",
            headers={
                "apiKey": "<YOUR API KEY>",
                "Content-Type": "text/plain; charset=utf-8",
            },
            data="{
                    \"id\": 17553,
                    \"date\": \"2016-05-02T22:32:22Z\"
                  }"
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
        path: '/v2/public/registrant/check-in',
        method: 'POST',
        headers: {"apiKey":"<YOUR API KEY>","Content-Type":"text/plain; charset=utf-8"}
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
    request.write("{\n  \"id\": 17553,\n  \"date\": \"2016-05-02T22:32:22Z\"\n}")
    request.end();

})((error, statusCode, headers, body) => {
    console.log('ERROR:', error);
    console.log('STATUS:', statusCode);
    console.log('HEADERS:', JSON.stringify(headers));
    console.log('BODY:', body);
});
```
```swift
func sendRequest() {
    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
        "Content-Type":"text/plain; charset=utf-8",
    ]

    // Custom Body Encoding
    struct RawDataEncoding: ParameterEncoding {
        public static var `default`: RawDataEncoding { return RawDataEncoding() }
        public func encode(_ urlRequest: URLRequestConvertible, with parameters: Parameters?) throws -> URLRequest {
            var request = try urlRequest.asURLRequest()
            request.httpBody = "{\n  \"id\": 17553,\n  \"date\": \"2016-05-02T22:32:22Z\"\n}".data(using: String.Encoding.utf8, allowLossyConversion: false)
            return request
        }
    }

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/registrant/check-in", method: .post, encoding: RawDataEncoding.default, headers: headers)
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
    "id": 17553,
    "date": "2017-08-24T00:00:00Z"
  },
  "totalResults": 1
}
```

#### HTTP Request
`GET /v2/public/registrant/check-in`

#### Request Params
Parameter			                          |	Description
----------------------------------------|----------------------------------------
**id**<br>*string*<br>required 				  | Id of the registrant
**date**<br>*timestamp*<br>required     | The timestamp to set as the checkin date

#### Response Object
Attribute			                  |	Description
--------------------------------|-----------------------------------------------
**id**<br>*integer* 				    | Unique id of the registrant checked in
**date**<br>*timestamp*			    | The timestamp set for checkin

### Check In by Display Id
```shell
curl -X "POST" "https://api.webconnex.com/v2/public/registrant/check-in?pretty=true" \
     -H "apiKey: <YOUR API KEY>" \
     -d $'{
            "displayId": 17492,
            "date": "2016-05-02T22:32:22Z"
          }'
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
	"strings"
)

func sendRequest() {
	body := strings.NewReader(`{
    "displayId": 17553,
    "date": "2016-05-02T22:32:22Z"
  }`)

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("POST", "https://api.webconnex.com/v2/public/registrant/check-in", body)

	// Headers
	req.Header.Add("apiKey", "<YOUR API KEY>")
	req.Header.Add("Content-Type", "text/plain; charset=utf-8")

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
        response = requests.post(
            url="https://api.webconnex.com/v2/public/registrant/check-in",
            headers={
                "apiKey": "<YOUR API KEY>",
                "Content-Type": "text/plain; charset=utf-8",
            },
            data="{
                    \"displayId\": 17553,
                    \"date\": \"2016-05-02T22:32:22Z\"
                  }"
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
        path: '/v2/public/registrant/check-in',
        method: 'POST',
        headers: {"apiKey":"<YOUR API KEY>","Content-Type":"text/plain; charset=utf-8"}
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
    request.write("{\n  \"displayId\": 17553,\n  \"date\": \"2016-05-02T22:32:22Z\"\n}")
    request.end();

})((error, statusCode, headers, body) => {
    console.log('ERROR:', error);
    console.log('STATUS:', statusCode);
    console.log('HEADERS:', JSON.stringify(headers));
    console.log('BODY:', body);
});
```
```swift
func sendRequest() {
    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
        "Content-Type":"text/plain; charset=utf-8",
    ]

    // Custom Body Encoding
    struct RawDataEncoding: ParameterEncoding {
        public static var `default`: RawDataEncoding { return RawDataEncoding() }
        public func encode(_ urlRequest: URLRequestConvertible, with parameters: Parameters?) throws -> URLRequest {
            var request = try urlRequest.asURLRequest()
            request.httpBody = "{\n  \"displayId\": 17553,\n  \"date\": \"2016-05-02T22:32:22Z\"\n}".data(using: String.Encoding.utf8, allowLossyConversion: false)
            return request
        }
    }

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/registrant/check-in", method: .post, encoding: RawDataEncoding.default, headers: headers)
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
    "displayId": 1480289239129099078,
    "date": "2017-08-24T00:00:00Z"
  },
  "totalResults": 1
}
```

#### HTTP Request
`GET /v2/public/registrant/check-in`

#### Request Params
Parameter			                          |	Description
----------------------------------------|----------------------------------------
**displayId**<br>*string*<br>required   | Display Id of the registrant
**date**<br>*timestamp*<br>required     | The timestamp to set as the checkin date

#### Response Object
Attribute			                  |	Description
--------------------------------|-----------------------------------------------
**displayId**<br>*string*				| Display Id of the registrant checked in
**date**<br>*timestamp*			    | The timestamp set for checkin

### Check Out by Id
```shell
curl -X "POST" "https://api.webconnex.com/v2/public/registrant/check-out?pretty=true" \
     -H "apiKey: <YOUR API KEY>" \
     -d $'{
            "id": 17492,
            "date": "2016-05-02T22:32:22Z"
          }'
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
	"strings"
)

func sendRequest() {
	body := strings.NewReader(`{
  "id": 17553,
  "date": "2016-05-02T22:32:22Z"
}`)

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("POST", "https://api.webconnex.com/v2/public/registrant/check-out", body)

	// Headers
	req.Header.Add("apiKey", "<YOUR API KEY>")
	req.Header.Add("Content-Type", "text/plain; charset=utf-8")

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
        response = requests.post(
            url="https://api.webconnex.com/v2/public/registrant/check-out",
            headers={
                "apiKey": "<YOUR API KEY>",
                "Content-Type": "text/plain; charset=utf-8",
            },
            data="{
                    \"id\": 17553,
                    \"date\": \"2016-05-02T22:32:22Z\"
                  }"
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
        path: '/v2/public/registrant/check-out',
        method: 'POST',
        headers: {"apiKey":"<YOUR API KEY>","Content-Type":"text/plain; charset=utf-8"}
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
    request.write("{\n  \"id\": 17553,\n  \"date\": \"2016-05-02T22:32:22Z\"\n}")
    request.end();

})((error, statusCode, headers, body) => {
    console.log('ERROR:', error);
    console.log('STATUS:', statusCode);
    console.log('HEADERS:', JSON.stringify(headers));
    console.log('BODY:', body);
});
```
```swift
func sendRequest() {
    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
        "Content-Type":"text/plain; charset=utf-8",
    ]

    // Custom Body Encoding
    struct RawDataEncoding: ParameterEncoding {
        public static var `default`: RawDataEncoding { return RawDataEncoding() }
        public func encode(_ urlRequest: URLRequestConvertible, with parameters: Parameters?) throws -> URLRequest {
            var request = try urlRequest.asURLRequest()
            request.httpBody = "{\n  \"id\": 17553,\n  \"date\": \"2016-05-02T22:32:22Z\"\n}".data(using: String.Encoding.utf8, allowLossyConversion: false)
            return request
        }
    }

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/registrant/check-out", method: .post, encoding: RawDataEncoding.default, headers: headers)
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
    "id": 17553,
    "date": "2017-08-24T00:00:00Z"
  },
  "totalResults": 1
}
```

#### HTTP Request
`GET /v2/public/registrant/check-out`

#### Request Params
Parameter			                          |	Description
----------------------------------------|----------------------------------------
**id**<br>*string*<br>required 				  | Id of the registrant
**date**<br>*timestamp*<br>required     | The timestamp to set as the checkout date


#### Response Object
Attribute			                  |	Description
--------------------------------|-----------------------------------------------
**id**<br>*integer* 				    | Unique id of the registrant checked out
**date**<br>*timestamp*			    | The timestamp set for checkout


### Check Out by Display Id
```shell
curl -X "POST" "https://api.webconnex.com/v2/public/registrant/check-out?pretty=true" \
     -H "apiKey: <YOUR API KEY>" \
     -d $'{
            "displayId": 17492,
            "date": "2016-05-02T22:32:22Z"
          }'
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
	"strings"
)

func sendRequest() {
	body := strings.NewReader(`{
    "displayId": 17553,
    "date": "2016-05-02T22:32:22Z"
  }`)

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("POST", "https://api.webconnex.com/v2/public/registrant/check-out", body)

	// Headers
	req.Header.Add("apiKey", "<YOUR API KEY>")
	req.Header.Add("Content-Type", "text/plain; charset=utf-8")

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
        response = requests.post(
            url="https://api.webconnex.com/v2/public/registrant/check-out",
            headers={
                "apiKey": "<YOUR API KEY>",
                "Content-Type": "text/plain; charset=utf-8",
            },
            data="{
                    \"displayId\": 17553,
                    \"date\": \"2016-05-02T22:32:22Z\"
                  }"
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
        path: '/v2/public/registrant/check-out',
        method: 'POST',
        headers: {"apiKey":"<YOUR API KEY>","Content-Type":"text/plain; charset=utf-8"}
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
    request.write("{\n  \"displayId\": 17553,\n  \"date\": \"2016-05-02T22:32:22Z\"\n}")
    request.end();

})((error, statusCode, headers, body) => {
    console.log('ERROR:', error);
    console.log('STATUS:', statusCode);
    console.log('HEADERS:', JSON.stringify(headers));
    console.log('BODY:', body);
});
```
```swift
func sendRequest() {
    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
        "Content-Type":"text/plain; charset=utf-8",
    ]

    // Custom Body Encoding
    struct RawDataEncoding: ParameterEncoding {
        public static var `default`: RawDataEncoding { return RawDataEncoding() }
        public func encode(_ urlRequest: URLRequestConvertible, with parameters: Parameters?) throws -> URLRequest {
            var request = try urlRequest.asURLRequest()
            request.httpBody = "{\n  \"displayId\": 17553,\n  \"date\": \"2016-05-02T22:32:22Z\"\n}".data(using: String.Encoding.utf8, allowLossyConversion: false)
            return request
        }
    }

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/registrant/check-out", method: .post, encoding: RawDataEncoding.default, headers: headers)
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
    "displayId": 1480289239129099078,
    "date": "2017-08-24T00:00:00Z"
  },
  "totalResults": 1
}
```

#### HTTP Request
`GET /v2/public/registrant/check-out`

#### Request Params
Parameter			                          |	Description
----------------------------------------|----------------------------------------
**displayId**<br>*string*<br>required   | Display Id of the registrant
**date**<br>*timestamp*<br>required     | The timestamp to set as the check out date


#### Response Object
Attribute			                  |	Description
--------------------------------|-----------------------------------------------
**displayId**<br>*string*				| Display Id of the registrant checked out
**date**<br>*timestamp*			    | The timestamp set for check out
