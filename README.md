# Liquid Prep - Hardware

Liquid Prep hardware is the device that measures the soil moisture value and is read in the Liquid Prep App to determine the watering advice for the selected crop.

## Table of Contents

1. [Soil Moisture Device Support](#soil-moisture-device-support)
2. [Troubleshooting](#troubleshooting)

## Soil Moisture Device Support

There are 2 options of soil moisture sensor devices supported;

1. **[Arduino UNO](https://www.arduino.cc/)**:
   Please go through the [Arduino UNO setup documentation](./Arduino%20UNO/User-Manual.pdf) for stepwise instructions on how to setup the Arduino based sensor device.
2. **[ESP32](http://esp32.net/)**:

# For End Users
## Flash firmware directly from [Liquid Prep Web Tools](https://playground.github.io/liquid-prep-web-tools/)

# For Developers

## Develop/build firmware with PlatformIO
    Intall PlatformIO plugin in VSCode
    Open "Soil Moisture Sensor" project

    Build & Upload firmware to ESP32

### Notes
    Upload page.json and config.json to update UI
    esptool.py --chip esp32 -p /dev/cu.usbserial-0001 erase_flash
    http://192.168.1.xxx/_ac/update
    http://192.168.1.xxx/_ac/config
    ESP32 default ip 192.168.4.1, 192.168.1.184 

Sets IP address for Soft AP in captive portal. When AutoConnect fails the initial WiFi.begin, it starts the captive portal with the IP address specified this.

The default IP value is 172.217.28.1
password: 12345678


# Set up your soil moisture sensor to work with Liquid Prep
After plugging usb cable and the ESP32 is powered on, you will see an esp32ap as one of your WiFi AP(access point) options.  
- Select esp32ap, the Join "esp32ap" window will pop open. ![Alt text](image1.jpg?raw=true "Title") 
- Select "Configure New AP" from the menu options
- Your WiFi AP should be listed as one of the options
- Select the WiFi you would like join
- Provide the passphrase to join your WiFi, if you want to assign a static ip to the sensor, uncheck "Enable DHCP" then key in the proper values. ![Alt text](image2.jpg?raw=true "Title")
- To calibrate the sensor, go to http://yoursensorip/save_config
- To get moisture level reading go to http://yoursensorip/moisture.json


# References
   Please see the [ESP32 setup video](https://youtu.be/EU28Z_lu67w) for stepwise instructions on how to setup the ESP32 based sensor device.

## Troubleshooting

- **The USB com port isn’t recognized during flashing**
  - Unplug the microcontroller and plug it back in. This will restart it and it should then be recognized.
- **Android bluetooth sometimes does not connect**
  - Unplug the microcontroller and plug it back in. This will restart it and it should then connect.
- **Program size larger than the default**
  - In the IDE, choose a different built-in partition scheme from the Tools menu.
    Click on _Tools > Partition scheme: No OTA (Large APP)_. This will allocate enough memory for it to write.
    ![Partition Scheme Example](/assets/large-app.png)
- **Arduino out of the box is missing libraries needed for the card.**

  - Libraries to include:
    -- [ArduinoJson](https://www.arduino.cc/reference/en/libraries/arduino_json/)
    -- [AsyncTCP](https://github.com/me-no-dev/AsyncTCP)
    -- [AutoConnect](https://www.arduino.cc/reference/en/libraries/autoconnect/)
    -- [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer)
    -- [PageBuilder](https://www.arduino.cc/reference/en/libraries/pagebuilder/)

  - To install a new library into your Arduino IDE\* you can use the Library Manager. Open the IDE and click to the "Sketch" menu and then _Include Library > Manage Libraries_.

  \* It is recommended to use VSCode with the [PlatformIO IDE extension](https://docs.platformio.org/en/latest/integration/ide/vscode.html) instead of Arduino IDE. It is more user-friendly.
