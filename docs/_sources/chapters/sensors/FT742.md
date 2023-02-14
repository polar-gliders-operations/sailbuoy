(sensors:FT742)=
# FT742 Wind sensor

The FT7 Series of ultrasonic wind sensors deliver highly accurate and consistent wind speed and direction data from compact sensors. With no moving parts, built-in heaters, and resistance to a wide range of environmental factors, the FT7 series sensors are maintenance-free and will last for years, even in the harshest of climates. [More information](https://fttechnologies.com/wind-sensors/ft7-series/).

```{figure} img/FT742.jpg
:name: FT742
```
---

(FT742:commands)=
## Commands


| Command  | Description | Min | Max | Example |
| --- | --- | --- | --- | --- |
| **[](FT742:commands:ft7.ena)** | Enables the FT742 sensor | 0 | 1 | [](FT742:commands:ft7.ena) 1 |
| **[](FT742:commands:ft7.rno)** | [Run order](datalogger:basic:common:runorder) (1-9) | 1 | 9 | [](FT742:commands:ft7.rno) 2 |
| **[](FT742:commands:ft7.rnc)** | [Run counter](datalogger:basic:common:runorder) | 1 | - | [](FT742:commands:ft7.rnc) 1 |
| **[](FT742:commands:ft7.gps)** | Enables the GPS | 0 | 1 | [](FT742:commands:ft7.gps) 1 |
| **[](FT742:commands:ft7.dev)** | Magnetic declination | 0 | 360 | [](FT742:commands:ft7.dev) 339 |
| **[](FT742:commands:ft7.ont)** | Measurement time | 0 | 180 | [](FT742:commands:ft7.ont) |
| **[](FT742:commands:ft7.log)** | Log to disk | 0 | 1 | [](FT742:commands:ft7.log) 1 |


---

(FT742:commands:ft7.ena)=
### \$FT742.ENA

Description: Enable the DCPS <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 1 <br>
Example: \$FT742.ON 1 <br>

Enables the DCPS, [\$FT742.ENA 1](FT742:commands:ft7.on) to turn it on, and [\$FT742.ENA 0](FT742:commands:ft7.ena) to turn it off. This can be useful to conserve battery.

---

(FT742:commands:ft7.rno)=
### \$FT742.RNO

Description: Run order <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 9 <br>
Example: \$FT742.RNO 1 <br>

Sets the Run order for the sensor. See [](datalogger:basic:common:runorder)

---

(FT742:commands:ft7.rnc)=
### \$FT742.RNC

Description: Run counter <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: - <br>
Example: \$FT742.RNC 1 <br>

Sets the Run counter for the sensor. See [](datalogger:basic:common:runcounter)

---

(FT742:commands:ft7.gps)=
### \$FT742.GPS

Description: Enable the GPS <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 2 <br>
Example: \$FT742.GPS 1 <br>

Enable the logging the start and end positions of the sensor acquisition.

---

(FT742:commands:ft7.dev)=
### \$FT742.DEV

Description: Set the magnetic declination <br>
No. of parameters: 1 <br>
Unit: degrees <br>
Parameter type: integer <br>
Minimum parameter value: -180 <br>
Maximum parameter value: 180 <br>
Example: \$FT742.DEV -21 <br>

The magnetic deviation used when transmitting surface currents. This will need to be set depending on location, Baltic Sea is ~+4°, while the SO can be ~-20°. Find out more about magnetic declination [here](https://en.wikipedia.org/wiki/Magnetic_declination)

---

(FT742:commands:ft7.ont)=
### \$FT742.ONT

Description: Measurement time <br>
No. of parameters: 1 <br>
Unit: seconds <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 1800 <br>
Example: \$FT742.ONT 20 <br>

The number of seconds the FT742 sensor is set to acquire data.

---

(FT742:commands:ft7.log)=
### \$FT742.LOG

Description: Log output <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 1 <br>
Example: \$FT742.LOG 1 <br>

Log sensor output to disk.

---

(FT742:data_fields)=
## Data fields

In the Datalogger data tab the following columns are displayed:

| Parameter name | Description | Unit |
| --- | --- | --- |
| FT_Temp | Acoustic Temperature: the ambient temperature via measurable acoustic properties of the airflow | degrees celsius |
| FT_WindDir | Wind direction relative to magnetic north | degrees |
| FT_WindSpeed | Average wind speed | m/s |
| FT_WindGust | Top 5% windspeed | m/s |
| FT_Heading | Sensor direction relative to magnetic north | degrees |

---