(datalogger)=
# Datalogger

(datalogger:basic)=
## Basic functionality

(datalogger:basic:acq_loop)=
### Acquisition loop

In run mode the datalogger does the following in sequence:
1. Get GPS fix (10-20 s)
2. Get internal sensor values (1 s)
3. Startup delay
4. Get sensor 1 data (time defined in the configuration)
5. Get sensor 2 data (time defined in the configuration)
6. Get sensor ... 
7. Send data (30-120 s) TX
8. Receive commands (10 s) RX
9. Low power mode (rest of the log interval)

```{figure} img/acq_loop.png
:name: aquisition loop
```

The datalogger has a watchdog timer that resets every 1.5 hours. If the log rate period is set to more than this or the software hangs for some reason the system is reset. After reset the datalogger restarts with the saved default configuration. The watchdog timer is turned off when downloading data, enabling the download to continue for several hours.

All sensors are disabled on power up and have to be actively enabled. This is to prevent sensors being switched on if a reboot occurs during a mission. A reboot can occur if a sensor malfunction causes the battery voltage to spike or the batteries are empty. When starting the datalogger all sensors are disabled by default and have to be actively switched on by sending the [](datalogger:commands:enable) command. 

:::{Note}
The sensors will automatically be deactivated when the voltage falls below a preset level
(battery level is ~ 10\%)
:::

When the datalogger is powered off the configuration reverts back to the saved settings. The datalogger has the ability to send small files. This is used by some sensors to send images or other kind of files.

---

(datalogger:basic:switch)=
### Turning on/off

The datalogger is powered up by **removing** the magnetic switch. It is switched off by placing the magnetic switch back on the Velcro pad.

:::{Note}
The solar panels will charge the batteries regardless if the datalogger is on or off.
:::

