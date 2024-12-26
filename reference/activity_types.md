# Activity Types

> [!IMPORTANT]
> As of early 2025, the activity types listed below should be considered "beta" and are still subject to changes.

`activity_type` is a trip attribute whose value is determined from the trip FIT file, and/or by the gear used for the trip. It takes one of the following values:

```
cycling:generic
cycling:road
cycling:gravel
cycling:cyclocross
cycling:mountain
cycling:recumbent
cycling:hand_cycling
cycling:commute
cycling:indoor
cycling:virtual
e_biking:generic
e_biking:road
e_biking:mountain
running:generic
running:road
running:trail
running:indoor
walking:generic
walking:hiking
walking:indoor
walking:speed
swimming:generic
swimming:lap
swimming:open_water
snow:generic
snow:alpine_skiing
snow:cross_country_skiing
snow:snowboarding
snow:snowshoeing
driving:generic
motorcycling:generic
motorcycling:atv
motorcycling:motocross
training:generic
training:strength
training:cardio
training:breathing
training:yoga
training:hiit
other:generic
unknown:generic
```

## `fit_sport` and `fit_sub_sport`

You can get more details on the activity from the `fit_sport` and `fit_sub_sport` trip attributes. They conform to the FIT specification, given here for reference:

```
Type       Value  Name
---------  -----  -----------------------
sport          0  generic
sport          1  running
sport          2  cycling
sport          3  transition
sport          4  fitness_equipment
sport          5  swimming
sport          6  basketball
sport          7  soccer
sport          8  tennis
sport          9  american_football
sport         10  training
sport         11  walking
sport         12  cross_country_skiing
sport         13  alpine_skiing
sport         14  snowboarding
sport         15  rowing
sport         16  mountaineering
sport         17  hiking
sport         18  multisport
sport         19  paddling
sport         20  flying
sport         21  e_biking
sport         22  motorcycling
sport         23  boating
sport         24  driving
sport         25  golf
sport         26  hang_gliding
sport         27  horseback_riding
sport         28  hunting
sport         29  fishing
sport         30  inline_skating
sport         31  rock_climbing
sport         32  sailing
sport         33  ice_skating
sport         34  sky_diving
sport         35  snowshoeing
sport         36  snowmobiling
sport         37  stand_up_paddleboarding
sport         38  surfing
sport         39  wakeboarding
sport         40  water_skiing
sport         41  kayaking
sport         42  rafting
sport         43  windsurfing
sport         44  kitesurfing
sport         45  tactical
sport         46  jumpmaster
sport         47  boxing
sport         48  floor_climbing
sport         49  baseball
sport         53  diving
sport         62  hiit
sport         64  racket
sport         65  wheelchair_push_walk
sport         66  wheelchair_push_run
sport         67  meditation
sport         69  disc_golf
sport         71  cricket
sport         72  rugby
sport         73  hockey
sport         74  lacrosse
sport         75  volleyball
sport         76  water_tubing
sport         77  wakesurfing
sport         80  mixed_martial_arts
sport         82  snorkeling
sport         83  dance
sport         84  jump_rope
sport        254  all

Type       Value  Name                     Description
---------  -----  -----------------------  -----------------------------
sub_sport      0  generic
sub_sport      1  treadmill                Run/Fitness Equipment
sub_sport      2  street                   Run
sub_sport      3  trail                    Run
sub_sport      4  track                    Run
sub_sport      5  spin                     Cycling
sub_sport      6  indoor_cycling           Cycling/Fitness Equipment
sub_sport      7  road                     Cycling
sub_sport      8  mountain                 Cycling
sub_sport      9  downhill                 Cycling
sub_sport     10  recumbent                Cycling
sub_sport     11  cyclocross               Cycling
sub_sport     12  hand_cycling             Cycling
sub_sport     13  track_cycling            Cycling
sub_sport     14  indoor_rowing            Fitness Equipment
sub_sport     15  elliptical               Fitness Equipment
sub_sport     16  stair_climbing           Fitness Equipment
sub_sport     17  lap_swimming             Swimming
sub_sport     18  open_water               Swimming
sub_sport     19  flexibility_training     Training
sub_sport     20  strength_training        Training
sub_sport     21  warm_up                  Tennis
sub_sport     22  match                    Tennis
sub_sport     23  exercise                 Tennis
sub_sport     24  challenge
sub_sport     25  indoor_skiing            Fitness Equipment
sub_sport     26  cardio_training          Training
sub_sport     27  indoor_walking           Walking/Fitness Equipment
sub_sport     28  e_bike_fitness           E-Biking
sub_sport     29  bmx                      Cycling
sub_sport     30  casual_walking           Walking
sub_sport     31  speed_walking            Walking
sub_sport     32  bike_to_run_transition   Transition
sub_sport     33  run_to_bike_transition   Transition
sub_sport     34  swim_to_bike_transition  Transition
sub_sport     35  atv                      Motorcycling
sub_sport     36  motocross                Motorcycling
sub_sport     37  backcountry              Alpine Skiing/Snowboarding
sub_sport     38  resort                   Alpine Skiing/Snowboarding
sub_sport     39  rc_drone                 Flying
sub_sport     40  wingsuit                 Flying
sub_sport     41  whitewater               Kayaking/Rafting
sub_sport     42  skate_skiing             Cross Country Skiing
sub_sport     43  yoga                     Training
sub_sport     44  pilates                  Fitness Equipment
sub_sport     45  indoor_running           Run
sub_sport     46  gravel_cycling           Cycling
sub_sport     47  e_bike_mountain          Cycling
sub_sport     48  commuting                Cycling
sub_sport     49  mixed_surface            Cycling
sub_sport     50  navigate
sub_sport     51  track_me
sub_sport     52  map
sub_sport     53  single_gas_diving        Diving
sub_sport     54  multi_gas_diving         Diving
sub_sport     55  gauge_diving             Diving
sub_sport     56  apnea_diving             Diving
sub_sport     57  apnea_hunting            iving
sub_sport     58  virtual_activity
sub_sport     59  obstacle                 Used for events
sub_sport     62  breathing
sub_sport     65  sail_race                Sailing
sub_sport     67  ultra                    Ultramarathon
sub_sport     68  indoor_climbing          Climbing
sub_sport     69  bouldering               Climbing
sub_sport     70  hiit                     High Intensity Interval Training
sub_sport     73  amrap                    HIIT
sub_sport     74  emom                     HIIT
sub_sport     75  tabata                   HIIT
sub_sport     84  pickleball               Racket
sub_sport     85  padel                    Racket
sub_sport     86  indoor_wheelchair_walk
sub_sport     87  indoor_wheelchair_run
sub_sport     88  indoor_hand_cycling
sub_sport     94  squash
sub_sport     95  badminton
sub_sport     96  racquetball
sub_sport     97  table_tennis
sub_sport    110  fly_canopy               Flying
sub_sport    111  fly_paraglide            Flying
sub_sport    112  fly_paramotor            Flying
sub_sport    113  fly_pressurized          Flying
sub_sport    114  fly_navigate             Flying
sub_sport    115  fly_timer                Flying
sub_sport    116  fly_altimeter            Flying
sub_sport    117  fly_wx                   Flying
sub_sport    118  fly_vfr                  Flying
sub_sport    119  fly_ifr                  Flying
sub_sport    254  all
```
