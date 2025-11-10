# Routes and trips attributes

Attributes exposed by the API for routes and trips:

| Attribute             | Description                                 | Type    | Unit              | Route | Trip  |
|:--------------------- |:------------------------------------------- |:------- |:----------------- |:-----:|:-----:|
| `id`                  | Ride with GPS identifier                    | Integer | n/a               | Y     | Y     |
| `url`                 | Public API URL                              | String  | n/a               | Y     | Y     |
| `name`                | Name                                        | String  | n/a               | Y     | Y     |
| `visibility`          | Visibility [^1]                             | String  | n/a               | Y     | Y     | 
| `description`         | Description                                 | String  | n/a               | Y     | Y     |
| `departed_at`         | Trip departed timestamp ISO 8601            | String  | n/a               |       | Y     |
| `time_zone`           | Timezone for `departed_at`                  | String  | n/a               |       | Y     |
| `locality`            | Locality of first track point               | String  | n/a               |       | Y     |
| `administrative_area` | Admin area of first track point             | String  | n/a               |       | Y     |
| `country_code`        | Country of first track point                | String  | n/a               | Y     | Y     |
| `activity_type`       | [Activity types](activity_types.md)         | String  | n/a               |       | Y     |
| `fit_sport`           | [Fit sports](activity_types.md)             | Integer | n/a               |       | Y     |
| `fit_sub_sport`       | [Fit sub sports](activity_types.md)         | Integer | n/a               |       | Y     |
| `is_stationary`       | Indicates a stationary trip                 | Boolean | n/a               |       | Y     |
| `distance`            | Total distance                              | Integer | meters            | Y     | Y     |
| `duration`            | Total duration                              | Integer | seconds           |       | Y     |
| `moving_time`         | Moving time                                 | Integer | seconds           |       | Y     |
| `elevation_gain`      | Total elevation gain                        | Integer | meters            | Y     | Y     |
| `elevation_loss`      | Total elevation loss                        | Integer | meters            | Y     | Y     |
| `first_lat`           | First point latitude                        | Float   | degrees           | Y     | Y     |
| `first_lng`           | First point longitude                       | Float   | degrees           | Y     | Y     |
| `last_lat`            | Last point latitude                         | Float   | degrees           | Y     | Y     |
| `last_lng`            | Last point longitude                        | Float   | degrees           | Y     | Y     |
| `sw_lat`              | Track SW corner latitude                    | Float   | degrees           | Y     | Y     |
| `sw_lng`              | Track SW corner longitude                   | Float   | degrees           | Y     | Y     |
| `ne_lat`              | Track NE corner latitude                    | Float   | degrees           | Y     | Y     |
| `ne_lng`              | Track NE corner longitude                   | Float   | degrees           | Y     | Y     |
| `track_type`          | Type of track [^2]                          | String  | n/a               | Y     | Y     |
| `terrain`             | Type of terrain [^3]                        | String  | n/a               | Y     | Y     |
| `difficulty`          | Overall difficult [^4]                      | String  | n/a               | Y     | Y     |
| `unpaved_pct`         | Percentage of unpaved points                | Integer | n/a               | Y     |       |
| `surface`             | Surface type [^5]                           | String  | n/a               | Y     |       |
| `avg_speed`           | Average speed                               | Float   | kilometers / hour |       | Y     |
| `max_speed`           | Maximum speed                               | Float   | kilometers / hour |       | Y     |
| `avg_cad`             | Average cadence                             | Integer | rounds / minute   |       | Y     |
| `min_cad`             | Minimum cadence                             | Integer | rounds / minute   |       | Y     |
| `max_cad`             | Maximum cadence                             | Integer | rounds / minute   |       | Y     |
| `avg_hr`              | Average heart rate                          | Integer | beats / minute    |       | Y     |
| `min_hr`              | Minimum heart rate                          | Integer | beats / minute    |       | Y     |
| `max_hr`              | Maximum heart rate                          | Integer | beats / minute    |       | Y     |
| `avg_watts`           | Average power                               | Integer | watts             |       | Y     | 
| `min_watts`           | Minimum power                               | Integer | watts             |       | Y     |
| `max_watts`           | Maximum power                               | Integer | watts             |       | Y     |
| `calories`            | Calories burnt                              | Integer | calories          |       | Y     |
| `created_at`          | Creation date ISO 8601                      | String  | n/a               | Y     | Y     |
| `updated_at`          | Last update date ISO 8601                   | String  | n/a               | Y     | Y     |
| `device`              | Manufacturer and name of recording device   | String  | n/a               |       | Y     |
| `track_points`        | [Track points](track_points.md)             | Array   | n/a               | Y     | Y     |
| `course_points`       | [Course points](track_points.md)            | Array   | n/a               | Y     |       |
| `points_of_interest`  | [Points of interest](points_of_interest.md) | Array   | n/a               | Y     |       |

> [!NOTE]
> `track_points`, `course_points` and `points_of_interest` are only given when requesting a specific record.
> These attributes are not given in the responses of requests for a collection of records.

[^1]: `visibility` is one of `public`, `friends_only`, `private`
[^2]: `track_type` is one of `loop`, `out_and_back`, `point_to_point`, `unknown`
[^3]: `terrain` is one of `flat`, `rolling`, `climbing`
[^4]: `difficulty` is one of `casual`, `easy`, `moderate`, `hard`, `multi_day`
[^5]: `surface` is one of `paved`, `mostly_paved`, `mixed_surfaces`, `mostly_unpaved`, `unknown`
