## Endpoints

Method | Path                                 | Resource
------ | ------------------------------------ | ------------
GET    | /ping                                | Ping
GET    | /search/orders/{id}                  | Order
GET    | /search/orders                       | Order
GET    | /search/registrants/{id}             | Registrant
GET    | /search/registrants                  | Registrant
GET    | /search/tickets/{id}                 | Ticket
GET    | /search/tickets                      | Ticket
GET    | /search/subscriptions/{id}           | Subscription
GET    | /search/subscriptions                | Subscription
GET    | /search/transactions/{id}            | Transaction
GET    | /search/transactions                 | Transaction
GET    | /search/customers/{id}               | Customer
GET    | /search/customers                    | Customer
GET    | /forms                               | Form
GET    | /forms/{id}                          | Form
GET    | /forms/{formID}/inventory            | Inventory
GET    | /coupons/global                      | Coupon
GET    | /coupons/form/{formID}               | Coupon
GET    | /coupons/{couponID}                  | Coupon
GET    | /webhooks                            | Webhook
POST   | /webhooks                            | Webhook
GET    | /webhooks/{id}                       | Webhook
PUT    | /webhooks/{id}                       | Webhook
DELETE | /webhooks/{id}                       | Webhook
GET    | /webhooks/{id} /logs                 | Webhook Log
GET    | /webhooks/{webhookID}/logs/{id}      | Webhook Log
POST   | /webhooks/{webhookID}/resend/{logID} | Webhook Log
