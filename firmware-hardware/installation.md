# Installation

## Flashing the Props

You can use Bento upload the firmware to your props. At the moment it uses the Arduino IDE in the background to do the flashing. 

### **Preparation steps**

* Download and install the Arduino IDE from [https://www.arduino.cc/en/main/software](https://www.arduino.cc/en/main/software)
* [Install the ESP32 board definition](https://github.com/espressif/arduino-esp32#installation-instructions) 
  * Start Arduino and open Preferences window
  * Enter the release links below into _Additional Board Manager URLs_ field. You can add multiple URLs, separating them with commas. Stable release link: [https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package\_esp32\_index.json](https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json)
  * Open Boards Manager from Tools &gt; Board menu and install _esp32_ platform.
* Download the firmware for your prop

  * e.g. firmware for Flowtoy creator clubs are available from the [Bento Github release page](https://github.com/benkuper/BenTo/releases)

### **Flashing the firmware**

* Create a prop by clicking on the green plus icon in the prop panel, select your prop type \(e.g. Flowtoys Creator Club\) .
* Select the prop by clicking on the prop. The inspector will display it's parameters.
* In the container "Connection" select the Serial Device related to your prop.

![](../.gitbook/assets/bento-connection.png)

* Repeat these steps for all props that you want to flash.
* Go to menu "File" =&gt; "Preferences", scroll down to the container called "Bento Settings" and "Flashing.
* For the ESP32 Path click on "Browse" and find the path to your Arduino IDE. Typical locations are:
  * On Windows: C:\Program Files \(x86\)\Arduino
  * On MacOS: /Users/myUsername/Library/Arduino15
* For the Firmware Path click on "Browse" and select the firmware .bin file \(e.g. BentoFlowCreator.ino.bin\). Makes sure that the partitions .bin file is located in the same folder as the firmware \(e.g. BentoFlowCreator.ino.partitions.bin\)
* Click on "Flash Firmware" to flash the props

![](../.gitbook/assets/bento-flashing.png)

## Configuring the WiFi

* Connect your props via Serial \(USB\) connection
* Create props in the props panel and select the correct Serial device in the "Connections" container of the inspector
* Go to the menu "File" =&gt; "Preferences", scroll down to the containers called "Bento Settings" and "WiFi"
* Enter your WiFi SSID \(name of WiFi\) and WiFi password
* Press "Save credentials", this will send the credentials via the Serial connection to the props

![](../.gitbook/assets/bento-wifi-credentials.png)



