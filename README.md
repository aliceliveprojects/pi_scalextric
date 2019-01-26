# pi_scalextric

Have a look at the [schematic](https://aliceliveprojects.github.io/pi_scalextric/).

This is the parent project to the following components:

* [pi_scalextric_node_red](https://github.com/aliceliveprojects/pi_scalextric_node_red)
* [pi_scalextric_mqtt](https://github.com/aliceliveprojects/pi_scalextric_mqtt)
* [pi_scalextric_spwa](https://github.com/aliceliveprojects/pi_scalextric_spwa)



## How To

Here's how I'm setting up the system:

Please note: to run an MQTT server on Heroku will require a credit card, even if on a free tier. 

The best, safest, way to do this, is to obtain a top-up credit-card, such as one from [Pockit](https://www.pockit.com/) (Other Top-up cards are available). It will ensure that if something goes wrong, and a charge to the card is attempted, there are no funds available, and you won't fall into debt without being aware!

1. Download fresh [Raspbian](https://www.raspberrypi.org/downloads/raspbian/).

2. Pi: [Install](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) onto SD Card.

3. Pi: Update Raspbian

4. Pi: Check for updates - Node-RED on Raspbian

5. Pi: Check for updates -  Python on Raspbian

6. Pi: Install a [git gui](https://git-cola.github.io/downloads.html) if you really can't be bothered with command line

7. Web: Create a project alias on a GMail account

8. Web: Create a Heroku account, using the project alias

9. Web: Create an app in the Heroku account

10. Web: Add the CloudMQTT element to the app in the Heroku account (you'll need to provide a credit card for this)

11. Web: Find the connection details in the app's Config Vars

12. Dev Machine: Use an [MQTT debug client](http://www.mqttfx.org/) to check all is OK




Useful refs:

[Raspbian Download Page](https://www.raspberrypi.org/downloads/raspbian/)

[MQTT.fx](http://www.mqttfx.org/)

[GitCola](https://git-cola.github.io/downloads.html)

[pi pinout](https://www.digikey.co.uk/en/resources/conversion-calculators/conversion-calculator-resistor-color-code-4-band)

[resistor lookup](https://www.digikey.co.uk/en/resources/conversion-calculators/conversion-calculator-resistor-color-code-4-band)

[TIP3055 (NPN)](https://github.com/aliceliveprojects/pi_scalextric/blob/master/documentation/resources/TIP3055-D.PDF)

[back emf supression](https://progeny.co.uk/back-emf-suppression/)