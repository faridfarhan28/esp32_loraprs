# Experimental LoRa APRS ESP32 APRSDroid bluetooth modem and LoRa APRS-IS iGate
Tiny experimental amateur radio esp32 based LoRa APRSDroid bluetooth modem and iGate server.

Can be used in two modes: 
- **as LoRa APRS client**, you need to use APRSDroid application, connect to the modem using bluetooth, data will be re-transmitted through the LoRA radio, this is similar to APRSDroid micromodem - https://unsigned.io/micromodem/, received data will be sent back to the APRSDroid using bluetooth
- **as a LoRa APRS iGate server**, which connects to your WiFI and forwards received LoRA APRS positions into the APRS-IS network, it also reports client signal level, by appending it into the APRS comment

# Software Dependencies
- espressif/arduino-esp32 library (install using arduino library manager)
- sandeepmistry/arduino-LoRa (install using arduino library manager)

# Software Setup
- when setting up APRSDroid, use **"TNC (plaintext TNC2)"** connection protocol in Connection Preferences -> Connection Protocol
- go to esp32_loraprs.ino and make next changes based on your requirements
  - comment out / remove LORAPRS_CLIENT define if you are planning to run server mode iGate
  - for server mode fill LORAPRS_WIFI_SSID and LORAPRS_WIFI_KEY with your WiFI AP data
  - for server mode fill LORAPRS_LOGIN and LORAPRS_PASS with APRS-IS login callsign and pass
  - change LORAPRS_FREQ if you are planning to use different frequency, currently it is set to **432.500MHz**, which is 70cm band APRS frequency in IARU-1 region, see http://info.aprs.net/index.php?title=Frequencies
- if you are planning to use different esp32 pinouts for lora and/or different LoRA spread factor / bandwidth then modify loraprs.h
  - lora module CfgPinSs, pin 5
  - lora module CfgPinRst, pin 26
  - lora module CfgPinDio0, pin 14
  - lora bandwidth CfgBw, 20 kHz (to fit into standard 25 kHz channel)
  - lora spread factor CfgSpread, 11 (down to -17.5dB)
  - lora coding rate CfgCodingRate, 7
  - lora output power CfgPower, 20 (set to maximum 20 dBm ~ 100mW, change to lower value if needed)
- use 80 MHz ESP32 frequency in Arduino, it will prolong battery life when operating portable, higher speed is not needed

# Test Results
- **About 4 km** when server is 30m above the ground and client is 2m above the ground
- **About 13 km** when server is 30m above the ground and client is at some higher point ~40m above the ground

# Hardware Photos
