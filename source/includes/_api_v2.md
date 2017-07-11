# API

## Structure

### Overview

The Webconnex API is build upon simple REST patterns. We use standard HTTP methods and error codes in our responses.

URL: `https://api.webconnex.com/v2/public/`

### Authentication

Authentication happens through the use of an API key issued from the Integrations pane under account settings.

### Rate Limits

We have a daily limit of 15000 requests per day and a burst limit of up to 900 requests per 15 minutes.

### Responses

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
X-Burst-Limit | The number of allowed requests in the current period (15 min)
X-Burst-Remaining | The number of remaining requests in the current period (15 min)
X-Burst-Limit-Reset | The number of seconds left in the current period (15 min)
X-Retry-After | If surpassed `X-Daily-Limit` or `X-Burst-Limit`, - the unix time when requests can be submitted again (15 min or daily depending on which limit is hit)

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
**responseCode**<br>*integer*   | The http response code of the request
**data**<br>*object* or *array*	| The requested data in an array or object format
**totalResults**<br>*integer*	  | The total number of results found (not returned)
**startingAfter**<br>*integer*  | The id to begin when retrieving the next page of results
**hasMore**<br>*bool*		        | A boolean specifying if more results exist and should be requested via paging

#### Error Response Object

> API returns typical error JSON structured like this:

```json
{
	"responseCode": 400,
	"error": {
		"code": 4000,
		"message": "invalid request - expected int received string"
	}
}
```
Attribute			                  |	Description
--------------------------------|-----------------------------------------------
**responseCode**<br>*integer*   | The http response code of the request
**error**<br>*object*           |
**code**<br>*integer*	          | Internal error code
**message**<br>*integer*        | A friendly error message

#### HTTP Codes (HTTP Response Code)

Below are the http response codes used by the API

| HTTP Code		                  | Description 
| ------------------------------|-----------------------------------------------
| **200**<br>OK                 | The request was successful, we updated/created the resource and the responded body contains the representation
| **204**<br>OK DELETED	        | The request was successful; the resource was deleted
| **400**<br>BAD REQUEST        | The data provided or requested failed validation. Inspect the request and / or response body for details
| **401**<br>UNAUTHORIZED	      | The supplied credentials, if any, are not sufficient to create or update the resource
| **402**<br>REQUEST FAILED	    | The parameters were valid but the request failed |
| **404**<br>NOT FOUND          | Not found (or unauthorized)	|
| **405**<br>METHOD NOT ALLOWED	| You can't POST or PUT to the resource
| **429**<br>TOO MANY REQUESTS  | Your application is sending too many simultaneous requests
| **500**<br>SERVER ERROR	| We couldn't create or update the resource. Please try again
| **502**<br>SERVER ERROR	| We couldn't create or update the resource. Please try again

### Paging
```markdown
https://api.webconnex.com/parent?limit=100&startingAfter=45&sort=desc
```
Paging is requested though URI promoter for any resource the returns a collection of objects

Parameter		     	              |	Description
--------------------------------|-----------------------------------------------
**sort**<br>*string* 		      	| sets the returned order (`asc` or `desc`)
**limit**<br>*string* 				  | limits the number of results returned
**startingAfter**<br>*integer*  | filter to only show results with id's after the supplied value

### Expand
```markdown
Example Usage
https://api.webconnex.com/parent/id/child?[]expand=registrants,tickets,subscription,inventory
```

Multiple endpoints allow for a `[]expand=?` URI parameter to be passed to return additional information

Endpoints which support `[]expand`:

- [View Form](#get-form-by-id)

- [View Order](#view-order-by-id)

- [View Registrant](#view-registrant-by-id)
