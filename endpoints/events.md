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
      "user_id": 1,
      "url": "https://ridewithgps.com/api/v1/events/999.json",
      "html_url": "https://ridewithgps.com/api/v1/events/999-last-event",
      "name": "Last event",
      // ...
    },
    {
      "id": 844,
      "user_id": 1,
      "url": "https://ridewithgps.com/api/v1/events/844.json",
      "html_url": "https://ridewithgps.com/api/v1/events/844-another-event",
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

Events in this representation do not include details about their associated routes, participants, or organizers.

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
    "start_date": "2025-11-02",
    "start_time": "08:00",
    "end_date": "2025-11-02",
    "end_time": "14:30",
    "all_day": false,
    "created_at": "2025-10-01T09:27:00-07:00",
    "updated_at": "2025-10-01T09:27:00-07:00",
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
          "created_at": "2021-01-03T09:26:03Z",
          "updated_at": "2025-09-15T17:12:55Z"
        },
        "status": "participant",
        "created_at": "2025-10-03T00:03:39Z",
        "updated_at": "2025-10-03T00:03:39Z"
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

## POST /api/v1/events.json

Create a new event, owned by the authenticated user:

**Request**

* **Method**: `POST`
* **URL**: `https://ridewithgps.com/api/v1/events.json`
* **Authentication**: [Required](../authentication.md)

**Example Body**

```javascript
{
  "event": {
    "name": "A long day",
    "description": "Many routes to choose from",
    "visibility": "public",
    "location": "The Bakery",
    "lat": 45.561964,
    "lng": -122.68902,
    "time_zone": "America/Los_Angeles",
    "start_date": "2024-11-02",
    "start_time": "08:00",
    "end_date": "2024-11-02",
    "end_time": "14:30",
    "route_ids": [ 1, 2, 3],
    "organizer_ids": [ 9 ]
  }
}
```

 | Attribute              | Required  | Type      | Description                                     |
 | :--------------------- | :-------- | :-------  | :---------------------------------------------- |
 | `name`                 | True      | String    | The name for the event                          |
 | `description`          | False     | String    | Description                                     |
 | `visibility`           | False     | String    | Visibility [^1], defaults to `public`           |
 | `location`             | False     | String    | Location                                        |
 | `lat`                  | False     | Float     | Latitude for the event location                 |
 | `lng`                  | False     | Float     | Longitude for the event location                |
 | `time_zone`            | False     | String    | Timezone [^2], defaults to the user's time zone |
 | `start_date`           | True      | String    | Start date [^3]                                 |
 | `start_time`           | False     | String    | End time [^4], defaults to `null`               |
 | `end_date`             | False     | String    | End date [^3], defaults to `null`               |
 | `end_time`             | False     | String    | End time [^4], defaults to `null`               |
 | `route_ids`            | False     | [Integer] | Routes IDs to associate with the event [^5]     |
 | `organizer_ids`        | False     | [Integer] | IDs of the users organizing the event [^6]      |

* [^1]: `visibility` must be one of `public`, `private`, `friends_only` for user events, and one of `public`, `managers_only`, `members_only` for organization events.
* [^2]: `time_zone` must be one of the [supported time zone](../reference/time_zones.md). Defaults to the time zone of the authenticated user. 
* [^3]: Start and end dates must be provided in the ISO 8601 extended date format `YYYY-MM-DD`
* [^4]: Start and end times must be provided in the ISO 8601 extended time format `HH:MM` (24 hours clock)
* [^5]: Only routes owned by the event owner can be added to the event.
* [^6]: Only active members of the organization can be specified as event organizers. 

**Example Response**

The response body includes a full event representation, identical to the one of `GET /api/v1/events/:id.json`

## PATCH /api/v1/events/:id.json

Update an existing event owned by the authenticated user:

**Request**

* **Method**: `PATCH`
* **URL**: `https://ridewithgps.com/api/v1/events/:id.json`
* **Authentication**: [Required](../authentication.md)

**Example Body**

The event update endpoint accepts the same body as the event create endpoint. Partial updates are supported. For example, to replace the routes associated with an event:

```javascript
{
  "event": {
    "route_ids": [4, 5, 6]
  }
}
```

**Example Response**

The response body includes a full event representation, identical to the one of `GET /api/v1/events/:id.json`

## DELETE /api/v1/events/:id.json

Delete an event owned by the authenticated user:

**Request**

* **Method**: `DELETE`
* **URL**: `https://ridewithgps.com/api/v1/events/:id.json`
* **Authentication**: [Required](../authentication.md)

**Example Response**

On successful deletion, a `204` status code is returned.

```javascript
// DELETE https://ridewithgps.com/api/v1/events/1.json
// 204 - No Content
```
