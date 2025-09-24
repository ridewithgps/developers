# Trip endpoints

## GET /api/v1/trips.json

Returns a paginated list of trips owned by the authenticated user, ordered by `updated_at` descending.

**Request**

* **Method**: `GET`
* **URL**: `https://ridewithgps.com/api/v1/trips.json`
* **Authentication**: [Required](../authentication.md)
* **Query params**: 
  * `page=<page_number>` - Optional, used for [pagination](../README.md#pagination)

**Example response**

```javascript
// 200 - OK
{
  "trips": [
    {
      "id": 999,
      "url": "https://ridewithgps.com/api/v1/trips/1455.json",
      "name": "Last trip",
      // ...
    },
    {
      "id": 844,
      "url": "https://ridewithgps.com/api/v1/trips/1311.json",
      "name": "Another trip",
      // ...
    },
    // ...
  ],
  "meta": {
    "pagination": {
      "record_count": 22,
      "page_count": 1,
      "next_page_url": "https://ridewithgps.com/api/v1/trips.json?page=2"
    }
  }
}
```

Each trip in the response has all the attributes of the trip detail request below, except the `track_points` attribute.

## GET /api/v1/trips/:id.json

Returns a full representation of the trip identified by its `id`.

**Request**

* **Method**: `GET`
* **URL**: `https://ridewithgps.com/api/v1/trips/:id.json`
* **Authentication**: [Required](../authentication.md)

**Example Response**

```javascript
// GET https://ridewithgps.com/api/v1/trips/1.json
// 200 - OK
{
  "trip": {
    "id": 1,
    "url": "https://ridewithgps.com/api/v1/trips/1.json",
    "name": "Morning Ride",
    "description": null,
    "departed_at": "2008-01-05T11:25:03-08:00",
    "time_zone": "America/Los_Angeles",
    "locality": "Eugene",
    "administrative_area": "OR",
    "country_code": "US",
    "activity_type": "cycling:gravel",
    "fit_sport": 2,
    "fit_sub_sport": 46,
    "is_stationary": false,
    "distance": 16146,
    "duration": 2705,
    "moving_time": 2456,
    "elevation_gain": 363,
    "elevation_loss": 352,
    "first_lat": 44.012199,
    "first_lng": -123.073723,
    "last_lat": 44.012058,
    "last_lng": -123.073715,
    "sw_lat": 43.964836,
    "sw_lng": -123.107689,
    "ne_lat": 44.012199,
    "ne_lng": -123.073715,
    "avg_speed": 23.7,
    "max_speed": 49.3,
    "avg_cad": 77,
    "min_cad": 10,
    "max_cad": 115,
    "avg_hr": 163,
    "min_hr": 92,
    "max_hr": 238,
    "avg_watts": 289,
    "min_watts": null,
    "max_watts": null,
    "calories": 711,
    "track_type": "loop",
    "terrain": "climbing",
    "difficulty": "easy",
    "created_at": "2024-09-09T15:29:01-07:00",
    "updated_at": "2024-09-09T15:29:01-07:00",
    "track_points": [
      {
        "x": -123.073723,
        "y": 44.012199,
        "e": 158.2,
        "s": 0,
        "t": 1199561107,
        "h": 92,
        "c": 0
      },
      {
        "x": -123.073792,
        "y": 44.012196,
        "e": 156.8,
        "s": 2.27,
        "t": 1199561109,
        "h": 92,
        "c": 0
      },
      {
        "x": -123.073952,
        "y": 44.012169,
        "e": 152.9,
        "s": 3.06,
        "t": 1199561113,
        "h": 93,
        "c": 0
      }
      // ...
    ]
  }
}
```

If the authenticated user does not have permission to view the trip a `403 - Forbidden` error is returned.

## DELETE /api/v1/trips/:id.json

Delete a trip specifed by its `id`:

**Request**

* **Method**: `DELETE`
* **URL**: `https://ridewithgps.com/api/v1/trips/:id.json`
* **Authentication**: [Required](../authentication.md)

**Example Response**

```javascript
// 204 - No Content
```

**References**

* [Trip attributes](../reference/routes_and_trips.md)
* [Track points attributes](../reference/track_points.md)
