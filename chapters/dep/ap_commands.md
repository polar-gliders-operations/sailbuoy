(autopilot)=
# Autopilot

(autopilot:timing)=
## Timing

The Autopilot does the following things in sequence:
1. Get GPS fix (10-20 s)
2. Get internal sensor values (1 s)
3. Calculate next tack (3 s)
4. Send data (30-120 s) 
5. Recieve commands (10 s)
6. Steer tack (rest of tack interval)

```{figure} img/time_ap.png
:name: Timing
```
(autopilot:basic)=
## Basic functionality

The SB uses the wind for propulsion, yet it does not control its sail, only the rudder. The SB has four possible sailing directions relative to the wind: 

```{figure} img/tack.png
:name: SB tack

```

```{figure} img/tack_wind.png
:name: Wind tack

The direction and speed of these tacks will vary according to the wind and wave conditions, but will always lie within the yellow sectors.

```

(autopilot:basic:tacking)=
### Tacking


When the SB changes direction it will always gybe, meaning it will lose some ground if going against the wind. If the interval is set too short (i.e., 5 min) it might lose more ground when turning than it will gain during each tack. This would result in a figure 8 at best, or losing ground completely.

```{figure} img/gybe1.png
:width: 75%
:align: left
```

```{figure} img/gybe2.png
:width: 75%
:align: left
```

```{figure} img/ex1.png
:width: 75%
:align: left

```

```{figure} img/ex2.png
:width: 75%
:align: left

: Some examples of how the Autopilot gybes and follows a given track in an ideal world.
```

---

(autopilot:basic:interval)=
### Tick interval
Considerations:
- Turning radius
- Transmission costs
- Power consumption

In practice the tack interval should be set to 15 minutes or more in AUTO mode but can be reduced to 5 minutes in manual mode.

(autopilot:basic:radius)=
### Track radius

The track radius defines the corridor width. If the SB is further than the track radius from the track defined by the start and end waypoints, it will try to get inside the corridor before travelling towards the end waypoint. When outside the defined corridor the SB will choose a course that is perpendicular to the track.


```{figure} img/track_radius.png
:name: track radius

```

(autopilot:basic:restarting)=
### Restarting

The Autopilot can be restarted at any point in time without damaging the electronics. To restart the Autopilot first switch it off with the magnetic switch, wait 60 seconds, then remove the magnetic switch to start again. After this it will return back all settings to default.

(autopilot:basic:sail_position)=
### Sail position

The sail position is included in the message transmitted from the Autopilot. The three values **SailAtPort**, **SailInCentre**, and **SailAtStarboard** show the time spent in each position in percent. Normally, **SailAtPort** + **SailInCentre** + **SailAtStarboard** = **100\%**. The values **SailAtPortBow** and **SailAtStarboardBow** represents when the sail is past 90 degrees from the aft, on either side. This is indicative of storms, when waves and wind can force the sail outside the normal travel scope. 


```{figure} img/sail_position.png
:name: sail position

```

(autopilot:commands)=
## Commands

| Command | No Parameters | Description | Default | Min | Max | Example |
| --- | --- | --- | --- | --- | --- | --- |
| **[](autopilot:commands:taint)** | 1 | Tack interval in seconds | 300 | 300 | 3600 | [](autopilot:commands:taint) 1800 |
| **[](autopilot:commands:timin)** | 1 | Tack interval in minutes | 5 | 5 | 60 | [](autopilot:commands:timin) 10 |
| **[](autopilot:commands:strwp)** | 2 | Set start waypoint | - |  |  | [](autopilot:commands:strwp) 66.54 5.543 |
| **[](autopilot:commands:endwp)** | 2 | Set end waypoint | - |  |  | [](autopilot:commands:endwp) 65.54 2.543 |
| **[](autopilot:commands:rad)** | 1 | Corridor radius in meters| 5000 | 100 |  | [](autopilot:commands:rad) 2000 |
| **[](autopilot:commands:auto)** | 0 | Engage autopilot | On |  |  | [](autopilot:commands:auto) |
| **[](autopilot:commands:tack)** | 1 | Steer tack (disengages autopilot) | - | 0 | 3 | [](autopilot:commands:tack) 1 |
| **[](autopilot:commands:wprad)** | 1 | Waypoint reached radius | 1000 | 0 |  | [](autopilot:commands:wprad) 1000 |
| **[](autopilot:commands:swpmd)** | 1 | Enable fence mode | Off | 0 | 1 | [](autopilot:commands:swpmd) 1 |

