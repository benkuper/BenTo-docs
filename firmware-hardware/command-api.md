# Command API

The command API defines a set of commands that can be sent to a prop via **OSC** or **Serial** connection. The structure of the commands is the same for both connection types.

For example the following commands can be used to put the prop to sleep/shutdown:

* OSC: /root/sleep 
* Serial: root.sleep 

The **OSC messages** are **sent to port 9000** of the prop. **OSC feedback** \(e.g. button press, orientation data\) from the prop is sent to **port 10000** on the host machine.  
For sending through serial connection you send a string. The **baud rate** for the serial connection is **115200**.

## Detecting props

To detect props on the network you send a broadcast message to the network with the OSC address /yo containing the IP of your computer as a string. The prop will send feedbacks to the IP address received by the /yo message. It will respond with a /wassup message containing the IP address, MAC address and name of the prop. 

| OSC Command | Serial Command | Description |
| :--- | :--- | :--- |
| **/yo**  | N/A | Broadcast message to all props. Request props to send a wassup message to communicate it's IP address. |

## Power

<table>
  <thead>
    <tr>
      <th style="text-align:left">OSC Command</th>
      <th style="text-align:left">Serial Command</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>/root/sleep</b>
      </td>
      <td style="text-align:left"><b>root.sleep</b>
      </td>
      <td style="text-align:left">
        <p>Put the prop to sleep.</p>
        <p>Shutdown the prop.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/root/restart</b>
      </td>
      <td style="text-align:left"><b>root.restart</b>
      </td>
      <td style="text-align:left">Restart the prop.</td>
    </tr>
  </tbody>
</table>## WIFI Configuration

<table>
  <thead>
    <tr>
      <th style="text-align:left">OSC command</th>
      <th style="text-align:left">Serial command</th>
      <th style="text-align:left">Parameters</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>/wifi/setCredentials</b>
      </td>
      <td style="text-align:left"><b>wifi.setCredentials</b>
      </td>
      <td style="text-align:left">
        <p><b>SSID</b>: string</p>
        <p><b>password</b>: string</p>
      </td>
      <td style="text-align:left">Set the WIFI name (SSID) and password to which the prop should connect
        to.</td>
    </tr>
  </tbody>
</table>## RGB LED control

<table>
  <thead>
    <tr>
      <th style="text-align:left">OSC Command</th>
      <th style="text-align:left">Serial Command</th>
      <th style="text-align:left">Parameters</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>/leds/mode</b>
      </td>
      <td style="text-align:left"><b>leds.mode</b>
      </td>
      <td style="text-align:left">
        <p>LED mode as string or int</p>
        <p>direct (0)</p>
        <p>system (1)</p>
        <p>stream (2)</p>
        <p>player (3)</p>
      </td>
      <td style="text-align:left">Select the LED mode. Streaming is a UDP live streaming protocol of colors.
        Player is a sequence from the SD card.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/rgb/brightness</b>
      </td>
      <td style="text-align:left"><b>rgb.brightness</b>
      </td>
      <td style="text-align:left"><b>brightness</b>: float</td>
      <td style="text-align:left">Set the brightness of the RGB LEDs.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/rgb/fill</b>
      </td>
      <td style="text-align:left"><b>rgb.fill</b>
      </td>
      <td style="text-align:left">
        <p><b>red</b>: float</p>
        <p><b>green</b>: float</p>
        <p><b>blue</b>: float</p>
      </td>
      <td style="text-align:left">
        <p>Fill all LEDs with a color.</p>
        <p>Serial example setting red:
          <br /><code>rgb.fill 1,0,0</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/rgb/range</b>
      </td>
      <td style="text-align:left"><b>rgb.range</b>
      </td>
      <td style="text-align:left">
        <p><b>red</b>: float</p>
        <p><b>green</b>: float</p>
        <p><b>blue</b>: float</p>
        <p><b>alpha</b>: float</p>
        <p><b>position 1</b>: float</p>
        <p><b>position 2</b>: float</p>
      </td>
      <td style="text-align:left">
        <p>Fill a range of LEDs with a color.</p>
        <p>Serial example setting one half to red:
          <br /><code>rgb.range 1,0,0,1,0,0.5</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/rgb/point</b>
      </td>
      <td style="text-align:left"><b>rgb.point</b>
      </td>
      <td style="text-align:left">
        <p><b>red</b>: float</p>
        <p><b>green</b>: float</p>
        <p><b>blue</b>: float</p>
        <p><b>alpha</b>: float</p>
        <p><b>position 1</b>: float</p>
        <p><b>position 2</b>: float</p>
      </td>
      <td style="text-align:left">Create a point with a color.</td>
    </tr>
  </tbody>
