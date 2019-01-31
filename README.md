# pi_scalextric

Have a look at the [schematic](https://aliceliveprojects.github.io/pi_scalextric/).

This is the parent project to the following components:

* [pi_scalextric_mqtt](https://github.com/aliceliveprojects/pi_scalextric_mqtt) contains mqtt broker setup, python scripts and configuration files
* [pi_scalextric_spwa](https://github.com/aliceliveprojects/pi_scalextric_spwa) contains a simple single page web app to control scalextrix cars via mqtt



## How To

Here's how I'm setting up the system:

Please note: to run an MQTT server on Heroku will require a credit card, even if on a free tier. 

The best, safest, way to do this, is to obtain a top-up credit-card, such as one from [Pockit](https://www.pockit.com/) (Other Top-up cards are available). It will ensure that if something goes wrong, and a charge to the card is attempted, there are no funds available, and you won't fall into debt without being aware!

1. Web: Create a project alias on a GMail account

1. Web: Create a Heroku account, using the project alias

1. Web: Create an app in the Heroku account

1. Web: Add the CloudMQTT element to the app in the Heroku account (you'll need to provide a credit card for this)

1. Web: Find the connection details in the app's Config Vars

1. Dev Machine: Use an [MQTT debug client](http://www.mqttfx.org/) to check all is OK

1. Download fresh [Raspbian](https://www.raspberrypi.org/downloads/raspbian/).

1. Pi: [Install](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) onto SD Card.

1. Boot Pi from SD Card, into Desktop

1. Pi: Update Raspbian

1. Pi: Update Node-RED
   1. see [Node-RED update for Raspberry Pi](https://nodered.org/docs/hardware/raspberrypi)
   1. start the Node-RED server, as instructed

1. Pi: Install a [git gui](https://git-cola.github.io/downloads.html) if you really can't be bothered with command line

1. Pi: Clone the [pi_scalextric_node_red](https://github.com/aliceliveprojects/pi_scalextric_node_red) project

1. Pi: Clone the [pi_scalextric_mqtt](https://github.com/aliceliveprojects/pi_scalextric_mqtt) project

1. Pi: Alter the config file:
   * located at path: `<pi_scalextric_mqtt>/mqtt/src/config.json`
      * set the values for the broker as those you have in your MQTT broker account 'details'.
      * set the values for the paths:
         * resources: `<pi_scalextric_mqtt>/mqtt/src/pythonScripts/specialWeaponScripts`
         * throttle: `<pi_scalextric_mqtt>/mqtt/src/pythonScripts/throttleScripts/channel_throttle.py`
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



---

This is the work of [Yusof Bandar](https://github.com/YusofBandar) for [DigitalLabs@MMU](https://digitallabs.mmu.ac.uk/).

<p align="center">
<img align="middle" src="https://trello-attachments.s3.amazonaws.com/5b2caa657bcf194b4d089d48/5b98c7ec64145155e09b5083/d2e189709d3b79aa1222ef6e9b1f3735/DigitalLabsLogo_512x512.png"  />
 </p>
 
 
<p align="center">
<img align="middle" src="https://trello-attachments.s3.amazonaws.com/5b2caa657bcf194b4d089d48/5b98c7ec64145155e09b5083/e5f47675f420face27488d4e5330a48c/logo_mmu.png" />
 </p>