---
(autopilot:commands:taint)=
### \$TAINT
Description: Tack interval in seconds <br>
No. of parameters: 1 <br>
Parameter type: integer <br>
Unit: seconds <br>
Minimum parameter value: 300 <br>
Maximum parameter value: 3600 <br>
Example: $TAINT 900 <br>

Sets the tack interval in seconds. [\$TAINT 900](autopilot:commands:taint) will set the tack interval to 15 minutes. This means that every 30 min the autopilot will exit steer tack mode, get new GPS fix and select a new tack. If a short tack interval is set, say [$TAINT 300](autopilot:commands:taint), a new tack will be selected every 5 min. This can affect the performance since it will turn quite often and lose ground in every turn. The best performance is achieved when the tack interval is 30 min. Most of the power consumption is when the GPS and iridium modems are active, therefore a 5-minute tack interval will use around 6 times as much power as a 30 min. tack interval. 
A 5-minute tack interval is useful in manual mode when deploying or retrieving since the position is updated every 5 minutes. 

:::{Caution}
The tack interval can have the following values: 300, 600, 900, 1800, 3600. Other values might lead to unexpected behavior.
:::

---

(autopilot:commands:timin)=
### \$TIMIN
Description: Tack interval in minutes<br>
No. of parameters: 1 <br>
Parameter type: Float <br>
Unit: minutes <br>
Minimum parameter value: 5 <br>
Maximum parameter value: 60 <br>
Example: \$TIMIN 10 <br>

Sets the tack interval in minutes. This is an alternative to [](autopilot:commands:taint) but uses minutes instead of seconds. See the [](autopilot:commands:taint).

---

(autopilot:commands:strwp)=
### $STRWP
Description: Start waypoint <br>
No. of parameters: 2 <br>
Parameter type: Floating point <br>
Unit: decimal degrees <br>
Minimum parameter value: -180.0 <br>
Maximum parameter value: 180.0 <br>
Example: \$STRWP 65.1232 -5.23423 <br>

Sending this parameter sets the start waypoint on the autopilot. The autopilot will use this coordinate to calculate tacks to follow the line defined by start waypoint and end waypoint.

---

(autopilot:commands:endwp)=
### \$ENDWP
Description: End waypoint <br>
No. of parameters: 2 <br>
Parameter type: Floating point <br>
Unit: decimal degrees <br>
Minimum parameter value: -180.0 <br>
Maximum parameter value: 180.0 <br>
Example: \$ENDWP 65.1232 -5.23423 <br>

Sending this parameter sets the end waypoint on the autopilot. The autopilot will use this coordinate to calculate tacks to follow the line defined by start waypoint and end waypoint. The autopilot will follow the great circle route between the waypoints. The distance between the waypoints can be from 0 meters to thousands of kilometers. It is advisable to send both the start and the end waypoint in the same message or else it is easy to lose track of the autopilot setting.

:::{Note}
Both the [](autopilot:commands:strwp) and [](autopilot:commands:endwp) require the latitude first and longitude second, in decimal degrees (DD.dddd)
:::

---

(autopilot:commands:rad)=
### \$RAD 
Description: Track radius <br>
No. of parameters: 1 <br>
Parameter type: integer <br>
Unit: meters <br>
Minimum parameter value: 0 <br>
Maximum parameter value: - <br>
Example: $RAD 5000 <br>

Sending this parameter sets track radius in meters. Sending the command [$RAD 5000](autopilot:commands:rad) will set the track radius to 5 km. The corridor with will then be 10 km. Track radius is the distance the autopilot can veer away from the ideal track. If the autopilot is further away from the ideal track than the track radius, it will only try to get back inside the corridor, ignoring the end waypoint. Once inside the corridor it will resume following the ideal track again.

---

(autopilot:commands:auto)=
### \$AUTO
Description: Engage autopilot <br>
No. of parameters: 0 <br>
Parameter type: - <br>
Unit: - <br>
Minimum parameter value: - <br>
Maximum parameter value: - <br>
Example: \$AUTO <br>

Sending this command reengages the autopilot after using manual mode. The autopilot will the control the Sailbuoy and select the best tacks to follow the corridoor defined by [](autopilot:commands:strwp), [](autopilot:commands:endwp) and [](autopilot:commands:rad).

