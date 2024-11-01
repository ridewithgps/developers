# Event endpoints

## GET /api/v1/events.json

Returns a paginated list of routes owned by the authenticated user, ordered by `created_at` descending.

**Request**

* **Method**: `GET`
* **URL**: `https://ridewithgps.com/api/v1/events.json`
* **Authentication**: [Required](../authentication.md)
* **Query params**: 
  * `page=<page_number>` - Optional, used for [pagination](../README.md#pagination)

**Example response**

```javascript
// GET https://ridewithgps.com/api/v1/events.json
// 200 - OK
{
  "events": [
    {
      "id": 999,
      "url": "https://ridewithgps.com/api/v1/events/999.json",
      "name": "Last event",
      // ...
    },
    {
      "id": 844,
      "url": "https://ridewithgps.com/api/v1/events/844.json",
      "name": "Another event",
      // ...
    },
    // ...
  ],
  "meta": {
    "pagination": {
      "record_count": 12,
      "page_count": 2,
      "next_page_url": "https://ridewithgps.com/api/v1/events.json?page=2"
    }
  }
}
```

Events in this representation do not include details on the routes they are associated with.

## GET /api/v1/events/[id].json

Returns a full representation of the event identified by its `id`.

**Request**

* **Method**: `GET`
* **URL**: `https://ridewithgps.com/api/v1/events/[id].json`
* **Authentication**: [Required](../authentication.md)

**Example Response**

```javascript
// GET https://ridewithgps.com/api/v1/events/1.json
// 200 - OK

{
  "event": {
    "id": 1,
    "url": "https://ridewithgps.com/api/v1/events/1-boring-event.json",
    "name": "It's going to be a long day",
    "description": null,
    "starts_on": "2024-11-02",
    "starts_at": "2024-11-02T00:00:00-07:00",
    "ends_on": "2024-11-03",
    "ends_at": null,
    "created_at": "2024-10-25T09:27:00-07:00",
    "updated_at": "2024-10-25T09:27:00-07:00",
    "routes": [
      {
        "id": 3,
        "url": "http://localhost/api/v1/routes/1.json",
        "name": "A very hard centuryt",
        "description": "",
        "locality": "Portland",
        // ...
      },
      // ...
    ]
  }
}
```

The routes in the response are in their short representation, query the route URL to get track points, course points and points of interest.

If the authenticated user does not have permission to view the event, a `403 - Forbidden` error is returned.
