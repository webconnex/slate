# Endpoints

Method			|	Path 									|	Resource 			| Description
------------|-----------------------|---------------|------------------------------
GET 				|/ping									| Ping					| Simple endpoint to check API health
GET					|/forms									|	Form					|
GET 				|/forms/{id}						|	Form					|
GET					|/webhooks							|	Webhook				|
POST				|/webhooks							|	Webhook 			|
GET					|/webhooks/{id}					| Webhook				|
PUT					|/webhooks/{id}					| Webhook				|
DELETE			|/webhooks/{id}					|	Webhook				|
GET					|/orders/{id}						|	Order					|
GET					|/search/orders					|	Order					| Required params: product
GET					|/orders								|	Order					|
GET					|/transactions/{id}			| Transaction		|
GET					|/transactions					| Transaction		|
GET					|/registrants/{id}			| Registrant		|
GET					|/registrants						| Registrant		|
GET					|/tickets/{id}					| Ticket				|
GET					|/tickets								| Ticket				|
GET					|/subscriptions/{id}		| Subscription	|
GET					|/subscriptions					| Subscription	|
GET					|/coupons/global				| Coupon				|
GET					|/coupons/form/{formID}	|	Coupon				|
GET					|/coupons/{couponID}		|	Coupon				|

[//]: # (PUT 				|/forms/{id}						|	Form					|)
[//]: # (DELETE			|/forms/{id} 						|	Form 					|)
[//]: # (POST 				|/forms									|	Form					|)
