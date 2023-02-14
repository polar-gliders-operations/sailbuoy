(piloting)=
# Piloting

The Sailbuoy (SB) is controlled through Ididium Data Services (IDS) and is done [here](https://ids.sailbuoy.no). Each SB has two parts, Autopilot, which concerns controlling the SB's movements, and Datalogger, which controlls the sensors. These are considered to be two separate instruments on IDS, as each has its own modem to send data.

:::{Note}
You cannot control the Datalogger by sending commands to the Autopilot, and vice-versa. Make sure that you send commands to the correct modem.
:::

(piloting:ids)=
## Iridium Data Service

The IDS is the piloting software used to pilot and access data from the SB. This service uses the Azure cloud service to achieve the utmost reliability and uptime. As no system is 100% reliable, we oblige to pilot the SB in such a way that we do not put it as risk if the service experiences downtime. The service provides a user-friendly and easy way to communicate with instruments, showing data as text or graphs, displaying positions and tracks on a map, and controlling the instruments. The IDS have five major tabs that are used: **[](piloting:map)**, **[](piloting:files)**, **[](piloting:data)**, **[](piloting:plot)**, and **[](piloting:control)**. 

---

(piloting:map)=
## Map


This view shows the instruments position on a world map. The positions are automatically updated on the map as data is received from the instruments. In this view it is possible to select the active instrument. <br>

```{margin} The drop down menu to select instrument.

```{figure} img/select_instrument.png
:name: IDS map
```

```{figure} img/IDS_map.png
:name: IDS map

: **History**: Shows historical positions. **Layers**: Add different layers to the map. **Track**: Download KML file.
```


(piloting:map:defining)=
### Defining the track commands

```{figure} img/track_cmd.png
:name: IDS track

: By selecting the checkbox under cursor you can activate the mission plan, where you need to define a start and an end waypoint.

```

:::{Note}
Place waypoints, then copy the waypoint command to send as a **[command](piloting:control)**. The waypoint command is not automatically sent from here, it's just a way to visualize a transect.
:::


---

(piloting:files)=
## Files

```{figure} img/files.png
:name: Files tab

: The available files sent over Iridium. If the current size is smaller than the size, then all the data was not transmitted. You can download each file by selecting it in the list, and then clicking the *"Download Selected File"* in the bottom left corner. 

```

---

(piloting:data)=
## Data

```{figure} img/data.png
:name: Data tab

: The available data sent over Iridium. You can download all the data by clicking the *"Download All as CSV file"* in the bottom left corner.

```

:::{Note}
The columns vary depending on whether you've selected [Autopilot](autopilot:data_fields) or [Datalogger](datalogger:data_fields) in the [](piloting:map) tab.
:::

:::{Warning}
IDS do not send alarms, and it is the pilot in charge that is responsible for checking the Autopilot regularly for warnings, leaks, or low battery reported.
:::

---

(piloting:plot)=
## Plot

```{figure} img/plot.png
:name: Plot tab

: A simple timeseries of the selected variable.

```

---

(piloting:control)=
## Control

```{figure} img/control.png
:name: Control tab

Sending commands to the SB. More info under *Commands or sth*
```
: This view give access to controlling the instrument by entering text commands. A message log is shown on the right where previous commands can be downloaded.

:::{Note}
A password is required to send the commands to the instrument.
:::

* Enter a meaningful comment with initials of who sent the command.
* The commands are written directly in the textbox. 
* Do not enter more than 250 characters per message.
* The order of the commands is arbitrary.

:::{Warning}
There is no way currently to check the current parameters, so it is very much adviced to wait for a response from the instrument before sending the next message. This allows you to know which set of commands that got taken by the SB. Update on this is pending.
:::


---