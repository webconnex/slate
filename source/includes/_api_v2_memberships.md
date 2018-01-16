### Memberships

#### Search Memberships
```shell
curl "https://api.webconnex.com/v2/public/search/memberships?product=regfox.com&pretty=true" \
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
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/search/memberships?product=regfox.com", nil)

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
            url="https://api.webconnex.com/v2/public/search/memberships",
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
        path: '/v2/public/search/memberships?product=regfox.com',
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
    Alamofire.request("https://api.webconnex.com/v2/public/search/memberships", method: .get, parameters: urlParams, headers: headers)
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
      "id": 3000018,
      "memberId": "3000000938781",
      "customerId": 3000000,
      "registrantId": 3000230,
      "email": "lindsay@webconnex.com",
      "fee": 10,
      "expirationDate": "2019-02-12T00:00:00Z",
      "autoRenew": true,
      "status": "active",
      "dateCreated": "2017-08-02T01:13:39Z",
      "firstName": "Lindsay",
      "lastName": "Bluth",
      "levelId": 3000004,
      "levelHash": "1476292756717792168",
      "levelName": "Gold",
      "levelFee": 100,
      "levelExpirationType": "fixed date",
      "levelExpirationSchedule": "0 0 0 12 2 *",
      "levelNextRenewalDate": "2019-02-12T00:00:00Z",
      "levelAllowAutoRenew": true,
      "levelActive": true,
      "paymentMethod": "card",
      "paymentMask": "VISA-1111"
    },
    {
      "id": 3000016,
      "memberId": "3000000375348",
      "importedMemberId": "A23FHE",
      "customerId": 3000003,
      "registrantId": 3000149,
      "email": "maeby@webconnex.com",
      "fee": 10,
      "expirationDate": "2019-02-12T08:00:00Z",
      "autoRenew": true,
      "status": "active",
      "dateCreated": "2018-01-10T00:49:56Z",
      "dateUpdated": "2018-01-15T18:04:00Z",
      "firstName": "Maeby",
      "lastName": "Fünke",
      "levelId": 3000003,
      "levelHash": "42987290842374892364",
      "levelName": "Silver",
      "levelFee": 10,
      "levelExpirationType": "anniversary quarterly",
      "levelNextRenewalDate": "2020-06-01T00:00:00Z",
      "levelAllowAutoRenew": true,
      "levelActive": true,
      "paymentMethod": "card",
      "paymentMask": "VISA-1111"
    }
  ],
  "totalResults": 2,
}
```
##### HTTP Request
`GET /v2/public/search/memberships?product=`

##### Request Params
Parameter			                                      |	Description
----------------------------------------------------|---------------------------------
**product**<br>*string*<br>(required)		            | Name of the product you to search for memberships on
**formId**<br>*integer*<br>(optional) 		          | Id of the form you want to filter memberships by
**status**<br>*string*<br>(optional) 				        | Status string of the order you want to filter on
**sort**<br>*string*<br>(optional) 			          	|
**limit**<br>*string*<br>(optional) 				        | Limits the number of results returned
**greaterThanId**<br>*integer*<br>(optional) 		 		| Filter memberships to only show results greater than provided id
**registrantId**<br>*integer*<br>(optional) 			       	| Filter memberships to only show results matching the registrant id
**customerId**<br>*integer*<br>(optional) 				  | Filter memberships to only show results matching the customer id
**email**<br>*string*<br>(optional) 				    | Filter memberships to only show results matching the email
**lessThanId**<br>*integer*<br>(optional) 		     	| Filter memberships to only show results less than provided id
**startingAfter**<br>*integer*<br>(optional) 			  | Filter memberships to only show results with id's after value
**dateCreatedBefore**<br>*timestamp*<br>(optional)  | Filter memberships to only show results created before date
**dateCreatedAfter**<br>*timestamp*<br>(optional) 	| Filter memberships to only show results created before date
**dateUpdatedBefore**<br>*timestamp*<br>(optional) 	| Filter memberships to only show results updated before date
**dateUpdatedAfter**<br>*timestamp*<br>(optional) 	| Filter memberships to only show results updated after date

<!-- TODO -->
<!-- level, status, etc... -->

