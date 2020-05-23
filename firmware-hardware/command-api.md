# Command API

The command API defines a set of commands that can be sent to a prop via OSC or Serial connection. The structure of the commands is the same for both connection types.

For example the following commands can be used to put the prop to sleep/shutdown:

* OSC: /root/sleep 
* Serial: root.sleep 

The OSC messages are **sent to port 9000** of the prop. OSC feedback \(e.g. button press, orientation data\) from the prop is sent to port 10000 on the host machine.  
For sending through serial connection you send a string. The baud rate for the serial connection is 115200.

## Detecting props

To detect props on the network you send a broadcast message to the network with the OSC address /yo containing the IP of your computer as a string. The prop will send feedbacks to the IP address received by the /yo message. It will respond with a /wassup message containing the IP address, MAC address and name of the prop. 

| OSC Command | Serial Command | Description |
| :--- | :--- | :--- |
| /yo  | N/A | Broadcast message to all props. Request props to send a wassup message to communicate it's IP address. |

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
      <td style="text-align:left">/root/sleep</td>
      <td style="text-align:left">root.sleep</td>
      <td style="text-align:left">
        <p>Put the prop to sleep.</p>
        <p>Shutdown the prop.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">/root/restart</td>
      <td style="text-align:left">root.restart</td>
      <td style="text-align:left">Restart the prop.</td>
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
      <td style="text-align:left">leds.mode</td>
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
      <td style="text-align:left">rgb.brightness</td>
      <td style="text-align:left"><b>brightness</b>: float</td>
      <td style="text-align:left">Set the brightness of the RGB LEDs.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>/rgb/fill</b>
      </td>
      <td style="text-align:left">rgb.fill</td>
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
      <td style="text-align:left">rgb.range</td>
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
      <td style="text-align:left">rgb.point</td>
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
</table>