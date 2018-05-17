# Appendix

Below is additional information and resources

## Maintenance Window

Webconnex regularly performs system maintenance Tuesday's between 9:00 am UTC (2am Pacific Daylight Time, 1am Pacific Standard Time) and 10:00 am UTC (3am Pacific Daylight Time, 2am Pacific Standard Time). During this maintenance window various endpoints may be unavailable as well as Webhook Events may be queued and not delivered till after the maintenance window completes. We recommend scheduling your applications around this time window.

## URI Parameters

### Date Formats

The following datetime formats can be used when querying with a `timestamp` URI parameter.

- "2006-01-02 15:04"
- "01-02-2006"
- "2006-01-02"
- "2006-01-02T15:04:05Z"

## Orders Details

| Available Statuses
| -----------------------
| pending
| abandoned
| completed
| canceled
| pending offline payment
| pending final payment
| waitlisted

Click [HERE](http://help.regfox.com/article/973-registration-statuses-explained) to see a help article explaining these statuses.

## Registrants Details

| Available Statuses
| -----------------------
| pending
| abandoned
| completed
| transferred
| pending transfer
| canceled
| pending offline payment
| pending final payment
| waitlisted

Click [HERE](http://help.regfox.com/article/973-registration-statuses-explained) to see a help article explaining these statuses.

## Tickets Details

| Available Statuses
| -----------------------
| pending
| abandoned
| completed
| canceled
| pending offline payment
| pending final payment

Click [HERE](http://help.ticketspice.com/article/501-order-statuses-explained) to see a help article explaining these statuses.

## Transactions Details

### Statuses

| Available Statuses
| ------------------
| processing
| pending offline
| declined
| canceled
| completed
| voided
| canceled
| gateway error
| error

Click [HERE](http://help.regfox.com/article/972-transaction-statuses-explained) to see a help article explaining these statuses.

### Types

| Types | Description
| -------------	| -------------------------------------------------------
| charge				|
| refund				|
| voucher				|
| cash					|
| preauth				| A zero dollar transaction used for validating a future payment method
| chargeback		| Transaction used to report when a credit card holder contacts his bank or credit card company to dispute a charge on his account

## Subscriptions / Reoccurring Payments Details

Available Statuses | Description
------------------ | -------------------------------------------------------
active             | Is active and will continue to process future payments
inactive           | Is inactive and will not process future payments
canceled           | Is canceled and will no longer process future payments
completed          | Is completed and will no longer process future payments

## Memberships Details

| Available Statuses
| ------------------
| purchasing
| active
| inactive
| expired
| purchasing
| abandoned

## Forms Details

| Available Statuses
| ------------------
| open
| closed
| scheduled
| archived
| deleted

## Webhooks Details

### Statuses

| Available Statuses
| ------------------
| enabled
| disabled

### Types

Id   | Available Types
---- | ------------------------------------------------
1    | Standard webhook
2-20 | Internal webhook types that should not be edited

## Currency Details

Note: additional new currencies can be added at any time.

Code | Name                                    | Symbol
---- | --------------------------------------- | ------
USD  | United States dollar                    | $
CAD  | Canadian dollar                         | $
AUD  | Australian dollar                       | $
NZD  | New Zealand dollar                      | $
GBP  | British pound sterling                  | £
MXN  | Mexican peso                            | $
EUR  | Euro                                    | €
CHF  | Swiss Franc                             | FR
CNY  | Chinese Yuan Renminbi                   | ¥
JPY  | Yen  	                                 | ¥
