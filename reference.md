# Reference

## Route and trip attributes

Attributes exposed by the API for routes and trips:

| Attribute        | Description                          | Type    | Unit              | Route | Trip  |
|:---------------- |:------------------------------------ |:------- |:----------------- |:-----:|:-----:|
| `first_lat`      | First point latitude                 | Float   | degrees           | Y     | Y     |
| `first_lng`      | First point longitude                | Float   | degrees           | Y     | Y     |
| `last_lat`       | Last point latitude                  | Float   | degrees           | Y     | Y     |
| `last_lng`       | Last point longitude                 | Float   | degrees           | Y     | Y     |
| `sw_lat`         | Bounding box SW corner latitude      | Float   | degrees           | Y     | Y     |
| `sw_lng`         | Bounding box SW corner longitude     | Float   | degrees           | Y     | Y     |
| `ne_lat`         | Bounding box NE corner latitude      | Float   | degrees           | Y     | Y     |
| `ne_lng`         | Bounding box NE corner longitude     | Float   | degrees           | Y     | Y     |
| `distance`       | Total distance                       | Integer | meters            | Y     | Y     |
| `elevation_gain` | Total elevation gain                 | Integer | meters            | Y     | Y     |
| `elevation_loss` | Total elevation loss                 | Integer | meters            | Y     | Y     |
| `track_type`     | Type of track                        | String  | n/a               | Y     | Y     |
| `terrain`        | Type of terrain                      | String  | n/a               | Y     | Y     |
| `difficulty`     | Overall difficult                    | String  | n/a               | Y     | Y     |
| `unpaved_pct`    | Unpaved percentage                   | Integer | n/a               | Y     |       |
| `surface`        | Inferred surface                     | String  | n/a               | Y     |       |
| `is_stationary`  | Indicated is the trip is stationary  | Boolean | n/a               |       | Y     |
| `duration`       | Total duration                       | Integer | seconds           |       | Y     |
| `moving_time`    | Moving time                          | Integer | seconds           |       | Y     |
| `avg_speed`      | Average speed                        | Float   | kilometers / hour |       | Y     |
| `max_speed`      | Maximum speed                        | Float   | kilometers / hour |       | Y     |
| `avg_cad`        | Average cadence                      | Integer | rounds / minute   |       | Y     |
| `min_cad`        | Minimum cadence                      | Integer | rounds / minute   |       | Y     |
| `max_cad`        | Maximum cadence                      | Integer | rounds / minute   |       | Y     |
| `avg_hr`         | Average heart rate                   | Integer | beats / minute    |       | Y     |
| `min_hr`         | Minimum heart rate                   | Integer | beats / minute    |       | Y     |
| `max_hr`         | Maximum heart rate                   | Integer | beats / minute    |       | Y     |
| `avg_watts`      | Average power                        | Integer | watts             |       | Y     | 
| `min_watts`      | Minimum power                        | Integer | watts             |       | Y     |
| `max_watts`      | Maximum power                        | Integer | watts             |       | Y     |
| `calories`       | Calories burnt                       | Integer | calories          |       | Y     |

* `track_type` is one of `loop`, `out_and_back`, `point_to_point`, `unknown`
* `terrain` is one of `flat`, `rolling`, `climbing`
* `difficulty` is one of `casual`, `easy`, `moderate`, `hard`, `multi_day`
* `surface` is one of `paved`, `mostly_paved`, `mixed_surfaces`, `mostly_unpaved unknown`

## Track and course points

A track is described by many track points, each track point having (usually) at least a longitude (`x`) and a latitude (`y`), so it can be drawn on a map.

When a trip is recorded, the device (Ride with GPS mobile app or a bike computer) records track points at fixed frequency (at best 1Hz, 1 point per second) with their coordinates, and potentially many other attributes like the current speed, cadence, power or ambiant temperature.

When a route is planned, enough track points are recorded to properly describe the track. The route track points might also include attributes like elevation or surface type.

Course points are present on routes only, they are the cues that form a cuesheet for the route. Course points have coordinates (`x` and `y`), but also directional attributes ("Turn left on 2nd avenue"). Course points are automatically generated for a route when it is auto-traced, and can also be customized by the user.

**Attributes**

Attributes exposed by the API for course points and track points:

| Attribute  | Description           | Type    | Unit              | Route<br>track points | Route<br>course points | Trip<br>track points |
|:---------- |:--------------------- |:------- |:----------------- |:---------------------:|:----------------------:|:--------------------:|
| `x`        | Longitude             | Float   | degrees           | Y                     | Y                      | Y                    |
| `y`        | Latitude              | Float   | degrees           | Y                     | Y                      | Y                    |
| `d`        | Distance from start   | Integer | meters            | Y                     | Y                      | Y                    |
| `e`        | Elevation             | Integer | meters            | Y                     |                        | Y                    |
| `S`        | Surface type          | Int     | n/a               | Y                     |                        |                      |
| `R`        | Highway tag           | Int     | n/a               | Y                     |                        |                      |
| `i`        | Cue track index       | String  | n/a               |                       | Y                      |                      |
| `t`        | Type of cue           | String  | n/a               |                       | Y                      |                      |
| `n`        | Cue text              | String  | n/a               |                       | Y                      |                      |
| `_e`       | User edited cue       | Boolean | n/a               |                       | Y                      |                      |
| `t`        | Unix epoch time       | Int     | seconds           |                       |                        | Y                    |
| `s`        | Speed                 | Float   | kilometers / hour |                       |                        | Y                    |
| `T`        | Temperature           | Int     | degrees celsius   |                       |                        | Y                    |
| `h`        | Heart rate            | Int     | beats / minute    |                       |                        | Y                    |
| `c`        | Cadence               | Int     | rounds / minute   |                       |                        | Y                    |
| `p`        | Power output          | Int     | watts             |                       |                        | Y                    |
| `pb`       | Power balance         | Int     | percent L/R       |                       |                        | Y                    |
| `lap`      | Start of lap          | Boolean | n/a               |                       |                        | Y                    |
| `k`        | Exclude from metrics  | Boolean | n/a               |                       |                        | Y                    |
| `m`        | User modified         | Boolean | n/a               |                       |                        | Y                    |

## Points of interest

Points of interest are provided by the user and are present for routes only. They are exposed through the API with one of the following `type_id` and `type_name`.

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

## Activity types

Actvity types exposed by the API:

| Activity Type          |
|:---------------------- |
| cycling                |
| road_cycling           |
| gravel_unpaved_cycling |
| mountain_biking        |
| indoor_cycling         |
| ebiking                |
| emountain_biking       |
| running                |
| indoor_running         |
| trail_running          |
| walking                |
| hiking                 |
| motorcycling           |
| skiing                 |
| snowboarding           |
| swimming               |
| lap_swimming           |
| open_water_swimming    |
| horseback_riding       |
| other                  |
