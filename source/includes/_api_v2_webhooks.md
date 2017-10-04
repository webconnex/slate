## Webhooks

### List
```shell
curl "https://api.webconnex.com/v2/public/webhooks?pretty=true" \
     -H "apiKey: <YOUR API KEY>"
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func sendList() {

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/webhooks", nil)

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
            url="https://api.webconnex.com/v2/public/webhooks",
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
        path: '/v2/public/webhooks',
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
func sendListRequest() {

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/webhooks", method: .get, headers: headers)
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
      "id": 28,
      "accountId": 1,
      "forms": [{
        "formId": -1
      }],
      "token": "b4148448406443eda7bc5c44d11c9cd3",
      "events": [
        "registration",
        "subscription"
      ],
      "method": "POST",
      "url": "https://webhook-endpoint.your-url.com",
      "typeId": 1,
      "status": 1,
      "meta": {
        "name": "Registration Capture"
      },
      "dateCreated": "2015-11-10T06:09:11Z",
      "dateUpdated": "2015-11-23T19:14:16Z"
    },
    {
      "id": 29,
      "accountId": 1,
      "forms": [{
        "formId": 376
      },{
        "formId": 19234
      }],
      "token": "64fca5a66a8945b3958905b320f72adb",
      "events": [
        "registration",
        "coupon"
      ],
      "method": "POST",
      "url": "https://webhook-endpoint.your-url.com",
      "typeId": 1,
      "status": 1,
      "meta": {
        "name": "Internal CRM integration"
      },
      "dateCreated": "2015-11-10T16:54:20Z",
      "dateUpdated": "2015-11-23T19:14:27Z"
    }
  ],
  "totalResults": 2
}
```
#### HTTP Request
`GET /v2/public/webhooks`

#### Request Params
No filtering implemented on this HTTP resource.

#### Response Object
Attribute			                    |	Description
----------------------------------|---------------------------------------------
**id**<br>*integer* 				      | Unique id of the webhook
**accountId**<br>*integer*				| Id of the associated account
**forms**<br>*array*              | Array of objects containing the form id's associated with the webhook.
**token**<br>*string*					    | Unique token for the webhook
**events**<br>*array*					    | List of events assigned to the webhook
**method**<br>*string*					  | HTTP method used for the webhook delivery request
**url**<br>*string*					      | Endpoint URL used for the webhook delivery request
**typeId**<br>*integer*					  | Webhook Type id (See appendix for types)
**status**<br>*string*					  | Status of the webhook (See appendix for statuses)
**meta**<br>*object*					    | Contains additional webhook information
**dateCreated**<br>*timestamp*    | Timestamp of the creation of the webhook
**dateUpdated**<br>*timestamp*    | Timestamp the webhook was last updated

### View
```shell
curl "https://api.webconnex.com/v2/public/webhooks/1623423?pretty=true" \
     -H "apiKey: <YOUR API KEY>"
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func sendList() {

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/webhooks/1623423", nil)

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
            url="https://api.webconnex.com/v2/public/webhooks/1623423",
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
        path: '/v2/public/webhooks/1623423',
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
func sendListRequest() {

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/webhooks/1623423", method: .get, headers: headers)
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
      "id": 28,
      "accountId": 1,
      "forms": [{
        "formId": 19234
      }],
      "token": "b4148448406443eda7bc5c44d11c9cd3",
      "events": [
        "registration"
      ],
      "method": "POST",
      "url": "https://webhook-endpoint.your-url.com",
      "typeId": 1,
      "status": 1,
      "meta": {
        "name": "Registration Capture"
      },
      "dateCreated": "2015-11-10T06:09:11Z",
      "dateUpdated": "2015-11-23T19:14:16Z"
    }],
  "totalResults": 1
}
```
#### HTTP Request
`GET /v2/public/webhooks/{id}`

#### Request Params
Parameter			                    |	Description
----------------------------------|---------------------------------------------------
**id**<br>*string*<br>(required)   | Id of the requested webhook

#### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique id of the webhook
**accountId**<br>*integer*  | Id of the associated account
**forms**<br>*array*				| Array of objects containing the form id's associated with the webhook.
**token**<br>*string*				| Unique token for the webhook
**events**<br>*array*				| List of events assigned to the webhook
**method**<br>*string*			| HTTP method used for the webhook delivery request
**url**<br>*string*					| Endpoint URL used for the webhook delivery request
**typeId**<br>*integer*			| Webhook Type id (See appendix for types)
**status**<br>*string*      | Status of the webhook (See appendix for statuses)
**meta**<br>*object*				| Contains additional webhook details
**dateCreated**<br>*timestamp* | Timestamp of the creation of the webhook
**dateUpdated**<br>*timestamp* | Timestamp the webhook was last updated