```{margin} 


```{figure} img/datalogger.png
:width: 100%
:name: datalogger
The cap to the datalogger serial connector.
```

```{figure} img/connecting.png
:width: 100%
:name: connect
The aft of the Sailbuoy, showing the magnetic switches for the datalogger and [](autopilot), as well as the serial cable connected to the datalogger port.
```

The serial port is used to communicate with the Datalogger. It can be used to configure the datalogger and monitor the datalogger output when running. The serial port will stop transmitting data after a while when the datalogger is running.

---

(datalogger:basic:connecting)=
### Connecting

1. Connect your PC with the Datalogger using the supplied serial cable to the serial port. 
2. Start Terraterm and select the correct serial port at 9600 baud.
3. Power on the datalogger by removing the magnetic switch.
4. Some text will appear in the terminal, press ESC within 60 seconds to enter the menu system.

---

(datalogger:basic:menu)=
### Main menu

Once you've completed the steps in [](datalogger:basic:connecting), you are greeted by the main menu of the datalogger. In this menu the configuration of the datalogger can be changed. By selecting `'*' :Run` the datalogger will enter run mode. Entering run mode via the menu system will enable all sensors by default. They are otherwise disabled and have to be enabled remotely.

The menu system responds to the following keys:
* `RET` (Enter) will display the menu again.
* `ESC` will exit a submenu.
* `SPACE` is to enter a note.


```
MAIN MENU 01.01.2019 00:00:00
'0': Sensor menu
'1': File menu
'2': Direct Serial menu
'P': Print Configuration
'E': Edit Configuration
'S': Save Configuration
'T': Set Date Time
'*': Run
```

---

(datalogger:basic:menu:sensormenu)=
#### Sensor menu

This menu is used to run each individual sensor with the current configuration. The content of this menu depends on which sensors are installed. It is also possible to run the GPS, Iridium modem and check the battery voltage.

```
SENSOR MENU 01.01.2019 00:00:55
'5': Sensor 1
'B': Sensor 2
'G': GPS
'I': Iridium SBD
'V': Battery Voltage
```

---

(datalogger:basic:menu:filemenu)=
#### File menu

This menu is used to download files and show the disk content. To erase all files see [](datalogger:basic:menu:delete)

```
FILE MENU MENU 01.01.2019 00:05:38
'3': Download files Ymodem
'4': Download one file Ymodem
'7': Format drive
'D': Display files
'P': Print file to screen
'B': Change baudrate
```

---

(datalogger:basic:menu:directserial)=
#### Direct serial
This menu is used to connect directly to each individual sensor. The sensor is switched on and the serial cable is connected directly to the sensors. This functionality can be used to connect the sensor to supplier software. Often used for sensor configuration. When the sensor is selected the datalogger becomes transparent.

:::{Tip}
To unlock the serial port, close the terminal editor before opening any software configuration tool.
:::

```
DIRECT SERIAL MENU 01.01.2019 00:01:30
'1': Sensor 1
'2': Sensor 2
```

---

(datalogger:basic:menu:download)=
#### Download files

1. Press `‘1’` to enter the file menu.
2. Select `‘B’` to change the baud rate and enter a higher value (i.e. 115 200 baud) to optimise download speed, and set the same value for Tera Term (`Setup->Serial Port... Speed`).
3. Press `RET` to display the menu.
4. Select `‘3’: Download files Ymodem`. The datalogger is now waiting for Tera Term to initiate the download.
5. Initiate the download by selecting the Tera Term menu item `File->Transfer->YMODEM->Receive...` (The download should begin immediately. If the download fails, try an alternative: `File->Transfer->XMODEM->Receive...`).
6. When the download is finished press return to display the datalogger menu.
7. You can now exit Tera Term and put back the magnetic switch.

:::{Warning}
It is extremely important that step 6 is not disturbed in any way.
:::


```{figure} img/terraterm.png
:width: 100%
:name: terraterm
```

:::{Note}
During the data download the watchdog timer is disabled.
:::

---

(datalogger:basic:menu:delete)=
#### Delete files

1. Enter the file menu.
2. Select `'7': Format drive`
3. Select `'D': Display files to ensure the disk is empty`
4. Press RET to display the menu.

#### Log datalogger output

To keep track of the changes made to the system it is good practive to log all the output from the datalogger to a file.

```{figure} img/log1.png
:width: 100%
:name: log1
```

```{figure} img/log2.png
:width: 100%
:name: log2
```
---

(datalogger:basic:common)=
### Common sensor parameters
(datalogger:basic:common:runorder)=
#### Run order

Each sensor has a RunOrder configuration value. This value decides in which order the sensors are run. The RunOrder value can be set to any number between 1 and 9.

The sensor with the lowest value will be run first.

```
Example 1:
Sensor1 RunOrder = 1
Sensor2 RunOrder = 2
Sensor3 RunOrder = 3
Sensor 1 will be run first, then sensor 2, then sensor 3.
```

---

(datalogger:basic:common:runcounter)=
#### Run counter

Each sensor has a RunCounter configuration value. This value decides how often the sensor is run. If RunCounter = 1 the sensor is run each
acquisition period. If RunCounter = 2 the sensor is run every second period and so on. The maximum value is 255.

:::{Tip}
If two or more sensors have the same RunCounter value, they will run in the same acquisition period.
:::

---

(datalogger:basic:battery)=
### Battery voltage and solar panels

The solar panels are connected to the batteries by a charging circuit. This circuit is always active regardless if the datalogger is switched on or off. The battery voltage gives information about the charge of the battery. The battery is fully charged at 13.3V. Any voltage above this is due to the solar panels increasing the voltage. At 13.0V the battery has around 50\% charge left falling to about 15\% at 12.7V. At this voltage the datalogger automatically turns the sensors off to preserve energy for the Iridium communication and GPS.

---

(datalogger:basic:restarting)=
### Restarting

The datalogger can be restarted at any point in time without damaging the electronics. In some cases,a sensor does not like being switched off in the middle of an acquisition. Upon restart the datalogger will start with the saved default configuration. 

:::{Note}
To restart the datalogger first switch it off with the magnetic switch, wait 60 seconds, then remove the magnetic switch to start again.
:::

---

(datalogger:commands)=
## Commands

| Command | No Parameters | Description | Min | Max | Recommended | Example |
| --- | --- | --- | --- | --- | --- | --- |
| **[](datalogger:commands:logrt)** | 1 | Log rate in seconds | 60 | 3600 |900| [](datalogger:commands:logrt) 1800 |
| **[](datalogger:commands:lrmin)** | 1 | Log rate in minutes | 1 | 60 |15| [](datalogger:commands:lrmin) 30 |
| **[](datalogger:commands:txper)** | 1 | Only transmit every N acquisitions | 1 | 24 |1| [](datalogger:commands:txper) 10 |
| **[](datalogger:commands:strdl)** | 1 | Sensor start up delay in seconds | 0 | 1800 |150| [](datalogger:commands:strdl) 60 |
| **[](datalogger:commands:enable)** | 0 | Enable sensors|  |  || [](datalogger:commands:enable) |
| **[](datalogger:commands:disable)** | 0 | Disable sensors |  |  || [](datalogger:commands:disable) |
| **[](datalogger:commands:irifs)** | 1 | Send byte limit | 0 |  |5000| [](datalogger:commands:irifs) 5000 |
| **[](datalogger:commands:sendfile)** | 2 | Send end part of file |  |  || [](datalogger:commands:sendfile) TMP.TXT 1000 |
| **[](datalogger:commands:dir)** | 0 | Send disk listing |  |  || [](datalogger:commands:dir) |
| **[](datalogger:commands:save)** | 0 | Save current configuration |  |  || [](datalogger:commands:save) |

---

(datalogger:commands:logrt)=
### \$LOGRT

Description: Lograte <br>
No. of parameters: 1 <br>
Parameter type: integer <br>
Unit: seconds <br>
Minimum parameter value: 60 <br>
Maximum parameter value: 3600 <br>
Example: $LOGRT 900 <br>

This configuration value decides the acquisition period. This value is the period in seconds. [$LOGRT 900](datalogger:commands:logrt) sets the acquisition period to 15 minutes. This is interchangeable with [](datalogger:commands:lrmin).

---

(datalogger:commands:lrmin)=
### \$LRMIN

Description: Lograte <br>
No. of parameters: 1 <br>
Parameter type: integer <br>
Unit: minutes <br>
Minimum parameter value: 1 <br>
Maximum parameter value: 60 <br>
Example: $LRMIN 15 <br>

This configuration value decides the acquisition period. This value is the period in minutes. [$LRMIN 15](datalogger:commands:lrmin) sets the acquisition period to 15 minutes. This is interchangeable with [](datalogger:commands:logrt).

---

(datalogger:commands:txper)=
### \$TXPER

Description: Transmission frequency <br>
No. of parameters: 1 <br>
Parameter type: integer <br>
Unit: - <br>
Minimum parameter value: 1 <br>
Maximum parameter value: 24 <br>
Example: $TXPER 1 <br>

This configuration value decides how often a message is transmitted. A value of 1 will tell the datalogger to transmit each time it has run the sensors. Sending [$TXPER 10](datalogger:commands:txper) tells the datalogger to transmit every 10th acquisition period.

---

(datalogger:commands:strdl)=
### \$STRDL

Description: Start up delay <br>
No. of parameters: 1 <br>
Parameter type: integer <br>
Unit: seconds <br>
Minimum parameter value: 1 <br>
Maximum parameter value: 1800 <br>
Example: $STRDL 150 <br>

Sensor start up delay: A delay can be configured to start the sensor acquisition a set number of seconds after the datalogger starts a new acquisition period. Sending [$STRDL 150](datalogger:commands:strdl) tells the sensor acquisition to start 150 seconds after power up. It is recommended to use at least 2 minutes when using the DCPS.  
 
---

(datalogger:commands:enable)=
### \$ENABLE

Description: Enable sensor aquisition <br>
No. of parameters: 0 <br>
Parameter type: integer <br>
Unit: - <br>
Minimum parameter value: - <br>
Maximum parameter value: - <br>
Example: $ENABLE <br>

The datalogger always starts up with the sensors disabled. To enable the sensor acquisition, the command [](datalogger:commands:enable) must be sent. The sensors will then run according to their configuration.
 
---

(datalogger:commands:disable)=
### \$DISABLE

Description: Disable sensor aquisition <br>
No. of parameters: 0 <br>
Parameter type: integer <br>
Unit: - <br>
Minimum parameter value: - <br>
Maximum parameter value: - <br>
Example: $DISABLE <br>

This command disables the sensor acquisition.
 
---

(datalogger:commands:sendfile)=
### \$SENDFILE

Description: Send file <br>
No. of parameters: 2 <br>
Parameter type: integer <br>
Unit: - <br>
Minimum parameter value: - <br>
Maximum parameter value: - <br>
Example: $SENDFILE DCPS.TXT 1000 <br>

This command will transmit parts of a file over iridium. It can be used to check the state of a sensor or download some data. The [](datalogger:commands:sendfile) command takes 2 parameters, where the fist parameter is the filename on the datalogger disk and the second parameter is the number of bytes to send. 

:::{Note}
If the file is bigger than the second parameter N, only the
last N bytes of the file will be sent.
:::

[$SENDFILE DCPS.TXT 1000](datalogger:commands:sendfile) tells the datalogger to send the last 1000 bytes of the DCPS.TXT file. If the second parameter is bigger than the file size, the whole file will be sent. Note that the [](datalogger:commands:irifs) setting will limit the bytes sent.

---

(datalogger:commands:irifs)=
### \$IRIFS

Description: Send file <br>
No. of parameters: 2 <br>
Parameter type: integer <br>
Unit: bytes <br>
Minimum parameter value: 0 <br>
Maximum parameter value: - <br>
Example: $IRIFS 5000 <br>

This command limits the maximum bytes send in one period. [$IRIFS 5000](datalogger:commands:irifs) 5000 limits the transmission to bytes to 5 kB per period
 
---

(datalogger:commands:dir)=
### \$DIR

Description: List directory <br>
No. of parameters: 0 <br>
Parameter type: integer <br>
Unit: - <br>
Minimum parameter value: - <br>
Maximum parameter value: - <br>
Example: $DIR <br>

This command will send a text file showing the files on the disk, much like the DIR command in Windows. This command has no parameters. Sending []datalogger:commands:dir) will produce a file called DIR.TXT and below is an example of the contents of this file. This file is accessible to download  over at the [](piloting:files) tab.

```
|   Filename | Filesize[B] |       Date |     Time |
| SERIAL.TXT |         860 | 24.10.2019 | 00:01:28 |
| AIRMAR.TXT |       56024 | 24.10.2019 | 17:31:44 |
|    DIR.TXT |           0 | 24.10.2019 | 17:31:44 |

