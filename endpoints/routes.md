# Route endpoints

Reference for [route, track points, course points, points of interest and activity types](../reference.md)

## GET /api/v1/routes.json

Returns a paginated list of routes owned by the authenticated user, ordered by `created_at` descending.

**Request**

* **Method**: `GET`
* **URL**: `https://ridewithgps.com/api/v1/routes.json`
* **Authentication**: [Required](../authentication.md)
* **Query params**: 
  * `page=<page_number>` - Optional, used for [pagination](../README.md#pagination)

**Example response**

```javascript
// 200 - OK
{
  "routes": [
    {
      "id": 999,
      "url": "https://ridewithgps.com/api/v1/routes/999.json",
      "name": "Last route",
      // ...
    },
    {
      "id": 844,
      "url": "https://ridewithgps.com/api/v1/routes/844.json",
      "name": "Another route",
      // ...
    },
    // ...
  ],
  "meta": {
    "pagination": {
      "record_count": 22,
      "page_count": 1,
      "next_page_url": "https://ridewithgps.com/api/v1/routes.json?page=2"
    }
  }
}
```

Each route in the response has the same attributes as the route detail request below, except `track_points`, `course_points`, `points_of_interest` and `activity_types` that are not present here.

## GET /api/v1/routes/[id].json

Returns a full representation of the route identified by its `id`.

**Request**

* **Method**: `GET`
* **URL**: `https://ridewithgps.com/api/v1/routes/[id].json`
* **Authentication**: [Required](../authentication.md)

**Example Response**

```javascript
// GET https://ridewithgps.com/api/v1/routes/1.json
// 200 - OK

{
  "route": {
    "id": 1,
    "url": "http://localhost/api/v1/routes/1.json",
    "name": "Drummond Round Trip",
    "description": "Easy loop around Portland",
    "locality": "Portland",
    "administrative_area": "OR",
    "country_code": "US",
    "distance": 21453,
    "elevation_gain": 133,
    "elevation_loss": 134,
    "first_lat": 45.58787,
    "first_lng": -122.69944,
    "last_lat": 45.58824,
    "last_lng": -122.69944,
    "sw_lat": 45.52858,
    "sw_lng": -122.70294,
    "ne_lat": 45.58824,
    "ne_lng": -122.64282,
    "track_type": "loop",
    "terrain": "rolling",
    "difficulty": "easy",
    "unpaved_pct": 5,
    "surface": "mostly_paved",
    "activity_types": [ "cycling" ],
    "created_at": "2024-01-16T17:46:23-08:00",
    "updated_at": "2024-01-22T16:42:37-08:00",
    "track_points": [
      {
        "x": -122.69944,
        "y": 45.58708,
        "e": 25.5,
        "d": 87.9
      }
      {
        "x": -122.7014,
        "y": 45.58709,
        "e": 25.6,
        "d": 240.6
      },
      // ...
    ],
    "course_points": [
      {
        "x": -122.69944,
        "y": 45.58708,
        "d": 87.9,
        "i": 0,
        "t": "Right",
        "n": "Turn right onto North Houghton Street"
      },
      {
        "x": -122.70224,
        "y": 45.58709,
        "d": 306,
        "i": 3,
        "t": "Left",
        "n": "Turn slight left onto North Hamlin Avenue"
      },
      // ...
    ],
    "points_of_interest": [
      {
        "id": 1,
        "type_id": 24,
        "type_name": "Convenience Store",
        "name": "Seven Eleven",
        "description": "Get snacks on the way home.",
        "url": null,
        "lat": 45.561964,
        "lng": -122.68902
      },
      // ...
    ]
  }
}
```

If the authenticated user does not have permission to view the route a `403 - Forbidden` error is returned.