---

(autopilot:commands:tack)=
### \$TACK
Description: Steer tack <br>
No. of parameters: 1 <br>
Parameter type: integer <br>
Unit: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 3 <br>
Example: \$TACK 2 <br>

Sending this command overrides the autopilot tacks, telling the autopilot to steer a certain tack. For example, sending the command [$TACK 2](autopilot:commands:tack) will tell the autopilot to steer tack 2 indefinitely until a new command is sent. This way of controlling the autopilot is called manual mode. This mode is mostly used during deployment and retrieval to ensure that the Sailbuoy behaves in a predictable manner. To enter automatic mode again, send the command [](autopilot:commands:auto).

:::{Warning}
This command **DISABLES** the autopilot mode, must send [](autopilot:commands:auto) again to re-engage.
:::

---

(autopilot:commands:wprad)=
### \$WPRAD
Description: Waypoint reached radius <br>
No. of parameters: 1 <br>
Parameter type: integer <br>
Unit: meters <br>
Minimum parameter value: 0 <br>
Maximum parameter value: - <br>
Example: \$WPRAD 2000 <br>

Sending this command tells the autopilot when the end waypoint is reached. The autopilot only uses this parameter in fence mode. The autopilot checks if its current position is within the circle defined by this radius around the end waypoint. If it is then the end waypoint is reached. For example, sending [\$WPRAD 2000](autopilot:commands:wprad) will tell the autopilot that the waypoint is reached when the Sailbuoys GPS position is closer than 2 km from the end waypoint. This command is used in fence mode telling the autopilot when to turn around. Sending the command [\$WPRAD 0](autopilot:commands:wprad) will tell the autopilot to get as close to the end waypoint as possible before turning around in fence mode.

---

(autopilot:commands:swpmd)=
### \$SWPMD
Description: Switch waypoint mode (fence mode) <br>
No. of parameters: 1 <br>
Parameter type: integer <br>
Unit: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 1 <br>
Example: \$SWPMD 1 <br>

Sending this command tells the autopilot what to do when it reaches the end waypoint (see [](autopilot:commands:wprad)). [\$SWPMD 0](autopilot:commands:swpmd) will tell the autopilot to stay at the end waypoint until further notice (i.e. new commands are sent) while [\$SWPMD 1](autopilot:commands:swpmd) tells the autopilot to swap the start and end waypoint causing the Sailbuoy to head back towards the original start waypoint. When it arrives at this new end waypoint, it will swap waypoints again causing it to turn back. It will keep doing this back and forth until told otherwise.

(autopilot:modes)=
## Autopilot modes

(autopilot:modes:follow_track)=
### Follow track mode

This is the default mode where the SB follows an ideal track from its current position to a waypount. <br>
<br>
Example commands: <br>
[](autopilot:commands:strwp) -53.5 0 <br>
[](autopilot:commands:endwp) -54.5 0 <br>
[](autopilot:commands:rad) 5000 <br>

A **non-repeating** transect from 53.5°S, 0°E to 54.5°S, 0°E with a corridor radius of 5000 meters.

```{figure} img/track_mode.png
:width: 100%
:name: track mode
```

(autopilot:modes:station_keep)=
### Station keeping mode

This is the default mode when the SB has reached its waypount. In the example above, this is the expected behavior when reaching the location determined by [](autopilot:commands:endwp).

```{figure} img/station.png
:width: 25%
:name: station mode
:align: center
```

(autopilot:modes:fence_mode)=
### Fence mode

In this mode the SB travels between 2 waypoints. We add the command [\$SWPMD 1](autopilot:commands:swpmd), which tells it to swap waypoints once reaching the location determined by [](autopilot:commands:endwp). The previous [](autopilot:commands:strwp) now becomes [](autopilot:commands:endwp) and vice versa. We also add the command [\$WPRAD 2000](autopilot:commands:wprad) which sets the `reached waypoint` radius to 2 km. 

```{figure} img/fence_mode.png
:width: 50%
:name: fence mode
```

Example commands: <br>
[](autopilot:commands:strwp) -53.5 0 <br>
[](autopilot:commands:endwp) -54.5 0 <br>
[](autopilot:commands:rad) 5000 <br>
[](autopilot:commands:swpmd) 1 <br>
[](autopilot:commands:wprad) 2000 <br>
<br>

