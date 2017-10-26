### Coupons

#### List Global coupons

```shell
curl "https://api.webconnex.com/v2/public/coupons/global?pretty=true" \
     -H "apiKey: <YOUR API KEY>"
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func requescoupon() {

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/coupons/global", nil)

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

```javascript
(function(callback) {
    'use strict';

    const httpTransport = require('http');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'api.webconnex.com',
        port: '80',
        path: '/v2/public/coupons/global',
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

```python
# Install the Python Requests library:
# `pip install requests`

import requests

def send_request():
    try:
        response = requests.get(
            url="https://api.webconnex.com/v2/public/coupons/global",
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

```swift
func couponRequest() {

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Add URL parameters
    let urlParams = [
        "product":"redpodium.com",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/coupons/global", method: .get, parameters: urlParams, headers: headers)
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

##### HTTP Request
`GET /v2/public/coupons/global`

##### Request Params
Parameter			                      |	Description
------------------------------------|----------------------------------
**Product**<br>*string*<br>(required)| Name of the product you to search for coupons on
**sort**<br>*string*<br>(optional)                  |
**limit**<br>*string*<br>(optional)                 | Limits the number of results returned
**greaterThanId**<br>*integer*<br>(optional)          |
**lessThanId**<br>*integer*<br>(optional)             |
**dateExpiresBefore**<br>*timestamp*<br>(optional)    |
**dateExpiresAfter**<br>*timestamp*<br>(optional)     |
**redeemedGreaterThan**<br>*integer*<br>(optional)    |
**lessThanRedeemed**<br>*integer*<br>(optional)       |
**greaterThanAvailable**<br>*integer*<br>(optional)   |
**lessThanAvailable**<br>*integer*<br>(optional)      |
**code**<br>*string*<br>(optional)                    |

##### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				    | Unique id of the coupon
**name**<br>*string*					  | The name of the coupon
**redeemed**<br>*integer*				| Number of coupons redeemed
**available**<br>*integer*      | Number of coupons available ([-1] means unlimited)
**currency**<br>*string*        | Currency of the coupon
**discounts**<br>*array*        | Discount associated with coupon
**codes**<br>*array*            | Codes associated with coupon
**dateCreated**<br>*timestamp*  | Timestamp of the creation of the order
**dateUpdated**<br>*timestamp*  | Timestamp the order was last updated (optional)

#### List Form Coupons

```shell
curl "https://api.webconnex.com/v2/public/coupons/forms/28609?pretty=true" \
     -H "apiKey: <YOUR API KEY>"
```

```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func sendListByForm() {

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/coupons/forms/28609", nil)

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

```javascript
// request List By Form
(function(callback) {
    'use strict';

    const httpTransport = require('https');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'api.webconnex.com',
        port: '443',
        path: '/v2/public/coupons/forms/28609',
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

```python
# Install the Python Requests library:
# `pip install requests`

import requests

def send_request():
    try:
        response = requests.get(
            url="https://api.webconnex.com/v2/public/coupons/forms/28609",
            params={
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

```swift
func sendListByFormRequest() {
    /**
     List By Form
     get https://api.webconnex.com/v2/public/coupons/forms/28609
     */

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Add URL parameters
    let urlParams = [
        "pretty":"true",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/coupons/forms/28609", method: .get, parameters: urlParams, headers: headers)
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

##### HTTP Request

`GET /v2/public/coupons/forms/{formId}`

##### Request Params
Parameter			                  |	Description
--------------------------------|-----------------------------------------------
**id**<br>*integer*<br>(required)| Form id to list coupons associated with

##### Response Object
Attribute			                  |	Description
--------------------------------|-----------------------------------------------
**id**<br>*integer* 				    | Unique id of the coupon
**name**<br>*string*					  | The name of the coupon
**redeemed**<br>*integer*				| Number of coupons redeemed
**available**<br>*integer*      | Number of coupons available ([-1] means unlimited)
**currency**<br>*string*        | Currency of the coupon
**discounts**<br>*array*				| Discount associated with coupon
**codes**<br>*array*				    | Codes associated with coupon
**dateCreated**<br>*timestamp*  | Timestamp of the creation of the order
**dateUpdated**<br>*timestamp*  | Timestamp the order was last updated (optional)

#### View Coupon by Id

```shell
### View Single
curl "https://api.webconnex.com/v2/public/coupons/1250?pretty=true" \
     -H "apiKey: <YOUR API KEY>"
```

```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func viewSingle() {
	// View Single (GET https://api.webconnex.com/v2/public/coupons/1250)

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/coupons/1250", nil)

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

```javascript
// request View Single
(function(callback) {
    'use strict';

    const httpTransport = require('https');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'api.webconnex.com',
        port: '443',
        path: '/v2/public/coupons/1250',
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

```python
# Install the Python Requests library:
# `pip install requests`

import requests


def send_request():
    # View Single
    # GET https://api.webconnex.com/v2/public/coupons/1250

    try:
        response = requests.get(
            url="https://api.webconnex.com/v2/public/coupons/1250",
            params={
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

```swift
func viewSingleRequest() {
    /**
     View Single
     get https://api.webconnex.com/v2/public/coupons/1250
     */

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Add URL parameters
    let urlParams = [
        "pretty":"true",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/coupons/1250", method: .get, parameters: urlParams, headers: headers)
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

##### HTTP Request
`GET /v2/public/coupons/{id}`

##### Request Params
Parameter			                  |	Description
--------------------------------|-----------------------------------------------
**id**<br>*integer*<br>(required)| Id of the requested coupon

##### Response Object
Attribute			                  |	Description
--------------------------------|-----------------------------------------------
**id**<br>*integer* 				    | Unique id of the coupon
**name**<br>*string*					  | The name of the coupon
**redeemed**<br>*integer*				| Number of coupons redeemed
**available**<br>*integer*      | Number of coupons available (-1 means unlimited)
**currency**<br>*string*        | Currency of the coupon
**discounts**<br>*array*				| Discount associated with coupon
**codes**<br>*array*					  | Codes associated with coupon
**dateCreated**<br>*timestamp*  | Timestamp of the creation of the order
**dateUpdated**<br>*timestamp*  | Timestamp the order was last updated (optional)
