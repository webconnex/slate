# Appendix

Below is additional information and resources

## URI Parameters

### Date Formats

The following date formats can be used when querying with a timestamp URI parameter.

- "2006-01-02 15:04"
- "01-02-2006"
- "2006-01-02"
- "2006-01-02T15:04:05Z"

## Orders

| Available Statuses
| -----------------------
| pending
| abandoned
| completed
| canceled
| pending offline payment
| pending final payment
| waitlisted

## Registrants

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

## Tickets

| Available Statuses
| -----------------------
| pending
| abandoned
| completed
| canceled
| pending offline payment
| pending final payment

## Transactions

| Available Statuses
| ------------------
| pending offline
| declined
| canceled
| completed
| voided
| canceled
| gateway error
| error

| Types
| ------------------
| charge
| refund
| voucher

## Subscriptions

Available Statuses | Description
------------------ | -------------------------------------------------------
active             | Is active and will continue to process future payments
inactive           | Is inactive and will not process future payments
canceled           | Is canceled and will no longer process future payments
completed          | Is completed and will no longer process future payments

## Memberships

| Available Statuses
| ------------------
| active
| inactive
| expired
| purchasing
| abandoned

## Forms

| Available Statuses
| ------------------
| open
| closed
| scheduled
| archived
| deleted

## Webhooks

| Available Statuses
| ------------------
| enabled
| disabled

Id   | Available Types
---- | ------------------------------------------------
1    | Standard webhook
2-10 | Internal webhook types that should not be edited

## Currency

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