3 File(s) 56884 bytes
977 MB free
```
---

(datalogger:commands:save)=
### \$SAVE

Description: Save current configuration <br>
No. of parameters: 0 <br>
Parameter type: integer <br>
Unit: - <br>
Minimum parameter value: - <br>
Maximum parameter value: - <br>
Example: $SAVE <br>

This command saves the current configuration as default. Sending [](datalogger:commands:save) will save the current configuration as default.

---


(datalogger:data_fields)=
## Data fields

In the Datalogger data tab the following columns are displayed:

| Parameter name | Description | Unit |
| --- | --- | --- |
| Time | Time for start of sampling | Time UTC |
| Lat | Latitude in decimal degrees | decimal degrees |
| Long | Longitude in decimal degrees | decimal degrees |
| TTFF | Time to first fix. The time in seconds the GPS uses to obtain a valid position. | seconds |
| Count | Tack counter. For each tack this counter is incremented. It rolls over after a set number of tacks. | integer |
| Commands | Received commands count. Shows the number of command values received and processed on the previous transmission. | integer |
| Tx Tries | Iridium transmission tries. Shows the number of transmissions tries on the previous transmission. This is normally set to 3 and if this value is 3 it is due to 3 tries end success or 3 tries and fail. | integer |
| ONT | On time (time in acquisition mode) | seconds |
| I | Current consumption after GPS fix. | A |
| V | Battery voltage. Shows the battery voltage. >13.3 fully charged. Maximum voltage is 14.2 volts when charging. <br> 13.0 V ~ 50\% charged. <br> 12.8 V ~ 15\% charged. | V |
| Temperature | Payload temperature. The internal temperature of the payload container. | °C |

:::{Caution}
Each transmitted value has a limited range, i.e a maximum and minimum value. If the acquired
value falls outside of these limits the transmitted value will be NULL. This is to save on transmission costs.
:::

:::{Note}
The transmitted data for the sensors is shown in the user manuals for each sensor. This depends on the
configuration of the vehicle.
:::

