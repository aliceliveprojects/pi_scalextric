# pi_scalextric

Have a look at the [schematic](https://aliceliveprojects.github.io/pi_scalextric/).

## Project Structure
* [pi_scalextric_mqtt](https://github.com/aliceliveprojects/pi_scalextric_mqtt) contains mqtt broker setup, python scripts and configuration files
* [pi_scalextric_spwa](https://github.com/aliceliveprojects/pi_scalextric_spwa) contains a simple single page web app to control scalextrix cars via mqtt
* [alice-mqtt-broker](https://github.com/aliceliveprojects/alice-mqtt-broker) contains an Aedes MQTT broker implementation, with in-memory persistence, ready for deployment on Heroku. Supports websockets only.
* [alice-mqtt-dynamic](https://github.com/aliceliveprojects/alice-mqtt-dynamic) contains an implementation of the Node-RED mqtt-dynamic node, which supports communication to an MQTT broker via websockets.

---

# Summary
This is the parent project covering the above projects, which use a Rasberry Pi to  control a modified Scalextric set. 

1. Set-up a development system connecting the Raspberry Pi and your PC / Mac, via a local network connection, using a router. 
1. Deploy `alice-mqtt-broker` to Heroku.
1. Clone `pi_scalextric_mqtt` onto Raspberry Pi:
   1. Edit the `config.json`, `resources.json` and `sensors.json` files with appropriate details
   1. Run `node-red-start` and import the `mqtt_flow.json` flow into Node-RED
   1. Change global context: configPath to the absolute path to the `config.json` file
   1. In Node-RED:  Setup new Mqtt connections for each Mqtt module and deploy
1. Clone `alice-mqtt-dynamic` to the Raspberry Pi
   1. Use the instructions in the repo to replace the mqtt-dynamic node with `alice-mqtt-dynamic`.
1. Deploy `pi_scalextric_spwa` to GitHub pages.
1. Create a QR Code wich will load the SPWA onto a recent Android or iPhone:
   1. On the RPi: Run `python qrCodeGen.py [PATH_TO_CONFIG_FILE] [HOST_OF_SPWA]`
   1. Generated Qr code can be scanned to direct users to SPWA

## How To

Here's how I'm setting up the system:

1. Web: Create a project alias on a GMail account

1. Web: Create a Heroku account, using the project alias

1. Web: Create an app in the Heroku account

1. Web: Connect Heroku to the `alice-mqtt-broker` and deploy

1. Dev Machine: Use an [MQTT debug client](https://chrome.google.com/webstore/detail/mqttbox/kaajoficamnjijhkeomgfljpicifbkaf) to check all is OK

1. Download fresh [Raspbian](https://www.raspberrypi.org/downloads/raspbian/).

1. Pi: [Install](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) onto SD Card.

1. Boot Pi from SD Card, into Desktop

1. Pi: Update Raspbian

1. Pi: Update Node-RED
   1. see [Node-RED update for Raspberry Pi](https://nodered.org/docs/hardware/raspberrypi)
   1. start the Node-RED server, as instructed

1. Install the development environment:
   1. see [Development Environment](https://github.com/aliceliveprojects/little_blue_pi/blob/master/documentation/worklogs/27.01.2020.md)

1. Pi: Clone the [pi_scalextric_mqtt](https://github.com/aliceliveprojects/pi_scalextric_mqtt) project
   1. we'll refer to it as <pi_scalextric_mqtt>
1. Pi: Alter the config file:
   * located at path: `<pi_scalextric_mqtt>/mqtt/src/config.json`
      * set the values for the broker as those you have in your MQTT broker account settings
      * set the values for the paths:
         * resources: `<pi_scalextric_mqtt>/mqtt/src/pythonScripts/specialWeaponScripts`
         * sensors: `<pi_scalextric_mqtt>/mqtt/src/pythonScripts/sensorScripts/sensors.py`
1. Pi: Node-RED: import the project:
   * Edit `<pi_scalextric_node_red>/node_red_flow.txt`. Select all,copy to clipboard.
   * Install missing node types, using the 'Manage Palette' menu.
      * (Note: If this doesn't exist, you don't have npm running)
      * install `node-red-contrib-mqtt-dynamictopic`: NOTE really important not to confuse this with node-red-contrib-mqtt-dynamic
      * install `node-red-contrib-grovepi`
1. Pi: Node-RED: change parameters
   *  Mqtt Subscribe: Set Global Context: configPath
      * set value to the path: `<pi_scalextric_mqtt>/mqtt/src/config.json`
   *  Mqtt Subscribe: Set sensor definition path
      * Set value on the Sensors File node: `<pi_scalextric_mqtt>/mqtt/src/sensors.json`
1. Pi:Node-RED: set the mqtt connection parameters
   * select any one of the Nodes of type: **mqtt-dynamic**
   * in the [sidebar](https://nodered.org/docs/user-guide/editor/) click on the gear icon to bring up the configuration
   * the configuration sets the values for all nodes of this type.
   * set the MQTT connection info to the same as that entered for the `config.json`
1. Pi: Python: Install packages for mqtt - python checks the sensor values and sends to MQTT.
   * `pip install paho-mqtt`
   




Useful refs:

[Raspbian Download Page](https://www.raspberrypi.org/downloads/raspbian/)

[MQTT.fx](http://www.mqttfx.org/)

[GitCola](https://git-cola.github.io/downloads.html)

[pi pinout](https://pinout.xyz/)

[LED](https://www.electronics2000.co.uk/pin-out/led.php)

[resistor lookup](https://www.digikey.co.uk/en/resources/conversion-calculators/conversion-calculator-resistor-color-code-4-band)

[TIP3055 (NPN)](https://github.com/aliceliveprojects/pi_scalextric/blob/master/documentation/resources/TIP3055-D.PDF)

[back emf supression](https://progeny.co.uk/back-emf-suppression/)

[grove pi board](https://www.seeedstudio.com/GrovePi-p-2241.html) - used for convenience

[grove pi ir reflective sensors](https://www.seeedstudio.com/Grove-Infrared-Reflective-Sensor-v1-2-p-2791.html) - used for lap-times


---

This is the work of [Yusof Bandar](https://github.com/YusofBandar) for [DigitalLabs@MMU](https://digitallabs.mmu.ac.uk/).

<p align="center">
<img align="middle" src="https://trello-attachments.s3.amazonaws.com/5b2caa657bcf194b4d089d48/5b98c7ec64145155e09b5083/d2e189709d3b79aa1222ef6e9b1f3735/DigitalLabsLogo_512x512.png"  />
 </p>
 
 
<p align="center">
<img align="middle" src="https://trello-attachments.s3.amazonaws.com/5b2caa657bcf194b4d089d48/5b98c7ec64145155e09b5083/e5f47675f420face27488d4e5330a48c/logo_mmu.png" />
 </p>

