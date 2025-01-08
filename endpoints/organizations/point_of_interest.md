# Point Of Interest endpoints

> [!IMPORTANT]  
> These API endpoints can only be used by a **club**. See [here](../../authentication.md#organization-accounts) to get access.


## GET /api/v1/points_of_interest.json

Returns a paginated list of points of interest in a club POI library, ordered by `updated_at` descending.

**Request**

* **Method**: `GET`
* **URL**: `https://ridewithgps.com/api/v1/points_of_interest.json`
* **Authentication**: [Required](../../authentication.md#organization-accounts)
* **Query params**: 
  * `page=<page_number>` - Optional, used for [pagination](../README.md#pagination)

**Example response**

```javascript
// 200 - OK
{
  "points_of_interest": [
    {
      "id": 13,
      "type_id": 32,
      "type_name": "Winery",
      "name": "Pinot Noir",
      "description": "Ode to",
      "url": null,
      "lat": 45.535239,
      "lng": -122.657811,
      "tag_names": [
        "foo"
      ]
    },
    {
      "id": 11,
      "type_id": 14,
      "type_name": "Viewpoint",
      "name": "Big Old Mountain",
      "description": "It's tall",
      "url": null,
      "lat": 0,
      "lng": 0,
      "tag_names": [
        "baz",
        "boo"
      ]
    },
   // ...
  ],
  "meta": {
    "pagination": {
      "record_count": 100,
      "page_count": 2,
      "next_page_url": "https://ridewithgps.com/api/v1/points_of_interest.json?page=2"
    }
  }
}
```

Note that tag names are returned in the response.

## GET /api/v1/points_of_interest/[id].json

Returns the point of interest identified by its `id`.

**Request**

* **Method**: `GET`
* **URL**: `https://ridewithgps.com/api/v1/points_of_interest/[id].json`
* **Authentication**: [Required](../../authentication.md#organization-accounts)
* **Successful Response Code**: 200

**Example Response**

```javascript
// GET https://ridewithgps.com/api/v1/points_of_interest/2.json
// 200 - OK
{
  "point_of_interest": {
    "id": 2,
    "type_id": 30,
    "type_name": "Water",
    "name": "Water Sucks! It really really sucks!",
    "description": "Gatorade not only quenches your thirst better, it tastes better!",
    "url": null,
    "lat": 45.514989,
    "lng": -122.67061,
    "tag_names": [
      "water"
    ]
  }
}
```

## PATCH /api/v1/points_of_interest/[id].json

Updates specific attributes of a point of interest by its `id`.

**Request**

* **Method**: `PATCH`
* **URL**: `https://ridewithgps.com/api/v1/points_of_interest/[id].json`
* **Authentication**: [Required](../../authentication.md#organization-accounts)
* **Successful Response Code**: 200
* **Body**: Example Updates
```json
{
  "point_of_interest": {
    "name": "Look I updated a POI!"
  }
}
```

**Example Response**

```javascript
// PATCH https://ridewithgps.com/api/v1/points_of_interest/3.json
// 200 - OK
{
  "point_of_interest": {
    "id": 3,
    "type_id": 30,
    "type_name": "Water",
    "name": "Look I updated a POI!",
    "description": null,
    "url": null,
    "lat": 45.514989,
    "lng": -122.67061,
    "tag_names": []
  }
}
```

## DELETE /api/v1/points_of_interest/[id].json

Deletes a point of interest by its `id`.

**Request**

* **Method**: `DELETE`
* **URL**: `https://ridewithgps.com/api/v1/points_of_interest/[id].json`
* **Authentication**: [Required](../../authentication.md#organization-accounts)
* **Successful Response Code**: 204

**Example Response**

```javascript
// DELETE https://ridewithgps.com/api/v1/points_of_interest/3.json
// 204 - OK
```

## POST /api/v1/points_of_interest.json

Creates a new point of interest. The following fields are **required**: `name`, `lat`, `lng`, `poi_type`.

**Request**

* **Method**: `POST`
* **URL**: `https://ridewithgps.com/api/v1/points_of_interest.json`
* **Authentication**: [Required](../../authentication.md#organization-accounts)
* **Successful Response Code**: 200
* **Body**: Example Create
```json
{
  "point_of_interest": {
    "name": "A new POI",
    "lat": 45.0,
    "lng": -75.0,
    "poi_type": 14,
    "description": "Updated!"
  }
}
```

**Example Response**

```javascript
// POST https://ridewithgps.com/api/v1/points_of_interest.json
// 200 - OK
{
  "point_of_interest": {
    "id": 4,
    "type_id": 14,
    "type_name": "Viewpoint",
    "name": "A new POI",
    "description": "Updated!",
    "url": null,
    "lat": 45,
    "lng": -75,
    "tag_names": []
  }
}
```

## POST /api/v1/points_of_interest/[id]/routes/[route_id].json

Adds a club poi in its library referenced by `id` to a club owned route referenced by `route_id`. We refer to this as associating a poi with a route.

**Request**

* **Method**: `POST`
* **URL**: `https://ridewithgps.com/api/v1/points_of_interest[id]/routes/[route_id].json`
* **Authentication**: [Required](../../authentication.md#organization-accounts)
* **Successful Response Code**: 204

**Example Response**

```javascript
// POST https://ridewithgps.com/api/v1/points_of_interest/3/routes/2.json
// 204 - No Content
```

## DELETE /api/v1/points_of_interest/[id]/routes/[route_id].json

Removes a club poi in its library referenced by `id` from a club owned route referenced by `route_id`. We refer to this as disassociating a poi from a route.

**Request**

* **Method**: `DELETE`
* **URL**: `https://ridewithgps.com/api/v1/points_of_interest[id]/routes/[route_id].json`
* **Authentication**: [Required](../../authentication.md#organization-accounts)
* **Successful Response Code**: 204

**Example Response**

```javascript
// DELETE https://ridewithgps.com/api/v1/points_of_interest/3/routes/2.json
// 204 - No Content
```



## Addendum

If the authenticated club does not have permission to view/create/update a point of interest a `403 - Forbidden` error is returned.

If a resource does not exists a `404 - Not Found` error is returned.

**References**

* [Points of interest attributes](../reference/points_of_interest.md)