A **repeating** transect from 53.5°S, 0°E to 54.5°S, 0°E with a corridor radius of 5000 meters.

---

(autopilot:modes:sochic)=
### Real world data

```{figure} img/sb_wind_vel.png
:width: 100%

 Sailbuoy velocity as a function of wind speed and difference between Sailbuoy heading and wind direction. Negative values on the x-axis indicates the the wind is coming from the starboard side, and vice versa. 

```



---

(autopilot:modes:manual)=
### Manual mode

Manual control will override the autopilots next calculated tack. When the command “[](autopilot:commands:tack) 0” is sent to the
autopilot, upon receiving the command it will steer on tack 0 and ignore the tacks calculated by the autopilot. One can send the following commands to steer manually: <br>
[](autopilot:commands:tack) 0 <br>
[](autopilot:commands:tack) 1 <br>
[](autopilot:commands:tack) 2 <br>
[](autopilot:commands:tack) 3 <br>

Sending the command [](autopilot:commands:auto) will end manual mode and revert to the autopilot mode.

(autopilot:data_fields)=
## Data fields

In the Autopilot data tab the following columns are displayed:

| Parameter name | Description | Unit |
| --- | --- | --- |
| Time | Start time for each tack. | Time UTC |
| Lat | Latitude in decimal degrees | decimal degrees |
| Long | Longitude in decimal degrees | decimal degrees |
| TTFF | Time to first fix. The time in seconds the GPS uses to obtain a valid position. | seconds |
| Warning | Warning indicator. Indicates that the pilot has to pay attention to the Sailbuoy status. | True/False |
| Count | Tack counter. For each tack this counter is incremented. It rolls over after a set number of tacks. | integer |
| Leak | Leak switch indicator. Indicates a leak in the hull. | True/False |
| Commands | Received commands count. Shows the number of command values received and processed on the previous transmission. | integer |
| I | Current consumption after GPS fix. | A |
| V | Battery voltage. Shows the battery voltage. >13.4 fully charged. Maximum voltage is 14.2 volts when charging. <br> 13.0 V ~ 50\% charged. <br> 12.8 V ~ 15\% charged. | V |
| Temperature | Payload temperature. The internal temperature of the payload container. | °C |
| Pressure | Payload pressure. The internal pressure of the payload container. | hPa |
| Humidity | Payload humidity. The humidity of the payload container. If this value increases it can indicate a leak in the payload container. | \% |
| TransmissionTries | Iridium transmission tries. Shows the number of transmissions tries on the previous transmission. This is normally set to 3 and if this value is 3 it is due to 3 tries end success or 3 tries and fail. | integer |
| OnTimeSec |  | seconds |
| Velocity | Velocity over ground. The velocity calculated from the previous GPS position. | m/s |
| Heading | GPS tack direction. Direction calculated from the previous GPS position. | deg |
| TrackDistance | Distance from the line defined by the start and end waypoint. If no value (NULL) the distance is greater than 24 km. | m |
| WaypointDirection | The direction for the current position to the end waypoint. | deg |
| TrackRadius | The radius of the corridor set by the \$RAD command | m |
| WindDirection | Calculated wind direction. The wind direction is calculated based on the behavior of the Sailbuoy on different tacks. The wind direction is recalculated when changing from Tack 0 to 1 or from tack 2 to 3. The autopilot uses this value to calculate the next tack. | deg |
| AutoModeEnabled | Indicates if the autopilot is controlling the navigation. AutoModeEnabled = 0 if in manual mode | True/False |
| SwitchWaypointModeEnabled | Is true if fence mode is enabled. Set by the \$SWPMD command | True/False |
| NextAutopilotTack | The next autopilot tack. This is the next tack chosen by the autopilot. When in manual mode this tack will be overridden by the manual tack. | integer |
| CurrentTack | The current tack sailed | integer |
| PreviousTack, T1, T2, T3 | Previous tacks | integer |
| WPReached | Waypoint reached | True/False |
| WithinTrackRadius | Within corridor | True/False |
| SailAtPortBow | Sail past 90 deg to port count | \% |
| SailAtPort | Sail at port count | \% |
| SailInCentre | Sail in middle count | \% |
| SailAtStarboard | Sail at starboard count | \% |
| SailAtStarboardBow | Sail past 90 deg to starboard count | \% |

