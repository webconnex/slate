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

#### HTTP Response Headers

> API returns typical JSON structured like this:

```json
{
  "responseCode": 200,
  "data": [
    {
			"foo": "bar",
      "bar": "foo"
    }
	]
}
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

> API returns typical JSON structured like this:

```json
{
	"responseCode": 400,
	"error": {
		"code": 4000,
		"message": "invalid request - expected int received string"
	}
}
```

#### HTTP Codes (HTTP Response Code)

| HTTP Code		| Description |
| ------------ |------------------------------------------|
| 200 OK	| The request was successful, we updated/created the resource and the responded body contains the representation |
| 204 OK DELETED	| The request was successful; the resource was deleted |
| 400 BAD REQUEST | The data provided or requested failed validation. Inspect the request and / or response body for details |
| 401 UNAUTHORIZED	| The supplied credentials, if any, are not sufficient to create or update the resource	|
| 402 REQUEST FAILED	| The parameters were valid but the request failed |
| 404 NOT FOUND | Not found (or unauthorized)	|
| 405 METHOD NOT ALLOWED	| You can't POST or PUT to the resource	|
| 429 TOO MANY REQUESTS | Your application is sending too many simultaneous requests |
| 500 SERVER ERROR	| We couldn't create or update the resource. Please try again	|
| 502 SERVER ERROR	| We couldn't create or update the resource. Please try again	|
