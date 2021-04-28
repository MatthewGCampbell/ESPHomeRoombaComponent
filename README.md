# Roomba Component for ESPHome (for old models without wifi)

*THIS IS JUST FORK FROM GREAT COMPONNENT https://github.com/mannkind/ESPHomeRoombaComponent AND ALL CREDITS GOES TO THE AUTHOR. I JUST UPDATED THE INSTRUCTIONS AND EXAMPLES SINCE SOME THINGS IN ORIGINAL DOCUMENTATION HAVE ERRORS AND SOME NEEDED TO BE UPDATED.*

A barebones wrapper to enable control of a Roomba via MQTT with ESPHome.
Tested with ESPHome 1.16.2, and a Roomba 614 with adafruit hazzah installed.

![Sensors data](/docs/Annotation%202020-04-27%20102809.jpg)
![Commands](/docs/Annotation%202020-04-27%20102837.jpg)

## Hardware

The inspiration for this project is https://github.com/johnboiles/esp-roomba-mqtt. 

Since most of the users nowdays use cheap Wemos D1 mini developpment board, also wiring needs to be updated.

Most arduino boards have issues reading sensor data from the roomba, since the drive strength of a Roomba TX line is not enough to drive the RX line of another board (for example, in some revisions of Arduino). In this case, a simple PNP transistor (2N2907A, 2N3906, or 2N4403, among others) can be used to provide enough “drive” for the Arduino.

Since Wemos D1 mini uses 5v (or 3.3v), but roomba gives out up to 20v (when charging), you need to use simple DC-DC converter to have stabilized 5v power. I am using cheap 8-12V to usb converters from aliexpress.

The wiring mentioned in the tread above uses many wires and resistors, but everything could be much simplified. My wiring diagram:
![Wiring](/docs/wiring.jpg)

![Roomba pinout](https://community-home-assistant-assets.s3-us-west-2.amazonaws.com/original/2X/c/c1a32634d0727a8b8e8d1db0a5ec1219799d5ccc.png)

I will also draw my schema, but for refference you may use also this one **just select correct pins on arduino!**
![Adruino uno example](https://i.stack.imgur.com/aaifY.jpg)

# If you are using a D1 mini
The D1 mini is small enough to fit into the compartment by the wheel. The [example image of D1 mini inside Roomba compartment](https://community-home-assistant-assets.s3.dualstack.us-west-2.amazonaws.com/optimized/2X/a/a258c7253f8bd3fe76ad9e7aa1202b60bd113d74_2_496x600.jpg) image is not a photo of mine specifically, but it's useful to see where the components fit inside the Roomba. It was sourced from a [community project thread on the Home Assistant forums](https://community.home-assistant.io/t/add-wifi-to-an-older-roomba/23282).

## Board Setup

The origional creator used a D1 mini but i opted for a ESP-01 [Amazon](https://www.amazon.com/MakerFocus-Wireless-Transceiver-DC3-0-3-6V-Compatible/dp/B01EA3UJJ4/ref=asc_df_B01EA3UJJ4/?tag=hyprod-20&linkCode=df0&hvadid=309773039951&hvpos=&hvnetw=g&hvrand=4985446750337794805&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9010259&hvtargid=pla-599566692924&psc=1)as it was the smallest one i could find, I added female pins on my circuit oard so that i could easilly switch out chips and reflash if needed (Might add a onbaord debug port on my next revision)

![Example Circuit Board I made (Cut the side to see if it would fit but it didn't )](/docs/Beta 1.jpeg)
![My Board](/docs/Beta_1.jpeg)
![How I placed it inside the roomba](/docs/wires.jpeg)
![How I placed it inside the roomba](/docs/inside_roomba.jpeg)

## Software Setup/Use

Take a look at the example directory for a fully working example. My code has some fixes from original

* [<example/esphome.yaml>](/example/homeassistant-vacuum.yaml)  - code for configuration.yaml to integrate as a "MQTT Vacuum" in Home Assistant
* [<example/roomba.yaml>](/example/roomba.yaml)  - code for ESPhome