### Create
```shell

```
```go

```
```python

```
```javascript

```
```swift

```

> API returns JSON structured like this:

```json
{
	"responseCode": 200,
	"totalResults": 1
}
```
#### HTTP Request
`POST /v2/public/webhooks`

#### Request Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**forms**<br>*array*<br>Required					| Array of objects containing the form id's associated with the webhook. (send `[{"formid":-1}]` to subscribe to all forms)
**events**<br>*array*<br>Required					| List of events assigned to the webhook
**method**<br>*string*					| HTTP method used for the webhook delivery request
**url**<br>*string*					| Endpoint URL used for the webhook delivery request
**typeId**<br>*integer*					| Webhook Type id (See appendix for types)
**status**<br>*string*					| Status of the webhook (See appendix for statuses)
**meta**<br>*object*					| Contains webhook name and app key if required by the endpoint

#### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique id of the webhook
**accountId**<br>*integer*					| Id of the associated account
**forms**<br>*array*<br>Required					| Array of objects containing the form id's associated with the webhook.
**token**<br>*string*					| Unique token for the webhook
**events**<br>*array*					| List of events assigned to the webhook
**method**<br>*string*					| HTTP method used for the webhook delivery request
**url**<br>*string*					  | Endpoint URL used for the webhook delivery request
**typeId**<br>*integer*					| Webhook Type id (See appendix for types)
**status**<br>*string*					| Status of the webhook (See appendix for statuses)
**meta**<br>*object*					| Contains webhook name and app key if required by the endpoint
**dateCreated**<br>*timestamp* | Timestamp of the creation of the webhook
**dateUpdated**<br>*timestamp* | Timestamp the webhook was last updated

### Update
```shell

```
```go

```
```python

```
```javascript

```
```swift

```

> API returns JSON structured like this:

```json
{
	"responseCode": 200,
	"totalResults": 1
}
```

#### HTTP Request
`PUT /v2/public/webhooks/{id}`

#### Request Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique id of the webhook
**accountId**<br>*integer*					| Id of the associated account
**forms**<br>*array*<br>Required					| Array of objects containing the form id's associated with the webhook. (send `[{"formid":-1}]` to subscribe to all forms)
**events**<br>*array*<br>Required					| List of events assigned to the webhook
**method**<br>*string*					| HTTP method used for the webhook delivery request
**url**<br>*string*					| Endpoint URL used for the webhook delivery request
**typeId**<br>*integer*					| Webhook Type id (See appendix for types)
**status**<br>*string*					| Status of the webhook (See appendix for statuses)
**meta**<br>*object*					| Contains webhook name and app key if required by the endpoint

#### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Unique id of the webhook
**accountId**<br>*integer*					| Id of the associated account
**forms**<br>*array*<br>Required					| Array of objects containing the form id's associated with the webhook.
**token**<br>*string*					| Unique token for the webhook
**events**<br>*array*					| List of events assigned to the webhook
**method**<br>*string*					| HTTP method used for the webhook delivery request
**url**<br>*string*					| Endpoint URL used for the webhook delivery request
**typeId**<br>*integer*					| Webhook Type id (See appendix for types)
**status**<br>*string*					| Status of the webhook (See appendix for statuses)
**meta**<br>*object*					| Contains webhook name and app key if required by the endpoint
**dateCreated**<br>*timestamp* | Timestamp of the creation of the webhook
**dateUpdated**<br>*timestamp* | Timestamp the webhook was last updated

### Delete
```shell
curl -X "DELETE" "https://api.webconnex.com/v2/public/webhooks/4" \
     -H "apiKey: <YOUR API KEY>"
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func delete() {

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("DELETE", "https://api.webconnex.com/v2/public/webhooks/4", nil)

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
        response = requests.delete(
            url="https://api.webconnex.com/v2/public/webhooks/4",
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
        path: '/v2/public/webhooks/4',
        method: 'DELETE',
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
func sendDeleteRequest() {

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/webhooks/4", method: .delete, headers: headers)
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
	"totalResults": 1
}
```
#### HTTP Request
`DELETE /v2/public/webhooks/{id}`

#### Request Object
Attribute			      |	Description
--------------------|-----------------------------------------------------------------
**id**<br>*integer* | Id of the webhook

