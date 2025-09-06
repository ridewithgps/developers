# Event endpoints

## GET /api/v1/events.json

Returns a paginated list of routes owned by the authenticated user, ordered by `updated_at` descending.

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

Events in this representation do not include details on the events asscociate routes, participants or organizers.

## GET /api/v1/events/:id.json

Returns a full representation of the event identified by its `id`.

**Request**

* **Method**: `GET`
* **URL**: `https://ridewithgps.com/api/v1/events/:id.json`
* **Authentication**: [Required](../authentication.md)

**Example Response**

```javascript
// GET https://ridewithgps.com/api/v1/events/1.json
// 200 - OK

{
  "event": {
    "id": 1,
    "user_id": 1,
    "url": "https://ridewithgps.com/api/v1/events/1.json",
    "html_url": "https://ridewithgps.com/api/v1/events/1-long-day",
    "name": "Long day",
    "description": null,
    "visibility": "public",
    "location": "The bakery",
    "lat": 45.561964,
    "lng": -122.68902,
    "time_zone": "America/Los_Angeles",
    "start_date": "2024-11-02",
    "start_time": "08:00",
    "end_date": "2024-11-02",
    "end_time": "14:30",
    "all_day": false,
    "created_at": "2024-10-25T09:27:00-07:00",
    "updated_at": "2024-10-25T09:27:00-07:00",
    "routes": [
      {
        "id": 3,
        "url": "http://localhost/api/v1/routes/1.json",
        "name": "A very hard century",
        "description": "",
        "locality": "Portland",
        // ...
      },
      // ...
    ]
    "organizers": [
      {
        "id": 1,
        "name": "Testy",
        "created_at": "2024-10-25T16:26:06Z",
        "updated_at": "2025-09-03T15:35:17Z"
      },
      // ...
    ],
    "participants": [
      {
        "user": {
          "id": 2,
          "name": "Alice",
          "created_at": "2024-10-25T16:26:06Z",
          "updated_at": "2025-09-03T15:35:17Z"
        },
        "status": "participant",
        "created_at": "2025-09-06T00:03:39Z",
        "updated_at": "2025-09-06T00:03:39Z"
      },
      // ...
    ]
  }
}
```

In the response:

* The routes are in their short representation. Fetch the route URL to get track points, course points and points of interest.
* The organizer key is present only for organizations. It lists the organization members that are organizers of the event.
* The participant key lists users with their participation `status`. Possible values are `joined`, `interested`, `declined` and `disallowed`.

If the authenticated user does not have permission to view the event, a `403 - Forbidden` error is returned.
