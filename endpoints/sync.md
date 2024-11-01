# Sync endpoint

The `sync` endpoint is convenient to maintain a remote copy of a user's library of trips and/or routes.

## GET /api/v1/sync.json?since=[since]

Returns a list of items (routes and/or trips) that the user has interacted with (`created`, `updated`, `deleted`, `pinned` and `unpinned`) since the given `<since>` datetime.

**Request**

* **Method**: `GET`
* **URL**: `https://ridewithgps.com/api/v1/sync.json`
* **Authentication**: [Required](../authentication.md)
* **Query params**:
  * `since=[since]` - iso8601 formatted datetime
  * `assets=routes,trips` - the type of assets to return, defaults to your API client setting.

**Example response**

```javascript
// 200 - OK
{
  "items": [
    {
      "item_type": "route",
      "item_id": 217,
      "item_user_id": 2,
      "item_url": "httpis://ridewithgps.com/api/v1/routes/217.json",
      "action": "added",
      "datetime": "2024-09-05T23:17:55Z",
      "collection": {
        "id": 1,
        "type": "pinned",
        "name": "pinned",
        "url": "http://localhost/api/v1/collections/1.json"
      }
    },
    {
      "item_type": "route",
      "item_id": 218,
      "item_user_id": 1,
      "item_url": "https://ridewithgps.com/api/v1/routes/218.json",
      "action": "updated",
      "datetime": "2024-09-05T23:19:36Z",
      "collection": null
    },
    {
      "item_type": "trip",
      "item_id": 738,
      "item_user_id": 1,
      "item_url": "https://ridewithgps.com/api/v1/trips/738.json",
      "action": "created",
      "datetime": "2024-09-09T22:29:01Z",
      "collection": null
    }
  ],
  "meta": {
    "rwgps_datetime": "2024-09-09T22:53:52+00:00",
    "next_sync_url": "http://localhost:3000/api/v1/sync.json?assets=routes%2Ctrips&since=2024-09-09T22%3A53%3A52%2B00%3A00"
  }
}
```

* `item_type` is either `trip` or `route`.
* `item_id` is the `id` of the item.
* `item_user_id` is the `id` of the user who owns the item. It will be the `id` of the authenticated user for `created`, `updated` and `deleted` actions. It might point to another user for `added` and `removed`, when the authenticated user pins an item from another user.
* `datetime` is the datetime at which the action was taken.
* `action` is one of the following:

| Action    | Description                                             |
| --------- | ------------------------------------------------------- |
| `created` | The user created the item                               |
| `updated` | The user updated the item                               |
| `deleted` | The user deleted the item                               |
| `added`   | The added the item to the specified collection          |
| `removed` | The user removed the item from the specified collection |

* For `added` and `removed` action, `collection` is the target collection where the action was taken. It is currently always the collection of pinned items for the authenticated user, but we might expose other collections in the future.

## Sync workflow

This endpoint is optimized for performance (we use a similar setup for syncing our own mobile apps), and can return the entire library for the user by using a `since` value well in the past (for example `1970-01-01`).

The following workflow is suitable to maintain your copy of a user's library:

* When the user finalizes the OAuth workflow, get the current content of their library at `GET https://ridewithgps.com/api/v1/sync.json?since=1970-01-01`
* Download and integrate in your system every item in the response and store the value of the `meta.rwgps_datetime` key in the response
* Upon reception of a [webhook](../webhooks.md) for the user, get the and integrate the items that have changed from a new sync request at `GET https://ridewithgps.com/api/v1/sync.json?since=[rwgps_datetime]`. Store the new value of `meta.rwgps_datetime` for the next sync request.

Doing a sync request on webhook reception instead of processing the items in the body of the webhook leads to the same result and provides a recovery mechanism for previous webhooks that might have failed because of network or systems availability issues.
