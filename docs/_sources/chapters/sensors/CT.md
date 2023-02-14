(sensors:CT)=
# Aanderaa Conductivity

The Conductivity Sensor 4319 is a compact fully integrated sensor for measuring the electrical conductivity of seawater. More info at [AADI](https://www.aanderaa.com/media/pdfs/TD263-Condcutivity-sensor-4319.pdf).

```{figure} img/CT.jpg
:name: CT
```

---

(CT:commands)=
## Commands

| Command  | Description | Min | Max | Example |
| --- | --- | --- | --- | --- |
| **[](CT:commands:cndon)** | Enables the CT sensor | 0 | 1 | [](CT:commands:cndon) 1 |
| **[](CT:commands:cndrp)** | [Run order](datalogger:basic:common:runorder) (1-9) | 1 | 9 | [](CT:commands:cndrp) 3 |
| **[](CT:commands:cndrc)** | [Run counter](datalogger:basic:common:runorder) | 1 | - | [](CT:commands:cndrc) 1 |
| **[](CT:commands:cndsc)** | Measurement time | 10 | 600 | [](CT:commands:cndsc) |
| **[](CT:commands:cnlog)** | Log to disk | 0 | 1 | [](CT:commands:cnlog) 1 |

---

(CT:commands:cndon)=
### \$CNDON

Description: Enable the DCPS <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 1 <br>
Example: \$CNDON 1 <br>

Enables the CT sensor, [\$CNDON 1](CT:commands:cndon) to turn it on, and [\$CNDON 0](CT:commands:cndon) to turn it off. This can be useful to conserve battery.

---

(CT:commands:cndrp)=
### \$CNDRP

Description: Run order <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 9 <br>
Example: \$CNDRP 1 <br>

Sets the Run order for the sensor. See [](datalogger:basic:common:runorder)

---

(CT:commands:cndrc)=
### \$CNDRC

Description: Run counter <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: - <br>
Example: \$CNDRC 1 <br>

Sets the Run counter for the sensor. See [](datalogger:basic:common:runcounter)

---

(CT:commands:cndsc)=
### \$CNDSC

Description: Measurement time <br>
No. of parameters: 1 <br>
Unit: seconds <br>
Parameter type: integer <br>
Minimum parameter value: 10 <br>
Maximum parameter value: 600 <br>
Example: \$CNDSC 10 <br>

The number of seconds the CT sensor is set to acquire data.

---

(CT:commands:cnlog)=
### \$CNLOG

Description: Log output <br>
No. of parameters: 1 <br>
Unit: - <br>
Parameter type: integer <br>
Minimum parameter value: 0 <br>
Maximum parameter value: 1 <br>
Example: \$CNLOG 1 <br>

Log sensor output to disk.

---

(CT:data_fields)=
## Data fields

In the Datalogger data tab the following columns are displayed:

| Parameter name | Description | Unit |
| --- | --- | --- |
| AADI_Cond | Conductivity | mS/cm |
| AADI_Temp | Temperature | degrees celcius |

---