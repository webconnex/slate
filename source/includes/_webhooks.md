# Webhook

Our webhook system allows you to receive data when certain events happen on your account.

We currently support the following events:

- New Registrations/Orders Notification
- Subscription/Recurring Notification
- Reoccurring SMS Donation Notification (Beta)
- Form Published Notification
- Inventory Supply Notification
- Coupons Notification
- Test Notification

## Control Panel Interface

Aside from using the public API, you can create webhooks in the [control-panel interface](https://manage.webconnex.com) under the Extra -> Integrations Tab.

The default screen lists all of your current integrations.
![Integration Listings](/images/integration-listings.png)

Clicking on an integration will navigate to the details page where you can configure various options.

![Webhook Settings](/images/webhook-settings.png)

The control panel will show you a log of all the requests made for a given webhook and allow you to view your servers response to the sent webhook to help you troubleshoot any potential problems.

![Recent Webhooks](/images/webhook-recent.png)

Clicking on the details of a request will reveal more information that might be useful in troubleshooting problems. You can also resend your webhook from this pane.

![Webhook Details](/images/webhook-details.png)

## Headers

> Supplied Header:

```json
{
  "Content-Type": [
    "application/json"
  ],
  "User-Agent": [
    "Webconnex-Divvy"
  ],
  "X-Webconnex-Delivery": [
    "b473fe314def43ccacc10ec75aae1451"
  ],
  "X-Webconnex-Event": [
    "test"
  ],
  "X-Webconnex-Signature": [
    "bcfb8142ac545c5b7e5d6f0694234e6a01b2cd57d4732d883548a97d020221df"
  ]
}
```

Parameter             | Description
--------------------- | --------------------------------------------------------
Content-Type          | application/json
User-Agent            | Webconnex-Divvy
X-Webconnex-Delivery  | Hash for the delivery
X-Webconnex-Event     | Event types being sent
X-Webconnex-Signature | HMAC for the webhook. Note: Remains unchanged on resend events

## Verifying Signatures

> Generating expected signature in Ruby:

```ruby
key = 'cdcf15c7c0184636a0fd7af7dbd42929' # Found in Webhook Settings Page
data = response.body
digest = OpenSSL::Digest.new('sha256')
signature = OpenSSL::HMAC.hexdigest(digest, key, data)
```

It is highly recommended that you verify the signature of all webhook requests to ensure the events were sent by Webconnex and not by a third-party.  Verification can be performed by following the steps outlined below:

1. **Extract the signature**
   * Extract the signature from `X-Webconnex-Signature` header.
2. **Determine the expected signature**
   * Generate an HMAC with the SHA256 hash function using the webhook's `Signing Secret` as the key and the response body as the message.  The `Signing Secret` can be found on the webhook settings page.
3. **Compare signatures**
   * Compare the signature found in the `X-Webconnex-Signature` header to the generated expected signature in Step 2. It is a valid request if the signatures match.