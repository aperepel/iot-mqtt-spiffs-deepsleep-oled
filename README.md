# Overview
This is an evolution of the https://github.com/aperepel/iot-esp8266-starter project. Changelog:

* Added an MQTT support. Demo of an online/offline pattern with LWT and Retain messages. Send a message to show on a display.
* Externalized a number of configuration properties in a JSON file (MQTT broker, topic names, etc.). Hosted on ESP8266 SPIFFS file system.
* TODO - demo of how to create and upload a FS firmware image with PlatformIO
* More robust WiFi lifecycle. Moved connection logic from `setup()` to a `loop()`. If an access point is no longer available, wipe the credentials and transition into a SmartConfig mode after 30 seconds (TODO - make it configurable via the same `/data/config.json`?)
* The button now displays basic info and puts the system in `Deep Sleep` mode for 5 minutes (TODO - make this configurable too.) Upon awakening, reconnects to the MQTT broker.
* Updated wiring to support deep sleep - added a jumper between `D0` and `RST` pin)

# Building the Code
```
# serial port monitor part is optional, but nice
platformio run -t upload && platformio serialports monitor --baud 115200
```
# Building the File System
TODO add instructions

# IDE Support
Really, any IDE which PlatformIO supports will do (which in practice means everything.)
From free offerings I prefer Eclipse CDT for C++ development (a piece of me dies every time I use
Eclipse, but it still is light years ahead of other free alternatives for IoT development ;) )
```
# read PlatformIO reference docs for details, but here's an Eclipse example (respond Y when prompted)
platformio init --ide eclipse --board esp12e
```
In Eclipse, right-click in the project pane -> Import from Existing sources.

# Notes
* The `ESP_SSD1306` library is a display driver fork of the `Adafruit_SSD1306` with changes required for ESP8266.
* I had to inline the `Adafruit_GFX` library to pick up a more recent version from the one listed in PlatformIO repos.
# iot-mqtt-spiffs-deepsleep-oled
