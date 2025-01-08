# Points of interest API endpoints for organizations

> [!WARNING]  
> These API endpoints are deprecated and will be removed in the future. Please use our [new endpoints](./points_of_interest.md)

## Authentication

Requests to the endpoints below must authenticated with the following headers:

```
x-rwgps-api-key: <api_key>
x-rwgps-auth-token: <auth_token>
```

An `api_key` and `auth_token` for your organization will be provided to you by Ride with GPS.

## Create a point of interest

Create a new point of interest with a `POST` request:

```javascript
// POST https://ridewithgps.com/organizations/<organization_id>/points_of_interest.json
{
  "point_of_interest": {
    "name": "Point Of Interest",
    "poi_type": 17,
    "tag_names": [],
    "description": null,
    "url": null,
    "lat": 44.470349,
    "lng": -122.647507
  }
}
```

The response is a JSON representation of the point of interest that was created, including its `id`:

```javascript
{
  "point_of_interest": {
    "id": 1,
    "user_id": 1,
    "visibility": 0,
    "poi_type": 17,
    "lng": -122.647507,
    "lat": 44.470349,
    "name": "Point Of Interest",
    "url": null,
    "description": null,
    "created_at": "2024-05-24T19:05:55-07:00",
    "updated_at": "2024-05-24T19:05:55-07:00",
  }
}
```

## Retrieve a point of interest

Retrieve an existing point of interest with a `GET` request at its URL:


```javascript
// GET https://ridewithgps.com/organizations/<organization_id>/points_of_interest/<id>.json
```

The response is a JSON representation of the point of interest.

## Update a point of interest

Update a point of interest with a `PATCH` request at its URL:

```javascript
// PATCH https://ridewithgps.com/organizations/<organization_id>/points_of_interest/<id>.json
{
  "point_of_interest": {
    "name": "Point Of Interest Updated",
    "poi_type": 17,
    "tag_names": [],
    "description": null,
    "url": null,
    "lat": 44.470349,
    "lng": -122.647507
  }
}
```

The payload can include only the keys that need to be updated.

The response is an updated JSON representation of the Point Of Interest.

## Batch delete points of interest

Delete points of interest in batch by specifying their IDs in a `POST` request:

```javascript
// POST https://ridewithgps.com/organizations/<organization_id>/points_of_interest/batch_destroy.json
{
  poi_ids: [ 1, 2 ]
}
```

The response includes the JSON representation of each deleted point of interest.

## Points of interest types

Ride with GPS supports the following types for points of interest:

```javascript
[
  { "id": 3, "name": "camping" },
  { "id": 10, "name": "lodging" },
  { "id": 12, "name": "parking" },
  { "id": 13, "name": "food" },
  { "id": 14, "name": "viewpoint" },
  { "id": 15, "name": "restroom" },
  { "id": 17, "name": "generic" }, // default type
  { "id": 20, "name": "aid_station" },
  { "id": 21, "name": "bar" },
  { "id": 22, "name": "bike_shop" },
  { "id": 23, "name": "bike_parking" },
  { "id": 24, "name": "convenience_store" },
  { "id": 25, "name": "first_aid" },
  { "id": 26, "name": "hospital" },
  { "id": 27, "name": "rest_stop" },
  { "id": 28, "name": "trailhead" },
  { "id": 29, "name": "geocache" },
  { "id": 30, "name": "drinking_water" },
  { "id": 31, "name": "control" },
  { "id": 32, "name": "winery" },
  { "id": 33, "name": "start" },
  { "id": 34, "name": "stop" },
  { "id": 35, "name": "finish" },
  { "id": 36, "name": "atm" },
  { "id": 37, "name": "caution" },
  { "id": 38, "name": "coffee" },
  { "id": 39, "name": "ferry" },
  { "id": 40, "name": "gas" },
  { "id": 41, "name": "library" },
  { "id": 42, "name": "monument" },
  { "id": 43, "name": "park" },
  { "id": 44, "name": "segment_start" },
  { "id": 45, "name": "segment_end" },
  { "id": 46, "name": "shopping" },
  { "id": 47, "name": "shower" },
  { "id": 48, "name": "summit" },
  { "id": 49, "name": "swimming" },
  { "id": 50, "name": "transit" },
  { "id": 51, "name": "bikeshare" }
]
```
