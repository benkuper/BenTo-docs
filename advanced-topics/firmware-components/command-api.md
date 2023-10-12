# Command API

The command API defines a set of commands that can be sent to a prop via **OSC** or **Serial** connection. The structure of the commands is the same for both connection types.

For example the following commands can be used to put the prop to sleep/shutdown:

* OSC: /root/sleep&#x20;
* Serial: root.sleep&#x20;

The **OSC messages** are **sent to port 9000** of the prop. **OSC feedback** (e.g. button press, orientation data) from the prop is sent to **port 10000** on the host machine.\
For sending through serial connection you send a string. The **baud rate** for the serial connection is **115200**.

## Detecting props

To detect props on the network you send a broadcast message to the network with the OSC address /yo containing the IP of your computer as a string. The prop will send feedbacks to the IP address received by the /yo message. It will respond with a /wassup message containing the IP address, MAC address and name of the prop.&#x20;

| OSC Command | Serial Command | Description                                                                                                      |
| ----------- | -------------- | ---------------------------------------------------------------------------------------------------------------- |
| **/yo**     | N/A            | <p>Broadcast message to all props.<br>Request props to send a wassup message to communicate it's IP address.</p> |

## Power

| OSC Command       | Serial Command   | Description                                            |
| ----------------- | ---------------- | ------------------------------------------------------ |
| **/root/sleep**   | **root.sleep**   | <p>Put the prop to sleep.</p><p>Shutdown the prop.</p> |
| **/root/restart** | **root.restart** | Restart the prop.                                      |

## WIFI Configuration

| OSC command              | Serial command          | Parameters                                                                   | Description                                                                |
| ------------------------ | ----------------------- | ---------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **/wifi/setCredentials** | **wifi.setCredentials** | <p><strong>SSID</strong>: string</p><p><strong>password</strong>: string</p> | Set the WIFI name (SSID) and password to which the prop should connect to. |

## RGB LED control

| OSC Command         | Serial Command     | Parameters                                                                                                                                                                                                                      | Description                                                                                                                      |
| ------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **/leds/mode**      | **leds.mode**      | <p>LED mode as string or int</p><p>direct (0)</p><p>system (1)</p><p>stream (2)</p><p>player (3)</p>                                                                                                                            | Select the LED mode. Streaming is a UDP live streaming protocol of colors. Player is a sequence from the SD card.                |
| **/rgb/brightness** | **rgb.brightness** | **brightness**: float                                                                                                                                                                                                           | Set the brightness of the RGB LEDs.                                                                                              |
| **/rgb/fill**       | **rgb.fill**       | <p><strong>red</strong>: float</p><p><strong>green</strong>: float</p><p><strong>blue</strong>: float</p>                                                                                                                       | <p>Fill all LEDs with a color.</p><p>Serial example setting red: <br><code>rgb.fill 1,0,0</code></p>                             |
| **/rgb/range**      | **rgb.range**      | <p><strong>red</strong>: float</p><p><strong>green</strong>: float</p><p><strong>blue</strong>: float</p><p><strong>alpha</strong>: float</p><p><strong>position 1</strong>: float</p><p><strong>position 2</strong>: float</p> | <p>Fill a range of LEDs with a color.</p><p>Serial example setting one half to red: <br><code>rgb.range 1,0,0,1,0,0.5</code></p> |
| **/rgb/point**      | **rgb.point**      | <p><strong>red</strong>: float</p><p><strong>green</strong>: float</p><p><strong>blue</strong>: float</p><p><strong>alpha</strong>: float</p><p><strong>position 1</strong>: float</p><p><strong>position 2</strong>: float</p> | Create a point with a color.                                                                                                     |

## Player control

These commands provide control over the sequences stored on the SD card of the prop.

| OSC command        | Serial command    | Parameters                         | Description                                                                                                                                                                                                     |
| ------------------ | ----------------- | ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **/player/load**   | **player.load**   | **name** of sequence: string       | Load the sequence with the given name.                                                                                                                                                                          |
| **/player/play**   | **player.play**   | **start time** in seconds: float   | Start the loaded sequence at the start time given.                                                                                                                                                              |
| **/player/pause**  | **player.pause**  | _no parameter_                     | Pause the playing sequence.                                                                                                                                                                                     |
| **/player/resume** | **player.resume** | _no parameter_                     | Resume the paused sequence.                                                                                                                                                                                     |
| **/player/stop**   | **player.stop**   | _no parameter_                     | Stop the loaded sequence.                                                                                                                                                                                       |
| **/player/seek**   | **player.seek**   | **time** to seek in seconds: float | Seek the given position of a sequence.                                                                                                                                                                          |
| **/player/id**     | **player.id**     | **enabled**: boolean               | Show identification mode of sequence. A way to display/preview which prop belongs to which cluster.                                                                                                             |
| **/player/delete** | **player.delete** | **sequence name**: string          | <p>Delete the sequence with the given name. This deletes the .colors and .meta file of the sequence.<br></p><p>Example to delete a sequence called "timeline": </p><p><code>/player/delete /timeline</code></p> |

## Files

These command provide control over the file on the SD card.

| OSC command             | Serial command         | Parameters             | Description                                                                                                                                                                  |
| ----------------------- | ---------------------- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **/files/delete**       | **files.delete**       | **filepath**: string   | <p>Delete the file with the given file path.</p><p></p><p>Example to delete the .colors file of the timeline sequence:</p><p><code>/files/delete /timeline.colors</code></p> |
| **/files/deleteFolder** | **files.deleteFolder** | **folderpath**: string | Delete the folder with the given path.                                                                                                                                       |

## IMU

These commands provide control over the sensor data of the IMU.

| OSC command         | Serial command     | Parameters          | Description                                                             |
| ------------------- | ------------------ | ------------------- | ----------------------------------------------------------------------- |
| **/imu/enabled**    | **imu.enabled**    | **enable**: boolean | Enable sending of IMU values to the host computer.                      |
| **/imu/updateRate** | **imu.updateRate** | **rate**: integer   | Set the update rate at which the IMU data is sent to the host computer. |

## OSC&#x20;

| OSC command      | Serial command  | Parameters          | Description               |
| ---------------- | --------------- | ------------------- | ------------------------- |
| **/osc/enabled** | **osc.enabled** | **enable**: boolean | Enable OSC communication. |

## Serial

| OSC command               | Serial command           | Parameters          | Description           |
| ------------------------- | ------------------------ | ------------------- | --------------------- |
| **/serial/outputEnabled** | **serial.outputEnabled** | **enable**: boolean | Enable Serial output. |

