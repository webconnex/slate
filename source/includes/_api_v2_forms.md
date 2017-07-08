## Form

### List all Forms
```shell
curl -X "POST" "https://api.webconnex.com/v1/public/forms" \
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
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/forms?product=redpodium.com", nil)

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
            url="https://api.webconnex.com/v2/public/forms",
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
         path: '/v2/public/forms?product=redpodium.com&pretty=true',
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

     // Add URL parameters
     let urlParams = [
         "product":"redpodium.com",
         "pretty":"true",
     ]

     // Fetch Request
     Alamofire.request("https://api.webconnex.com/v2/public/forms", method: .get, parameters: urlParams, headers: headers)
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
      "id": 1203002,
      "name": "Form Number 1",
      "product": "ticketspice.com",
      "status": "open",
      "dateCreated": "2016-04-07T01:09:58Z",
      "dateUpdated": "2016-04-07T01:10:01Z"
    },
    {
      "id": 1203002,
      "name": "Form Number 2",
      "product": "ticketspice.com",
      "status": "closed",
      "dateCreated": "2016-04-07T01:09:40Z",
      "dateUpdated": "2016-04-07T01:09:43Z"
    }
	]
}
```

#### HTTP Request
`GET /v2/public/forms`

#### Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**product**<br>*string*<br>Optional 		| Name of the product you want to list forms for
**[]expand**<br>*string*<br>Optional 		| pass inventory to see form inventory

#### Response Object
Attribute			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*integer* 			   	| Unique ID of the
**name**<br>*string*					| Name of the form
**status**<br>*string*				| Status of the form
**dateCreated**<br>*timestamp* | Date and time of the creation of the form
**dateUpdated**<br>*timestamp* | Date and time the form was last updated (optional)

### Get Form By ID
```shell
curl -X "PUT" "https://api.webconnex.com/v2/public/forms/15689" \
     -H "apiKey: <YOUR API KEY>"
```

```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func sendView() {

	// Create client
	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/forms/?%5B%5Dexpand=inventory", nil)

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
            url="https://api.webconnex.com/v2/public/forms/",
            params={
                "[]expand": "inventory",
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
        path: '/v2/public/forms/47520?%5B%5Dexpand=inventory',
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
func sendViewRequest() {
    /**
     View
     get https://api.webconnex.com/v2/public/forms/
     */

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Add URL parameters
    let urlParams = [
        "pretty":"true",
        "[]expand":"inventory",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/forms/", method: .get, parameters: urlParams, headers: headers)
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
    "id": 1,
    "name": "Donation Form",
    "product": "givingfuel.com",
    "accRef": "DNTFORM",
    "fields": {
      "type": "form",
      "triggers": [],
      "header": {
        "type": "header",
        "key": "header"
      },
      "registrants": {
        "type": "registrants",
        "key": "registrants"
      },
      "billing": {
        "type": "billing",
        "key": "billing",
        "header": {},
        "name": {
          "type": "name",
          "key": "name",
          "attributes": {},
          "firstName": {},
          "lastName": {},
          "mi": {}
        },
        "address": {
          "type": "address",
          "key": "address",
          "attributes": {},
          "street1": {},
          "street2": {},
          "city": {},
          "state": {},
          "postalCode": {},
          "country": {}
        },
        "paymentMethod": {
          "type": "paymentMethod",
          "key": "paymentMethod",
          "attributes": {},
          "card": {},
          "check": {},
          "offline": {}
        },
        "card": {
          "type": "creditCard",
          "key": "card",
          "cardNumber": {},
          "expMonth": {},
          "expYear": {},
          "cvvCode": {}
        },
        "check": {
          "type": "check",
          "key": "check",

          "bankName": {},
          "accountType": {
            "type": "accountType",
            "key": "accountType",
            "checking": {},
            "savings": {}
          },
          "routingNumber": {
            "type": "routingNumber",
            "key": "routingNumber"
          },
          "accountNumber": {
            "type": "accountNumber",
            "key": "accountNumber"
					}
        },
        "email": {
          "type": "email",
          "key": "email"
        }
      },
      "submit": {},
      "footer": {}
    },
    "status": "open",
    "currency": "USD",
    "timeZone": "America/Los_Angeles",
    "dateCreated": "2016-01-28T00:11:10Z",
  },
  "totalResults": 1
}
```

#### HTTP Request
`GET /v2/public/forms/{id}`

#### Request Params
Parameter			|	Description
--------------|----------------------------------------------------------------------
**id**<br>*Integer*<br>Required 				| ID of the form that is being requested

#### Response Object
Attribute												|	Description
--------------------------------|----------------------------------------------------
**id**<br>*Integer* 						| Unique ID of the
**name**<br>*string*						| Name of the form
**status**<br>*string*					| Status of the form
**accRef**<br>*string*					| Accounting Reference
**fields**<br>*object*		      | A collection of fields that make up the form
**timeZone**<br>*string*			 | Timezone code for the form
**dateCreated**<br>*timestamp* | Date and time of the creation of the form
**dateUpdated**<br>*timestamp* | Date and time the form was last updated (optional)

#### Fields Object
Attribute												|	Description
--------------------------------|----------------------------------------------------
**type**<br>*string* 						| The root of the fields is always set to type form
**attributes**<br>*object*			| Key/Value attributes related to the field set
**triggers**<br>*object*				| A collection of actions/conditions to provide logic to the form
**header**<br>*object*<br>required			| Fields in set in the header. Always present on the form (Display only fields).
**registrants**<br>*object*<br>required					| Main data collection fields. Repeated for each registrant when using "multireg" forms. (registrants.attributes.multireg === true)
**billing**<br>*object*<br>required					| Billing fields for the form. Not used if the billing is disabled on the form.
**footer**<br>*object*<br>required | Fields in set in the footer. Always present on the form (Display only fields).