### List Logs
```shell
curl "https://api.webconnex.com/v2/public/webhooks/1623423/logs?pretty=true" \
     -H "apiKey: <YOUR API KEY>"
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func list() {

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/webhooks/1623423/logs", nil)

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
            url="https://api.webconnex.com/v2/public/webhooks/1623423/logs",
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
        path: '/v2/public/webhooks/1623423/logs',
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
func sendListRequest() {

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/webhooks/1623423/logs", method: .get, headers: headers)
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
      "id": 12128,
      "displayId": "7a2eb39d6dd04681ba5112da6446d0c7",
      "formId": 1,
      "webhookId": 46,
      "eventType": "publish",
      "eventId": 1234,
      "status": "error",
      "attempt": 1,
      "dateSent": "2016-09-15T23:30:04Z"
    },
    {
      "id": 12127,
      "displayId": "a9b9e3409e724ae39e939ef42b073fa4",
      "formId": 1,
      "webhookId": 46,
      "eventType": "subscription",
      "eventId": 1234,
      "status": "error",
      "attempt": 1,
      "dateSent": "2016-09-15T23:30:02Z"
    },
    {
      "id": 12125,
      "displayId": "4dceacfe166c4ea2abed0402f23a1e7c",
      "formId": 1,
      "webhookId": 46,
      "eventType": "registration",
      "eventId": 1234,
      "status": "error",
      "attempt": 1,
      "dateSent": "2016-09-15T23:29:59Z"
    },
    {
      "id": 12124,
      "displayId": "3c4f25cee893486182c211deefa33cbd",
      "formId": 1,
      "webhookId": 46,
      "eventType": "ping",
      "eventId": 1234,
      "status": "error",
      "attempt": 1,
      "dateSent": "2016-09-15T23:29:56Z"
    },
    {
      "id": 9849,
      "displayId": "5fe153f9533d4731893ef571676e5f90",
      "formId": 14280,
      "webhookId": 46,
      "eventType": "publish",
      "eventId": 8736,
      "status": "success",
      "attempt": 1,
      "dateSent": "2016-08-31T17:03:47Z"
    }
  ],
  "totalResults": 333,
  "startingAfter": 4,
  "hasMore": true
}
```

Get all logs for a given webhook

#### HTTP Request
`GET /v2/public/webhooks/{id}/logs`

#### Request Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 				| Id of the parent webhook

#### Request Params
Parameter		             	                          |	Description
----------------------------------------------------|---------------------------
**sort**<br>*string*<br>(optional)                  |
**limit**<br>*string*<br>(optional)                 | Limits the number of results returned
**greaterThanId**<br>*integer*<br>(optional)        |
**lessThanId**<br>*integer*<br>(optional)           |
**status**<br>*string*<br>(optional)                |
**dateSentBefore**<br>*timestamp*<br>(optional)     |
**dateSentAfter**<br>*timestamp*<br>(optional)      |

### View Webhook Log by Id
```shell
curl "https://api.webconnex.com/v2/public/webhooks/1623423/logs?pretty=true" \
     -H "apiKey: <YOUR API KEY>"
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func sendList() {

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/webhooks/46/logs/9849", nil)

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
            url="https://api.webconnex.com/v2/public/webhooks/46/logs/9849",
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
        path: '/v2/public/webhooks/46/logs/9849',
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
func sendListRequest() {

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/webhooks/46/logs/9849/", method: .get, headers: headers)
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
		"id": 9849,
		"displayId": "5fe153f9533d4731893ef571676e5f90",
		"webhookId": 46,
		"status": "success",
		"attempt": 1,
		"request": {
			"method": "POST",
			"url": "https://hooks.localhost.com/hooks/catch/1578515/4nr6xi/",
			"header": {
				"Content-Type": ["application/json"],
				"User-Agent": ["Webconnex-Divvy"],
				"X-Webconnex-Delivery": ["d44bf23f171f44958434b09eed2eaab4"],
				"X-Webconnex-Event": ["publish"],
				"X-Webconnex-Signature": ["42cf9e2bdf38df608e09f805a8a1254e372ad3139bd4c7a76982fa0286613062"]
			},
			"body": {
				"eventType": "publish",
				"accountId": 14,
				"formId": 14280,
				"data": {
					"accRef": "MMBRSHPTST",
					"currency": "USD",
					"datePublished": "2016-08-31T17:03:08Z",
					"eventStart": "2016-05-31T07:00:00Z",
					"id": 14280,
					"name": "Membership Example",
					"product": "regfox.com",
					"publishedPath": "awesomeco.regfox.com/membership-test-ek",
					"status": "open",
					"timeZone": "America/Regina"
				},
				"meta": {
					"name": "Webhook divvy example"
				}
			}
		},
		"response": {
			"code": 200,
			"header": {
				"Access-Control-Allow-Origin": ["*"],
				"Connection": ["keep-alive"],
				"Content-Length": ["152"],
				"Content-Type": ["application/json"],
				"Date": ["Wed, 31 Aug 2016 17:03:47 GMT"],
				"Response-Id": ["eW7TQDb9trUnoRgA"],
				"Server": ["nginx"],
			},
			"body": "{\"status\": \"success\", \"attempt\": \"57c70df3-d5e5-436f-aa27-e9c958aaf250\", \"id\": \"db89d766-5be4-4ba2-b312-5d7b5a23de7e\", \"request_id\": \"eW7TQDb9trUnoRgA\"}"
		},
		"dateSent": "2016-08-31T17:03:47Z"
	},
	"totalResults": 1
}
```

