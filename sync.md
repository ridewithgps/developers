# Sync and webhooks

Choose to sync routes and/or trips from each of your API client management page.


## Webhooks

Ride With GPS issues a `POST` request to your webhook URL whenever a user of your OAuth application creates, updates, deletes, pins or unpins a route or a trip (whichever you have selected to sync).

### Configuration

From your user account settings page go to the **Developers** tab and edit the API client for your OAuth application. Enter the URL at which you'd like to be notified and check the types of items that should trigger a notification. The `route` and `trip` types are supported, and you will be notified when the the `created`, `updated`, `deleted`, `pinned` or `unpinned` actions are taken on those items.

### Webhook request

Ride With GPS `POST` notifications at your webhook URL with actions that have been taken by one of your users on one or multiple items. Here is an example of a webhook request body:

```javascript
{
  "notifications": [
    {
      "user_id" : 1,
      "item_type": "route",
      "item_id": 1,
      "item_url": "https://ridewithgps.com/routes/1.json"
      "action": "pinned"
    },
    {
      "user_id" : 2,
      "item_type": "trip",
      "item_id": 1,
      "item_url": "https://ridewithgps.com/trips/1.json?privacy_code=abcdef"
      "action": "updated"
    }
    {
      "user_id" : 1,
      "item_type": "trip",
      "item_id": 2,
      "item_url": "https://ridewithgps.com/trips/2.json"
      "action": "created"
    },
  ]
}
```

No more than 100 notifications are sent at once.

Request to your webhook URL are made with the following headers:

```
content-type: application/json
user-agent: RideWithGPS
x-rwgps-api-key: <api_key>
x-rwgps-signature: <signature>
```

The `x-rwgps-api-key` header is included to let you identify the API client responsible for the request in case you handle multiple API clients from the same system.

Every webhook request includes a `x-rwgps-signature` header whose value is a HMAC-SHA256 signature of the raw request body, using your OAuth secret as the signing key. This allows you to validate that the request originated from Ride With GPS, by checking the validity of the signature before processing.

```python
# Python example
import hmac
signature = request_headers['x-rwgps-signature']
valid = hmac.compare_digest(signature, hmac.new('<oauth_secret>', request_raw_body, sha256).hexdigest())
```

```javascript
// Javascript example
const { createHmac } = require('crypto')
const signature = requestHeaders['x-rwgps-signature']
const valid = signature == createHmac('sha256', '<oauthSecret>').update(requestRawBody).digest('hex')
```

### Webhook request handling

When requesting your webhook, Ride With GPS expects a `200` response within 1 second. We strongly recommend that you acknowledge the webhook request as quickly as possible and process its content in a separate thread.

Processing a webhook request includes, for each `notification` in the `notifications` array:

* Retrieve from your system the OAuth `access_token` associated with the `notification.user_id`
* Fetch `item_url`, authenticating the request with the OAuth `access token` (see [OAuth documentation](authentication.md))
* Update your records with the new or updated item

Note: If you did not store the `user_id` alongisde the `access_token`, you can retrieve with a `GET https://ridewithgps.com/current.json` request autehnticated with `access_token`. The response includes information about the autehnticated user, including its ID.

### Other implementation notes

* No retry mechanism is implemented at this point.
* Ride With GPS does not follow `3xx` redirect status codes.




