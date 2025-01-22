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
        "type": "convenience_store",
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

They are exposed with one of the following `type`, `type_id` and `type_name`:

| Type                | Type ID | Type name          |
|:------------------- |:------- |:------------------ |
| camping             | 3       | Camping            |
| lodging             | 10      | Lodging            |
| parking             | 12      | Parking            |
| food                | 13      | Food               |
| viewpoint           | 14      | Viewpoint          |
| restroom            | 15      | Restroom           |
| generic             | 17      | Generic            |
| aid_station         | 20      | Aid Station        |
| bar                 | 21      | Bar                |
| bike_shop           | 22      | Bike Shop          |
| bike_parking        | 23      | Bike Parking       |
| convenience_store   | 24      | Convenience Store  |
| first_aid           | 25      | First Aid          |
| hospital            | 26      | Hospital           |
| rest_stop           | 27      | Rest Stop          |
| trailhead           | 28      | Trailhead          |
| geocache            | 29      | Geocache           |
| water               | 30      | Water              |
| control             | 31      | Control            |
| winery              | 32      | Winery             |
| start               | 33      | Start              |
| stop                | 34      | Stop               |
| finish              | 35      | Finish             |
| atm                 | 36      | ATM                |
| caution             | 37      | Caution            |
| coffee              | 38      | Coffee             |
| ferry               | 39      | Ferry              |
| gas                 | 40      | Gas Station        |
| library             | 41      | Library            |
| monument            | 42      | Monument           |
| park                | 43      | Park               |
| segment_start       | 44      | Segment Start      |
| segment_end         | 45      | Segment End        |
| shopping            | 46      | Shopping           |
| shower              | 47      | Shower             |
| summit              | 48      | Summit             |
| swimming            | 49      | Swimming           |
| transit             | 50      | Transit Center     |
| bikeshare           | 51      | Bike Share         |
