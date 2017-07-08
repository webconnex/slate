## Endpoints

Method			|	Path 											|	Resource 			| Description / Notes
------------|---------------------------|---------------|-----------------------
GET 				|/ping											| Ping					| Simple endpoint to check API health
GET					|/search/orders/{id}				|	Order					|
GET					|/search/orders							|	Order					| Required params: product
GET					|/search/registrants/{id}		| Registrant		|
GET					|/search/registrants				| Registrant		|	Required params: product
GET					|/search/tickets/{id}				| Ticket				|
GET					|/search/tickets						| Ticket				|
GET					|/search/subscriptions/{id}	| Subscription	|
GET					|/search/subscriptions			| Subscription	|	Required params: product
GET					|/search/transactions/{id}	| Transaction		|
GET					|/search/transactions				| Transaction		|	Required params: product
GET					|/search/customers/{id}			| Customer			|
GET					|/search/customers					| Customer			|	Required params: product
GET					|/forms											|	Form					|
GET 				|/forms/{id}								|	Form					|
GET					|/forms/{formID}/inventory	|	Inventory			|
GET					|/coupons/global						| Coupon				|	Required params: product
GET					|/coupons/form/{formID}			|	Coupon				|
GET					|/coupons/{couponID}				|	Coupon				|
GET					|/webhooks									|	Webhook				|
POST				|/webhooks									|	Webhook 			|
GET					|/webhooks/{id}							| Webhook				|
PUT					|/webhooks/{id}							| Webhook				|
DELETE			|/webhooks/{id}							|	Webhook				|
GET					|/webhooks/{id}	/logs				| Webhook Log		|
GET					|/webhooks/{webhookID}/logs/{id}			| Webhook Log	| Retrieve a list of sent webhooks in log format		|
POST				|/webhooks/{webhookID}/resend/{logID}	| Webhook Log	| Resend a webhook event	|
