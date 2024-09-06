# Webhooks

Ride with GPS issues a `POST` request to your webhook URL whenever a user of your OAuth application creates, updates, deletes, pins or unpins a route or a trip (whichever you have selected to sync).

## Configuration

Your API client must first be configured for OAuth.

From your API client management page, enter the URL (`webhook_url`) at which you'd like to be notified and check the types of assets should trigger a call to your webhook. The `route` and `trip` types are supported, and you will be notified when the the `created`, `updated`, `deleted`, `pinned` or `unpinned` actions are taken on those assets.

## Webhook request

Ride with GPS sends `POST` notifications at your webhook URL with actions that have been taken by one of your users on one or multiple items. Here is an example of a webhook request body:

**Request**

* **Method**: `POST`
* **URL**: `[webhook_url]`
* **Headers**: 
  * `content-type: application/json`
  * `user-agent: RideWithGPS`
  * `x-rwgps-api-key: [api_key]`
  * `x-rwgps-signature: [signature]`
* **Body**

```javascript
{
  "notifications": [
    {
      "user_id": 1,
      "item_type": "route",
      "item_id": 101,
      "item_user_id": 1,
      "item_url": "https://ridewithgps.com/routes/101.json",
      "action": "deleted",
      "collection": null
    },
    {
      "user_id": 2,
      "item_type": "route",
      "item_id": 102,
      "item_user_id": 1,
      "item_url": "https://ridewithgps.com/routes/102.json",
      "action": "added",
      "collection": {
        "id": 2,
        "type": "pinned",
        "url": null
      }
    },
    {
      "user_id": 1,
      "item_type": "route",
      "item_id": 201,
      "item_user_id": 1,
      "item_url": "https://ridewithgps.com/routes/201.json",
      "action": "created",
      "collection": null
    }
  ]
}
```

> [!NOTE]
> No more than 100 notifications are sent per request.

For each notification in the request payload:

* `user_id` is the id of the user who took the action.
* `item_type` is either `trip` or `route`.
* `item_id` is the `id` of the item.
* `item_user_id` is the `id` of the user who owns the item. It will equal `user_id` for `created`, `updated` and `deleted` actions. It might point to another user for `added` and `removed`, when the user user pins an item from another user.
* `action` is one of the following:

| Action    | Description                                             |
| --------- | ------------------------------------------------------- |
| `created` | The user created the item                               |
| `updated` | The user updated the item                               |
| `deleted` | The user deleted the item                               |
| `added`   | The added the item to the specified collection          |
| `removed` | The user removed the item from the specified collection |

* For `added` and `removed` action, `collection` is the target collection where the action was taken. It is currently always the collection of pinned items for user, but we might expose actions on other collections in the future.

Webhook requests include the following headers:

* `x-rwgps-api-key` lets you identify the API client responsible for the request in case you have created multiple API clients.
* `x-rwgps-signature` is a HMAC-SHA256 signature of the raw request body, using your OAuth secret as the signing key. Compute the signature on your end to validate that the request originated from Ride with GPS. For example:

```python
# Python example
import hmac
signature = request_headers['x-rwgps-signature']
valid = hmac.compare_digest(signature, hmac.new('[oauth_secret]', request_raw_body, sha256).hexdigest())
```

```javascript
// Javascript example
const { createHmac } = require('crypto')
const signature = requestHeaders['x-rwgps-signature']
const valid = signature == createHmac('sha256', '[oauthSecret]').update(requestRawBody).digest('hex')
```

## Webhook request handling

When requesting your webhook, Ride with GPS expects a `200` response within 1 second. We strongly recommend that you acknowledge the webhook request as quickly as possible and process its content in a separate thread.

Processing a webhook request includes, for each `notification` in the `notifications` array:

* Retrieve from your system the OAuth `access_token` associated with the `notification.user_id`
* Fetch `item_url`, authenticating the request with the OAuth `access_token` (see [OAuth documentation](authentication.md))
* Update your records with the new or updated item

> [!TIP]
> If you did not store the `user_id` alongside the `access_token`, you can retrieve it from [this endpoint](endpoints/users.md).

> [!NOTE]
> No retry mechanism is implemented at this point.
> Ride with GPS does not follow `3xx` redirect status codes.