##### Response Object
Attribute			                 |	Description
-------------------------------|------------------------------------------------------
<!-- **id**<br>*integer* 				    | Unique id of the membership
**displayId**<br>*string*		   	| Unique hash used as civilian facing id
**customerId**<br>*integer*			| Unique id of the associated customer
**billing**<br>*object*					| Billing object containing name and address details associated with order
**formId**<br>*integer*					| Id of the form that associated with the order
**formName**<br>*string*				| Name of the form that created membership
**formAccRef**<br>*string*			| Accounting reference string of the form that created membership
**fieldData**<br>*object*	  		|
**status**<br>*string*					| Status of the membership
**orderId**<br>*integer*				| Unique id of the order
**orderDisplayId**<br>*string*	| Unique hash used as civilian facing id
**orderNumber**<br>*string*			| Order number
**orderEmail**<br>*string*			| Email of the associated order
**total**<br>*float*				    | Total cost of the membership
**fee**<br>*float*				      | Membership Fee
**amount**<br>*float*				    | Membership Amount
**levelLabel**<br>*string*			|
**levelKey**<br>*string*			  |
**eventDate**<br>*timestamp*    |
**dateCreated**<br>*timestamp*  | Timestamp of the creation of the membership
**dateUpdated**<br>*timestamp*  | Timestamp the membership was last updated (optional) -->

#### View Membership by Id
```shell
curl "https://api.webconnex.com/v2/public/search/memberships/2233110?pretty=true&product=regfox.com" \
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
	req, err := http.NewRequest("GET", "https://api.webconnex.com/v2/public/search/memberships/2233110?product=regfox.com", nil)

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
            url="https://api.webconnex.com/v2/public/search/memberships/810343",
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
        path: '/v2/public/search/memberships/810343?product=regfox.com',
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
    Alamofire.request("https://api.webconnex.com/v2/public/search/memberships/810343", method: .get, parameters: urlParams, headers: headers)
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
      "id": 3000018,
      "memberId": "2000934381",
      "importedMemberId": "abc123",
      "customerId": 3000000,
      "registrantId": 3000230,
      "email": "tobias@webconnex.com",
      "fee": 10,
      "expirationDate": "2015-02-12T00:00:00Z",
      "autoRenew": true,
      "status": "inactive",
      "dateCreated": "2017-08-02T01:13:39Z",
      "firstName": "Tobias",
      "lastName": "Fünke",
      "levelId": 3000004,
      "levelHash": "1476292756717792168",
      "levelName": "Bronze",
      "levelFee": 100,
      "levelExpirationType": "yearly",
      "levelNextRenewalDate": "2021-09-20T00:00:00Z",
      "levelAllowAutoRenew": true,
      "levelActive": true,
      "paymentMethod": "card",
      "paymentMask": "VISA-1111"
    }
  ]
}
```

##### HTTP Request
`GET /v2/public/search/memberships/{id}`

##### Request Params
Parameter			                    |	Description
----------------------------------|---------------------------------------------------
**id**<br>*string*<br>(required)  | Id of the requested order

##### URI Params
Parameter			                        |	Description
--------------------------------------|-----------------------------------------------
**product**<br>*string*<br>(required) | Product to search against

##### Response Object
Attribute			                  |	Description
--------------------------------|-----------------------------------------------------
<!-- **id**<br>*integer* 				    | Unique id of the membership
**displayId**<br>*string*		   	| Unique hash used as civilian facing id
**customerId**<br>*integer*			| Unique id of the associated customer
**billing**<br>*object*					| Billing object containing name and address details associated with order
**formId**<br>*integer*					| Id of the form that associated with the order
**formName**<br>*string*				| Name of the form that created membership
**formAccRef**<br>*string*			| Accounting reference string of the form that created membership
**fieldData**<br>*object*	  		|
**status**<br>*string*					| Status of the membership
**orderId**<br>*integer*				| Unique id of the order
**orderDisplayId**<br>*string*	| Unique hash used as civilian facing id
**orderNumber**<br>*string*			| Order number
**orderEmail**<br>*string*			| Email of the associated order
**total**<br>*float*				    | Total cost of the membership
**fee**<br>*float*				      | Membership Fee
**amount**<br>*float*				    | Membership Amount
**levelLabel**<br>*string*			|
**levelKey**<br>*string*			  |
**eventDate**<br>*timestamp*    |
**dateCreated**<br>*timestamp*  | Timestamp of the creation of the membership
**dateUpdated**<br>*timestamp*  | Timestamp the membership was last updated (optional) -->
