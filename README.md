# Roomba Component for ESPHome

*THIS IS JUST FORK FROM GREAT COMPONNENT https://github.com/mannkind/ESPHomeRoombaComponent AND ALL CREDITS GOES TO THE AUTHOR. I JUST UPDATED THE INSTRUCTIONS AND EXAMPLES SINCE SOME THINGS IN ORIGINAL DOCUMENTATION HAVE ERRORS AND SOME NEEDED TO BE UPDATED.*

A barebones wrapper to enable control of a Roomba via MQTT with ESPHome.
Tested with ESPHome 1.14.x, and a Roomba 650 w/a Wemos D1 Mini installed.

![Sensors data](/docs/Annotation%202020-04-27%20102809.jpg)
![Commands](/docs/Annotation%202020-04-27%20102837.jpg)

## Hardware

The inspiration for this project is https://github.com/johnboiles/esp-roomba-mqtt. 

Since most of the users nowdays use cheap Wemos D1 mini developpment board, also wiring needs to be updated.

Most arduino boards have issues reading sensor data from the roomba, since the drive strength of a Roomba TX line is not enough to drive the RX line of another board (for example, in some revisions of Arduino). In this case, a simple PNP transistor (2N2907A, 2N3906, or 2N4403, among others) can be used to provide enough “drive” for the Arduino.

Since Wemos D1 mini uses 5v (or 3.3v), but roomba gives out up to 20v (when charging), you need to use simple DC-DC converter to have stabilized 5v power. I am using cheap 8-12V to usb converters from aliexpress.

The wiring mentioned in the tread above uses many wires and resistors, but everything could be much simplified. My wiring diagram:
![Wiring](/docs/wiring.jpg)

I will also draw my schema, but for refference you may use also this one **just select correct pins on arduino!**
![Adruino uno example](ttps://i.stack.imgur.com/aaifY.jpg)

The D1 mini is small enough to fit into the compartment by the wheel. The [example image of D1 mini inside Roomba compartment](https://community-home-assistant-assets.s3.dualstack.us-west-2.amazonaws.com/optimized/2X/a/a258c7253f8bd3fe76ad9e7aa1202b60bd113d74_2_496x600.jpg) image is not a photo of mine specifically, but it's useful to see where the components fit inside the Roomba. It was sourced from a [community project thread on the Home Assistant forums](https://community.home-assistant.io/t/add-wifi-to-an-older-roomba/23282).

## Software Setup/Use

Take a look at the example directory for a fully working example. My code has some fixes from original

* <example/esphome.yaml> - Contains the bits needed for ESPHome.
* <example/homeassistant-vacuum.yaml> - Contains the bits needed to integrate as a "MQTT Vacuum" in Home Assistant
