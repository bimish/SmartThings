# Generic HTTP Device
Link to the project: https://community.smartthings.com/t/43335

This project consists of a Raspberry Pi running Raspbian OS. It runs HTTPD with index.php as the source. The PHP runs the gpio command in order to enable the pins on the Pi. The code sample in the PHP file causes a relay to momentarily turn on then off. I'm using this on a gate so the short/momentary capability was key. However, it's very customizable and now offers on/off states for both switches. For advanced/full instructions on installing and configuring Raspbian OS, see the project link below.

The code and project expanded to the use of Atmel/AVR devices like Arduino UNO/Nano/Mega and the WIFI capable SOC like ESP8266/NodeMCU/WeMos D1 Mini. The code can use the popular Ethernet module ENC28J60 using a custom library linked below:
https://github.com/UIPEthernet/UIPEthernet

The Groovy file is the Device Handler for SmartThings.
index.php is meant to reside in /var/www/html folder of the Raspbery Pi and runs the external gpio command in Linux.
At the top of index.php, change the first variable to "true" instead of "false" and this will make the PHP page protected with basic authentication. After making that change, make sure to change the SmartThings preferences for the device.
The *.ino files are the Arduino IDE code samples. Verify the few options at the top of the script before flashing your device.

This project was tested successfully via an external IP, Pollster and with an Amazon Echo/Alexa. Echo can run TWO functions in my app. The ON command triggers the main function and OFF triggers the custom function but can be changed to only control the Main switch.

</br>v1.0.20170126 - NodeMCU sketch DHT sensor retry logic is a bit smarter. Small bug fixes.
</br>v1.0.20170121 - NodeMCU sketch is now able to do OTA updates via a web-page or directly via the Arduino IDE.
</br>v1.0.20170110 - Arduino & NodeMCU code updated. Stateful on/off functionality fixed. DHT sensor will now retry 5 times so should return results with more success than before. DHT part number displayed.
</br>v1.0.20170108 - ESP8266/NodeMCU can now be wired with an ENC28J60 using modified UIPEthernet library. Ability to use transistor/mosfet rather than relays. Reboot is now optionally modified via the web-page & stored in the first byte of the EEPROM thus the setting will survive a reboot or a flash. ST code now will work with an invalid header (impacts ESP8266 & ENC28J60 unreliability). Wiring diagrams updated.
</br>v1.0.20161231 - Arduino sketch enhancements & fixes: Added free memory/heap logic. UpTime reports day/days correctly now. Replaced reboot logic with a simple while loop to cause a soft watchdog reset. Switched to use5Vrelay=true to match wiring diagrams. Added abort when favicon.ico request is sent.
</br>v1.0.20161223 - Added UpTime for the Arduino IDE samples. Added device name & IP at the top of SmartThings screen. Added wiring for Arduino Nano & a generic ENC28J60 ethernet board.
</br>v1.0.20160806 - Security issue with the ESP8266 library, read this post: https://community.smartthings.com/t/esp8266-nodemcu-arduino-based-tv-remote/50161/22
</br>v1.0.20160731 - Added Arduino Nano v3 plus ENC28J60 Ethenet Shield sample code. Updated wiring diagrams.
</br>v1.0.20160719 - NodeMCU enhancements: forcing reboot every 8 hours to guarantee device being up. Also added simple variable to control whether using 5v or 3.3v relays & whether logic sends a HIGH or a LOW depending on that variable. Added temperature & humidity support for DHT11, DHT22 & DHT21.
</br>v1.0.20160604 - Added Arduino / ESP8266-12E / NodeMCU Support and a code sample to GitHub.
</br>v1.0.20160430 - Main and Custom switches can now be momentary or have on/off states. GPIO pin numbers for Main/Custom is now configurable. Ability to force Echo/Alexa to be restricted in controlling the Main switch when running ON/OFF commands when configured to be stateful ON/OFF (not momentary). Refresh works and updates Main/Custom tile per the GPIO pin status. Version contains lots of enhancements, bug fixes and future proofing.
</br>v1.0.20160428 - Now able to control in preferences whether CustomTrigger is momentary or has states like on/off. This is the CUSTOM tile, which can easily be made as the MAIN/primary tile, search top of ST code for MAIN designation & change to CustomTrigger.
</br>v1.0.20160423 - Small changes: using second line of df -h for space used. Scaling GPIO image better for RPi 3 with more lines on gpio readall command.
</br>v1.0.20160410 - Changing device ID to random number at end of execution so multiple devices can point to one IP. Amazon Echo can run both ON/main and OFF/custom functions. Added ability to output GPIO status in PHP. Releasing another ST device that will pull the image and control the installation of required packages hence the reset of device ID.
</br>v1.0.20160407 - Added Poll & Refresh to execute the TEST function. Now able to add the switch to Pollster and should see the time update in Test Triggered. Validated external IP with custom port and Amazon Echo/Alexa.
</br>v1.0.20160406 - Added the CustomTrigger button. Made buttons smaller. CPU Temp now accurately converts C to F. Added color to some tiles. Defaulting in port & body if left empty in prefs.
</br>v1.0.20160405 - Modified Space Used to use awk instead of cut and delimiters. GitHub reported bug.
</br>v1.0.20160402 - Added JSON support. Modified Reboot tile with states. Added Clear Tiles button.
</br>v1.0.20160328 - Modified tile background while in "running" states and added free memory tile.
</br>v1.0.20160327 - Toggling tile states in general and with respect to authentication. Fixed GPIO in the PHP script to be correct and toggle on then off. Used to have off then on, which is incorrect.
</br>v1.0.20160326 - Added temperature. Added basic authentication.
</br>v1.0.20160323 - Initial version
</br>
<img src="https://raw.githubusercontent.com/JZ-SmartThings/SmartThings/master/Devices/Generic%20HTTP%20Device/Screenshot_Android_App.png">
<img src="https://raw.githubusercontent.com/JZ-SmartThings/SmartThings/master/Devices/Generic%20HTTP%20Device/Screenshot_PHP_Page.png">
<img src="https://raw.githubusercontent.com/JZ-SmartThings/SmartThings/master/Devices/Generic%20HTTP%20Device/Screenshot_Arduino.png">
<img src="https://raw.githubusercontent.com/JZ-SmartThings/SmartThings/master/Devices/Generic%20HTTP%20Device/Screenhot_Prototype.jpg">
<img src="https://raw.githubusercontent.com/JZ-SmartThings/SmartThings/master/Devices/Generic%20HTTP%20Device/WIRING/NodeMCU-DualRelay5V.png">
<img src="https://raw.githubusercontent.com/JZ-SmartThings/SmartThings/master/Devices/Generic%20HTTP%20Device/WIRING/NodeMCU-ENC28J60-DualRelay5V.png">
<img src="https://raw.githubusercontent.com/JZ-SmartThings/SmartThings/master/Devices/Generic%20HTTP%20Device/WIRING/ArduinoNano-DualRelay5V.png">
<img src="https://raw.githubusercontent.com/JZ-SmartThings/SmartThings/master/Devices/Generic%20HTTP%20Device/WIRING/ArduinoNano-ENC28J60-DualRelay5V.png">
<img src="https://raw.githubusercontent.com/JZ-SmartThings/SmartThings/master/Devices/Generic%20HTTP%20Device/WIRING/ArduinoUNO-ENC28J60-DualRelay5V.png">