</table>## Player control

These commands provide control over the sequences stored on the SD card of the prop.

<table>
  <thead>
    <tr>
      <th style="text-align:left">OSC command</th>
      <th style="text-align:left">Serial command</th>
      <th style="text-align:left">Parameters</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>/player/load</b>
      </td>
      <td style="text-align:left"><b>player.load</b>
      </td>
      <td style="text-align:left"><b>name</b> of sequence: string</td>
      <td style="text-align:left">Load the sequence with the given name.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/player/play</b>
      </td>
      <td style="text-align:left"><b>player.play</b>
      </td>
      <td style="text-align:left"><b>start time</b> in seconds: float</td>
      <td style="text-align:left">Start the loaded sequence at the start time given.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/player/pause</b>
      </td>
      <td style="text-align:left"><b>player.pause</b>
      </td>
      <td style="text-align:left"><em>no parameter</em>
      </td>
      <td style="text-align:left">Pause the playing sequence.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/player/resume</b>
      </td>
      <td style="text-align:left"><b>player.resume</b>
      </td>
      <td style="text-align:left"><em>no parameter</em>
      </td>
      <td style="text-align:left">Resume the paused sequence.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/player/stop</b>
      </td>
      <td style="text-align:left"><b>player.stop</b>
      </td>
      <td style="text-align:left"><em>no parameter</em>
      </td>
      <td style="text-align:left">Stop the loaded sequence.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/player/seek</b>
      </td>
      <td style="text-align:left"><b>player.seek</b>
      </td>
      <td style="text-align:left"><b>time</b> to seek in seconds: float</td>
      <td style="text-align:left">Seek the given position of a sequence.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/player/id</b>
      </td>
      <td style="text-align:left"><b>player.id</b>
      </td>
      <td style="text-align:left"><b>enabled</b>: boolean</td>
      <td style="text-align:left">Show identification mode of sequence. A way to display/preview which prop
        belongs to which cluster.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/player/delete</b>
      </td>
      <td style="text-align:left"><b>player.delete</b>
      </td>
      <td style="text-align:left"><b>sequence name</b>: string</td>
      <td style="text-align:left">
        <p>Delete the sequence with the given name. This deletes the .colors and
          .meta file of the sequence.
          <br />
        </p>
        <p>Example to delete a sequence called &quot;timeline&quot;:</p>
        <p><code>/player/delete /timeline</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>## Files

These command provide control over the file on the SD card.

<table>
  <thead>
    <tr>
      <th style="text-align:left">OSC command</th>
      <th style="text-align:left">Serial command</th>
      <th style="text-align:left">Parameters</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>/files/delete</b>
      </td>
      <td style="text-align:left"><b>files.delete</b>
      </td>
      <td style="text-align:left"><b>filepath</b>: string</td>
      <td style="text-align:left">
        <p>Delete the file with the given file path.</p>
        <p></p>
        <p>Example to delete the .colors file of the timeline sequence:</p>
        <p><code>/files/delete /timeline.colors</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/files/deleteFolder</b>
      </td>
      <td style="text-align:left"><b>files.deleteFolder</b>
      </td>
      <td style="text-align:left"><b>folderpath</b>: string</td>
      <td style="text-align:left">Delete the folder with the given path.</td>
    </tr>
  </tbody>
</table>## IMU

These commands provide control over the sensor data of the IMU.

| OSC command | Serial command | Parameters | Description |
| :--- | :--- | :--- | :--- |
| **/imu/enabled** | **imu.enabled** | **enable**: boolean | Enable sending of IMU values to the host computer. |
| **/imu/updateRate** | **imu.updateRate** | **rate**: integer | Set the update rate at which the IMU data is sent to the host computer. |

## OSC 

| OSC command | Serial command | Parameters | Description |
| :--- | :--- | :--- | :--- |
| **/osc/enabled** | **osc.enabled** | **enable**: boolean | Enable OSC communication. |

## Serial

| OSC command | Serial command | Parameters | Description |
| :--- | :--- | :--- | :--- |
| /serial/outputEnabled | serial.outputEnabled | enable: boolean | Enable Serial output. |



