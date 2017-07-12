# API Reference

## Overview

The Webconnex API is build upon simple REST patterns. We use standard HTTP methods, resource-oriented URLs and HTTP error codes in our responses.

URL: `https://api.webconnex.com/v2/public/`


## Authentication

> Typical authenticated API request:

```curl
curl -X "GET" "http://api.webconnex.com/v2/public/ping" \
	-H "apiKey: <YOUR API KEY>"
```

Authentication happens through the use of an API key issued from the Integrations pane under account settings. A valid API Key must be included in the request header for each request.

## Structure

### Rate Limits

We have a default daily limit of *15,000* requests per day with a burst limit of up to *900* requests per *15 minutes* block of time.

### Responses

JSON is returned by all API responses, including errors.

#### HTTP Headers

> API returns typical JSON structured like this:

```markdown
HTTP/1.1 200 OK
Access-Control-Expose-Headers:
Content-Type: application/json; charset=UTF-8
Date: Sat, 08 Jul 2017 04:51:44 GMT
Server: nginx/1.6.3
X-Burst-Limit: 900
X-Burst-Limit-Reset: 1499489248
X-Burst-Remaining: 898
X-Daily-Limit: 100
X-Daily-Limit-Reset: 1499558399
X-Daily-Remaining: 96
Content-Length: 617
Connection: keep-alive
```

Header | Description
---------------------- | --------------
X-Daily-Limit | The number of allowed requests in the current period (daily)
X-Daily-Remaining | The number of remaining requests in the current period (daily)
X-Daily-Limit-Reset | The number of seconds left in the current period (daily)
X-Burst-Limit | The number of allowed requests in the current period (15 min blocks)
X-Burst-Remaining | The number of remaining requests in the current period (15 min blocks)
X-Burst-Limit-Reset | The number of seconds left in the current period (15 min blocks)
X-Retry-After | If surpassed `X-Daily-Limit` or `X-Burst-Limit`, - `X-Retry-After` is the unix time when requests can be submitted again (15 min or daily depending on which limit is hit)

#### Successful Response Object

> API returns typical JSON structured like this:

```json
{
  "responseCode": 200,
  "data": [
    {
      "foo": "bar",
      "bar": "foo"
    }
	],
  "totalResults": 1,
  "startingAfter": 1,
  "hasMore": false
}
```

Attribute			                  |	Description
--------------------------------|-----------------------------------------------
**responseCode**<br>*integer*   | Http response code of the request
**data**<br>*object* or *array*	| Requested data in an array or object format
**totalResults**<br>*integer*	  | Total number of results found (Note not the returned count)
**startingAfter**<br>*integer*  | an object ID that defines your place in the list
**hasMore**<br>*bool*		        | Whether or not there are more objects available after this set. If `false`, this is the end of the list

#### Error Response Object

> API returns typical error JSON structured like this:

```json
{
	"responseCode": 400,
	"error": {
		"code": 4000,
		"message": "invalid request - expected integer but received string"
	}
}
```

Attribute			                  |	Description
--------------------------------|-----------------------------------------------
**responseCode**<br>*integer*   | Http response code of the request
**error**<br>*object*           | Object containing the error details
**code**<br>*integer*	          | Internal Webconnex error code
**message**<br>*integer*        | A friendly error message

#### HTTP Response Code

webconnex uses standard HTTP response codes to indicate the success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate a request error and codes in the 5xx range indicate an internal error.

Below are a summary of the HTTP response codes used by the webconnex API.

| Code	/ Message	                  | Description
| ------------------------------|-----------------------------------------------
| **200**<br>OK                 | The request was successful, we updated/created the resource and the responded body contains the representation
| **204**<br>OK DELETED	        | The request was successful; the resource was deleted
| **400**<br>BAD REQUEST        | The data provided or requested failed validation. Inspect the request and / or response body for details
| **401**<br>UNAUTHORIZED	      | The supplied credentials, if any, are not sufficient to create or update the resource
| **402**<br>REQUEST FAILED	    | The parameters were valid but the request failed
| **404**<br>NOT FOUND          | Resource was not found
| **405**<br>METHOD NOT ALLOWED	| You can't POST or PUT to the resource
| **429**<br>TOO MANY REQUESTS  | Your application is sending too many requests
| **500**<br>SERVER ERROR	| We couldn't create or update the resource. Please try again
| **502**<br>SERVER ERROR	| We couldn't create or update the resource. Please try again

### Paging
```markdown
https://api.webconnex.com/parent?limit=100&startingAfter=45&sort=desc
```

Webconnex utilizes cursor-based pagination via the `startingAfter` and `limit` URI parameters. Paging can be used for any resource the returns a collection of objects.

Parameter		     	              |	Description
--------------------------------|-----------------------------------------------
**sort**<br>*string* 		      	| Sets the returned order `asc` or `desc`
**limit**<br>*string*<br>(optional, default is 50) 				  | A limit on the number of objects to be returned, between 1 and 50
**startingAfter**<br>*integer*  | startingAfter is an object id that defines your place in the list
**pretty**<br>*boolean* 		    | If `True` JSON response is returned in Tab formatted style

### Expand
```markdown
Example Usage
https://api.webconnex.com/parent/id/child?[]expand=registrants,tickets,subscription,inventory
```

Multiple endpoints allow for a `[]expand=?` URI parameter to be passed to return additional information about a resources children. You can expand multiple objects at once by identifying multiple items in the expand array.

Endpoints which support `[]expand` include:

- [View Form](#get-form-by-id)

- [View Order](#view-order-by-id)

- [View Registrant](#view-registrant-by-id)
