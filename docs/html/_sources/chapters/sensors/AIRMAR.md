(sensors:AIRMAR)=
# Airmar 200WX

The Airmar 200WX is a Weatherstation containing various sensors. Documentation can be found on
www.airmar.com

```{figure} img/airmar.jpg
:name: Airmar
```

(AIRMAR:config)=
## Configuration

The Airmar is configured to stream data at 4800 baud and to output the following sentences:

| Sentence  | Frequency [Hz] | Description |
| --- | --- | --- |
| GGA | 0.1 | - |
| HDG | 1 | - |
| MDA | 1 | - |
| MWV(R) | 1 | - |
| RMC | 1 | - |
| XDR(A) | 0.1 | - |
| XDR(C) | 1 | - |
| XDR(D) | 1 | - |


The sensor is configured using the WeatherCaster software from Airmar.
The following sentences should be enabled:

* \$WIMDA – windspeed, direction
* \$WIMWV – windspeed if no gps fix
* \$HCHDG - heading

---

(AIRMAR:commands)=
## Commands


| Command  | Description | Min | Max | Example |
| --- | --- | --- | --- | --- |
| **[](AIRMAR:commands:airrp)** | [Run order](datalogger:basic:common:runorder) | 1 | 9 | [](AIRMAR:commands:airrp) 1 |
| **[](AIRMAR:commands:airrc)** | [Run counter](datalogger:basic:common:runorder) | 0 | - | [](AIRMAR:commands:airrc) 3 |
| **[](AIRMAR:commands:airen)** | Enables the Airmar | 1 | - | [](AIRMAR:commands:airen) 10 |
| **[](AIRMAR:commands:airto)** | Measurement time | 0 | 3600 | [](AIRMAR:commands:airto) 1 |
| **[](AIRMAR:commands:airao)** | Always on | 0 | 1 | [](AIRMAR:commands:airao) 1|
| **[](AIRMAR:commands:airlg)** | Log to disk | 0 | 1 | [](AIRMAR:commands:airlg) |

:::{Note}
The sensor consumes around 100 mA while running.
:::

---

(AIRMAR:commands:airrp)=
### \$AIRRP

Description: Run order <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 1 <br>
Maximum parameter value: 9 <br>
Example: \$AIRRP 1 <br>

Sets the Run order for the sensor. See [](datalogger:basic:common:runorder)

---

(AIRMAR:commands:airrc)=
### \$AIRRC

Description: Run counter <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: - <br>
Example: \$AIRRC 1 <br>

Sets the Run counter for the sensor. See [](datalogger:basic:common:runcounter)

---

(AIRMAR:commands:airen)=
### \$AIREN

Description: Enable the Airmar <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 1 <br>
Example: \$AIREN 1 <br>

Enables the Airmar, [\$AIREN 1](AIRMAR:commands:airen) to turn it on, and [\$AIREN 0](AIRMAR:commands:airen) to turn it off. This can be useful to conserve battery.

---

(AIRMAR:commands:airto)=
### \$AIRTO

Description: Measurement time <br>
No. of parameters: 1 <br>
Unit: seconds <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 3600 <br>
Example: \$AIRTO 60 <br>

The number of seconds the Airmar is set to acquire data. With [\$AIRAO 1](AIRMAR:commands:airao) it is fine to have 60 seconds, but with [\$AIRAO 0](AIRMAR:commands:airao) we would require at least 15 minutes to achieve a GPS fix.

---

(AIRMAR:commands:airao)=
### \$AIRAO

Description: Set the Airmar Always On <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 1 <br>
Example: \$AIRAO 1 <br>

The Airmar can be configured to always be on, which allows it to get a GPS fix. The fix is required for accurate measurements of wind direction, and is sometimes difficult to get. This is why we usually leave the Airmar on between measurements. The power consumption increases massively, and should only be done in good light conditions, so that the battery are allowed to fully recharge during the day. Send [\$AIRAO 1](AIRMAR:commands:airao) to activate this function.

---

(AIRMAR:commands:dcps.min)=
### \$AIRLG

Description: Log output <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 1 <br>
Example: \$AIRLG 1 <br>

Log sensor output to disk.

---

(AIRMAR:data_fields)=
## Data fields

In the Datalogger data tab the following columns are displayed:




| Parameter name | Description | Unit |
| --- | --- | --- |
| AirmarAirTemp | Mean air temperature | degrees Celcius |
| AirmarWindDirection | Mean wind direction | degrees |
| AirmarWindSpeed | Mean wind speed | m/s |
| AirmarWindGust | 95% largest wind speed value during measurement | degrees |
| AirmarHeading | Mean heading during measurement | degrees |
| AirmarAirFix | GPS corrected data | degrees |

:::{Note}
If the sensor is not powered on long enough the AirmarAirFix will be 0. This means the sensor has
not gained a GPS fix and the data transmitted will be of a lower quality.
:::

---


(AIRMAR:mounting)=
## Mounting

Before attaching the sensor, it is important to lubricate around the connector with marine silicone to
ensure that water does not enter the pins when the sensor is mounted. **Hand tighten the screw**. Align the sensor with the alignment lines.