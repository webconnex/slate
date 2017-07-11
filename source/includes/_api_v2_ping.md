## Ping/Healthcheck
```shell
curl -X "GET" "http://api.webconnex.com/v2/public/ping?pretty=true" \
	-H "apiKey: <YOUR API KEY>"
```
```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func request() {

	client := &http.Client{}

	// Create request
	req, err := http.NewRequest("GET", "http://api.webconnex.com/v2/public/ping", nil)

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

    const httpTransport = require('http');
    const responseEncoding = 'utf8';
    const httpOptions = {
        hostname: 'api.webconnex.com',
        port: '80',
        path: '/v2/public/ping',
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
func Request() {
    /**
     Ping
     get https://api.webconnex.com/v2/public/ping
     */

    // Fetch Request
    Alamofire.request("https://api.webconnex.com/v2/public/ping", method: .get)
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

```python
# Install the Python Requests library:
# `pip install requests`

import requests

def send_request():
    try:
        response = requests.get(
            url="http://api.webconnex.com/v2/public/ping",
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
> API returns JSON structured like this:

```json
{
  "responseCode": 200,
  "data": "Some nights I always win, I always win..."
}
```
Simple endpoint to provide a health check endpoint to make sure we are alive and kickin'.

#### HTTP Request
`GET /v2/public/ping`

Attribute											|	Description
------------------------------|----------------------------
**responseCode**<br>*Integer*	| Response code of the request
**data**<br>*string*					| Random string to use as data payload
