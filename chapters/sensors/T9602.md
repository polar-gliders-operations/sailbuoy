(sensors:T9602)=
# Telaire T9602

---

(ADCP:commands)=
## Commands


| Command  | Description | Min | Max | Example |
| --- | --- | --- | --- | --- |
| **[](ADCP:commands:dcps.on)** | Enables the DCPS | 0 | 1 | [](ADCP:commands:dcps.on) 1 |
| **[](ADCP:commands:dcps.rp)** | [Run order](datalogger:basic:common:runorder) (1-9) | 1 | 9 | [](ADCP:commands:dcps.rp) 3 |
| **[](ADCP:commands:dcps.rc)** | [Run counter](datalogger:basic:common:runorder) | 1 | - | [](ADCP:commands:dcps.rc) 10 |
| **[](ADCP:commands:dcps.gps)** | Enables the GPS | 0 | 2 | [](ADCP:commands:dcps.gps) 1 |
| **[](ADCP:commands:dcps.dev)** | Magnetic declination | -180 | 180 | [](ADCP:commands:dcps.dev) -21|
| **[](ADCP:commands:dcps.min)** | Measurement time |  |  | [](ADCP:commands:dcps.min) |
| **[](ADCP:commands:dcps.avg)** | Number of cells to average | 0 | - | [](ADCP:commands:dcps.avg) 6 |
| **[](ADCP:commands:dcps.log)** | Log to disk | 0 | 1 | [](ADCP:commands:dcps.log) 1 |


---

(ADCP:commands:dcps.on)=
### \$DCPS.ON

Description: Enable the DCPS <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 1 <br>
Example: \$DCPS.ON 1 <br>

Enables the DCPS, [\$DCPS.ON 1](ADCP:commands:dcps.on) to turn it on, and [\$DCPS.ON 0](ADCP:commands:dcps.on) to turn it off. This can be useful to conserve battery.

---

(ADCP:commands:dcps.rp)=
### \$DCPS.RP

Description: Run order <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 9 <br>
Example: \$DCPS.RP 1 <br>

Sets the Run order for the sensor. See [](datalogger:basic:common:runorder)

---

(ADCP:commands:dcps.rc)=
### \$DCPS.RC

Description: Run counter <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: - <br>
Example: \$DCPS.RC 1 <br>

Sets the Run counter for the sensor. See [](datalogger:basic:common:runcounter)

---

(ADCP:commands:dcps.gps)=
### \$DCPS.GPS

Description: Enable the GPS <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 2 <br>
Example: \$DCPS.GPS 1 <br>

To compensate for vehicle movement the GPS must be enabled. **DCPS.GPS** = 1: The GPS is left powered on when the DCPS is acquiring data (faster fix). **DCPS.GPS** = 2: The GPS is powered off when the DCPS is acquiring data(saves power)

---

(ADCP:commands:dcps.dev)=
### \$DCPS.DEV

Description: Set the magnetic declination <br>
No. of parameters: 1 <br>
Unit: degrees <br>
Parameter type: integer <br>
Minimum parameter value: -180 <br>
Maximum parameter value: 180 <br>
Example: \$DCPS.DEV -21 <br>

