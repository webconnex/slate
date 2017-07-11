## Inventory

### View for Form
```shell
curl "https://api.webconnex.com/v2/public/forms/676/inventory?pretty=true" \
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
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/forms/676/inventory", nil)

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
```javascript
(function(callback) {
    'use strict';

    const httpTransport = require('https');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'api.webconnex.com',
        port: '443',
        path: '/v2/public/forms/676/inventory',
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
            url="https://api.webconnex.com/v2/public/forms/676/inventory",
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
func sendViewRequest() {

    // Add Headers
    let headers = [
        "apiKey":"<YOUR API KEY>",
    ]

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/forms/676/inventory", method: .get, headers: headers)
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
      "path": "registrants.registrationOptions",
      "name": "Registration Options",
      "sold": 8,
      "quantity": 12,
      "dateCreated": "2017-07-11T22:20:44Z"
    },
    {
      "path": "registrants.registrationOptions",
      "name": "Registration Options-registrants.registrationOptions",
      "key": "registrants.registrationOptions",
      "sold": 3,
      "quantity": 12,
      "dateCreated": "2017-07-11T22:20:44Z",
      "dateUpdated": "2017-07-12T08:06:24Z"
    }
  ],
  "totalResults": 2
}
```

#### HTTP Request
`GET /v2/public/forms/{formId}/inventory`

#### Request Params
Parameter			                          |	Description
----------------------------------------|----------------------------------------
**formId**<br>*integer*<br>required   	| The id of the parent form

#### Response Object
Attribute			                  |	Description
--------------------------------|-----------------------------------------------------
**path**<br>*string* 				    | Unique path scoped to a form
**name**<br>*string*            | Friendly public facing name of item
**sold**<br>*integer*					  | Quantity of sold inventory
**quantity**<br>*integer*				| Quantity of available inventory
**dateCreated**<br>*timestamp*  | Timestamp the inventory item was created
**dateUpdated**<br>*timestamp*  | Timestamp the inventory item was created
