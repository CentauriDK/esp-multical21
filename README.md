# esp-multical21

Added MQTT data upload to the project from weetmuts original the values was only send to the serial terminal.
And how the data is written to the serial terminal.

Added MQTT username and password to the code and example credentials.h
If no username and password are set on the MQTT server, change the commented lines in main.cpp

   ```c++
   // connect client to retainable last will message without credentials
  // return mqttClient.connect(ESP_NAME, "/watermeter/online", 0, true, "False");

  // connect client to retainable last will message with credentials
  return mqttClient.connect(ESP_NAME, MQTT_USER, MQTT_PASS, "/watermeter/online", 0, true, "False");
   ```

Recieve MQTT Topics via
"/watermeter/mydatajson" and 
"/watermeter/mydata"

ESP8266 decrypts wireless MBus frames from a Multical21 water meter

A CC1101 868 MHz modul is connected via SPI to the ESP8266 an configured to receive Wireless MBus frames.
The Multical21 is sending every 16 seconds wireless MBus frames (Mode C1, frame type B). The encrypted
frames are received from the ESP8266 an it decrypts them with AES-128-CTR. The meter information 
(total counter, target counter, medium temperature, ambient temperature, alalm flags (BURST, LEAK, DRY,
REVERSE) are sent via MQTT to a smarthomeNG/smartVISU service (running on a raspberry).

Thanks to [weetmuts](https://github.com/weetmuts) for his great job on the wmbusmeters.