View a specific webhook log

#### HTTP Request
`GET /v2/public/webhooks/{webhookid}/logs/{webhookLogid}`

#### Request Object
Attribute			                    |	Description
----------------------------------|---------------------------------------------------
**webhookid**<br>*integer* 				| Id of the parent webhook
**webhookLogid**<br>*integer* 		| Id of the webhook log

### Resend Webhook
```shell
curl -X "POST" "https://api.webconnex.com/v2/public/webhooks/39/resend/3899" \
     -H "apiKey: <YOUR API KEY>"
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func sendRequest() {

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("POST", "https://api.webconnex.com/v2/public/webhooks/39/resend/3899", nil)

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
        response = requests.post(
            url="https://api.webconnex.com/v2/public/webhooks/39/resend/3899",
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
        path: '/v2/public/webhooks/39/resend/3899',
        method: 'POST',
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
func sendRequest() {

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/webhooks/39/resend/3899", method: .post, headers: headers)
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
		"accountId": 1,
		"formId": 403,
		"logEntryId": null,
		"webhookId": 112,
		"webhookToken": "6aeeff5d8ad94c71b3b716fcfe0aa9ad",
		"eventType": "subscription",
		"eventId": 15128,
		"url": "https://myawesome.api/v2",
		"typeId": 6,
		"method": "POST",
		"hash": "8de2ee5d255149c6af2ed5ffbf24dd7f",
		"body": {
			"eventType": "subscription",
			"accountId": 1,
			"formId": 403,
			"eventId": 15128,
			"data": {
        "billing": {
          "address": {
            "city": "Sacramento",
            "country": "US",
            "postalCode": "95814",
            "state": "CA",
            "street1": "455 Capital Mall"
          },
          "card": {
            "cardNumber": "VISA-1111",
            "expMonth": 9,
            "expYear": 2022
          },
          "check": {
            "accountType": "Bank Name",
            "accountNumber": "4111",
            "routingNumber": "123456789"
          },
          "email": "help@webconnex.com",
          "name": {
            "first": "John",
            "last": "Doe"
          },
          "paymentMethod": "card"
        },
				"currency": "USD",
				"customerId": 1179,
				"deductibleTotal": 20.6,
				"id": "01BPYMJZHFJF34CZJJR",
				"lookupId": 12949,
				"orderNumber": "SDD2-001000T",
				"orderStatus": "completed",
				"subscription": {
					"amount": 20.6,
					"category": "General",
					"dateCreated": "2017-03-16T21:05:08Z",
					"dateLast": "2017-07-06T00:00:39Z",
					"dateNext": "2017-07-13T10:00:00Z",
					"dateUpdated": "2017-07-06T00:00:38Z",
					"email": "test@webconnex.com",
					"id": 472,
					"paymentsLeft": -1,
					"paymentsLeftString": "unlimited",
					"schedule": "0 0 0 * * 4",
					"scheduleString": "Thursdays",
					"status": "active"
				},
				"total": 20.6,
				"transactionReference": "TESTERCHARGE"
			},
			"meta": {
				"appKey": "webconnex",
				"appToken": "webconnex"
			}
		},
		"Attempt": 2
	},
	"totalResults": 1
}
```

Request that a particular webhook attempt be resent.

#### HTTP Request
`POST /v2/public/webhooks/{webhookid}/resend/{logId}`

#### Request Params
Parameter			                      |	Description
------------------------------------|-------------------------------------------
**webhookid**<br>*string*<br>(required)			| Id of the webhook
**logId**<br>*string*<br>(required)	| Id of the webhook log entry to be resent