The magnetic deviation used when transmitting surface currents. This will need to be set depending on location, Baltic Sea is ~+4°, while the SO can be ~-20°. Find out more about magnetic declination [here](https://en.wikipedia.org/wiki/Magnetic_declination)

---

(ADCP:commands:dcps.min)=
### \$DCPS.MIN

Description: Measurement time <br>
No. of parameters: 1 <br>
Unit: minutes <br>
Parameter type: integer <br>
Minimum parameter value: 2 <br>
Maximum parameter value: - <br>
Example: \$DCPS.MIN 4 <br>

The number of minutes the DCPS is set to acquire data. This setting should be set on 2 min intervals. 2,4,6,8 minutes etc., depending on the DCPS configuration.

---

(ADCP:commands:dcps.avg)=
### \$DCPS.AVG

Description: Cell averaging <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: - <br>
Example: \$DCPS.AVG 6 <br>

The number of cells down from surface used to calculate the average current.

---

(ADCP:commands:dcps.log)=
### \$DCPS.LOG

Description: Log output <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 1 <br>
Example: \$DCPS.LOG 1 <br>

Log sensor output to disk.

---

(ADCP:data_fields)=
## Data fields

In the Datalogger data tab the following columns are displayed:

```{margin} Status indicator bits:
0: No errors <br> 
1: Memory error  <br>
2: File Open error  <br>
4: Timeout error  <br>
8: GPS error  <br>

```{Note}
The binary sytem makes it possible for the sensor to communicate more than one error. E.g., if we see 9, we know that there was a memory and GPS error.
```


| Parameter name | Description | Unit |
| --- | --- | --- |
| DCPSStatus | Status indicator | integer|
| DCPSOnMin | Acquisition time. | minutes |
| DCPSSpeed | Average current speed. | m/s |
| DCPSDirection | Averagecurrent direction. | degrees |

---

The DCPS is preconfigured when delivered, and if you are reconfiguring the DCPS, make sure the output from the DCPS contain at least these values:

* Cell Index
* Horizontal Speed[cm/s]
* Direction[Deg.M]

This is so that the datalogger will be able to process the DCPS data. All other values will be ignored, but saved in the DCPS.txt.

To make changes to the internal sensor settings, make sure to follow the step outlined in the [](datalogger), until you get to the [](datalogger:basic:menu:directserial). After you have closed the terminal, you can use the manufacturers own software to make changes. This described more under [](ADCP:configuration). 


(ADCP:output)=
## Logged output from DCPS

The following output is saved to “DCPS.TXT” file on disk

* <span style="color:black">Black text</span>: This text is generated by the datalogger and contains date/time of the internal datalogger clock when saving to disk

* <span style="color:green">Green text</span>: This is the direct raw output of the DSCP instrument. To process this data, see DCPS manuals.

* <span style="color:Blue">Blue text</span>: This is the calculated current speed and direction calculated by the datalogger based on the raw DCPS output. Units are m/s and degrees.

* <span style="color:red">Red text</span>: GPS position and time of when the DCPS started and stopped acquisition.

Sensor log example (DCPS.TXT)


Sensorlog opened 23.06.2020 09:02:35 <span style="color:red">GPS: 23.06.2020 09:02:35 60.17471 5.49304 </span><br>
<span style="color:green">% <br>
StartupInfo 5400 460 Mode AADI Smart Sensor Terminal Protocol....... <br>
Initializing... <br>
Started... <br>
MEASUREMENT 5400 460 Heading[Deg.M] 2.941192E-01...... </span><br>
<span style="color:blue">*** Processed data: Deviation 0.00 deg <br>
Cell   0  Speed0.1154 Dir 337.8443   East -0.0435   North 0.1069   <br>
Cell   1  Speed 0.1163 Dir 359.2926   East -0.0014   North 0.1162   <br>
Cell   2  Speed 0.1133 Dir 356.9538   East -0.0060   North 0.1132   <br>
Cell   3  Speed 0.1026 Dir 353.6823   East -0.0113   North 0.1020   <br>
Cell   4  Speed 0.0764 Dir 65.6921   East 0.0696   North 0.0314  <br>
... </span><br>
Sensorlog closed 23.06.2020 09:05:05 <span style="color:red">GPS: 23.06.2020 09:05:01 60.17569 5.49435 </span><br>

(ADCP:algorithm)=
## Algorithm

The following algorithm is used to process the data:
* Read direction and speed for each cell from the DCPS in the <span style="color:green">“MEASUREMENT”</span> line
* Converts direction and speed to northing and easting speed.
* Calculatean average northing and easting speed for each cell if multiple records are received.
* Subtracts (actually add) the northing and easting speed derived from the GPS position at start and end of the acquisition, from each cell.
* Calculate the average northing and easting speed from the first N cells (decided by [](ADCP:commands:dcps.avg)).
* Convert the average to direction and speed (this is the surface current).

(ADCP:configuration)=
## DCPS configuration

To configure the internal sensor settings, cell size, 