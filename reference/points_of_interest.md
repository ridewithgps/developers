# Points of interest attributes

`points_of_interest` is a route only attribute, present when requesting the details of a route:

```javascript
// GET https://ridewithgps.com/api/v1/routes/1.json
{
  "route": {
    "id": 1,
    // ...
    "points_of_interest": [
      {
        "id": 1,
        "type_id": 24,
        "type_name": "Convenience Store",
        "name": "Seven Eleven"
        "description": "Get snacks on the way home",
        "url": null,
        "lat": 45.561964,
        "lng": -122.68902
      },
      // ...
    ]
  }
}
```

They are exposed with one of the following `type_id` and `type_name`.

| Type ID | Type name          |
|:------- |:------------------ |
| 3       | Camping            |
| 10      | Lodging            |
| 12      | Parking            |
| 13      | Food               |
| 14      | Viewpoint          |
| 15      | Restroom           |
| 17      | Generic            |
| 20      | Aid Station        |
| 21      | Bar                |
| 22      | Bike Shop          |
| 23      | Bike Parking       |
| 24      | Convenience Store  |
| 25      | First Aid          |
| 26      | Hospital           |
| 27      | Rest Stop          |
| 28      | Trailhead          |
| 29      | Geocache           |
| 30      | Water              |
| 31      | Control            |
| 32      | Winery             |
| 33      | Start              |
| 34      | Stop               |
| 35      | Finish             |
| 36      | ATM                |
| 37      | Caution            |
| 38      | Coffee             |
| 39      | Ferry              |
| 40      | Gas Station        |
| 41      | Library            |
| 42      | Monument           |
| 43      | Park               |
| 44      | Segment Start      |
| 45      | Segment End        |
| 46      | Shopping           |
| 47      | Shower             |
| 48      | Summit             |
| 49      | Swimming           |
| 50      | Transit Center     |
| 51      | Bike Share         |
