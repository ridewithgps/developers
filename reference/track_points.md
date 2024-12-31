# Track points and course points attributes

A track is described by many track points, each track point having (usually) at least a longitude (`x`) and a latitude (`y`), so it can be drawn on a map.

When a trip is recorded, the device (Ride with GPS mobile app or a bike computer) records track points at fixed frequency (at best 1Hz, 1 point per second) with their coordinates, and potentially many other attributes like the current speed, cadence, power or ambiant temperature.

When a route is planned, enough track points are recorded to properly describe the track. The route track points might also include attributes like elevation or surface type.

Course points are present on routes only, they are the cues that form a cuesheet for the route. Course points have coordinates (`x` and `y`), but also directional attributes ("Turn left on 2nd avenue"). Course points are automatically generated for a route when it is auto-traced, and can also be customized by the user.

**Attributes**

Attributes exposed by the API for `course_points` and `track_points`:

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

