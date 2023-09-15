forked from tbrasser and nldroid/CustomP1UartComponent
currently works well with belgian digital powermeter, HA 2023.6.1, espHome 2023.5.5


________________
This build can be used to read DSMR data from the P1 port of belgian smart meters with an NodeMCU ESP8266 module and pubish the result in [Home Assistant](https://www.home-assistant.io/).




The work is based on these projects:
- https://esphome.io/components/sensor/dsmr.html?highlight=dsmr (espHome component to read the P1 port) 
- https://github.com/tbrasser/CustomP1UartComponent 
- http://domoticx.com/p1-poort-slimme-meter-uitlezen-hardware/ (Information about hardware requirements. Examples for inverters.)

## Hardware

I used a NodeMCU ESP8266 to connect to the P1 port. 
You need some kind of [hardware inverter]. i used a 7404 chip: SN74HC04N (https://en.wikipedia.org/wiki/Inverter_(logic_gate)) because the UART component doesn't support inverting the signal with a software setting.
I read that the ESP32 does have this inverter function, but ESP32 doesn't like my espHome setup for some reason.

The board is powered by the smart meter, so no external powersuply is needed.

## Schema
![image](https://github.com/Ritchie3/-DSMR-reader_P1_espHome/assets/38915268/9f9ded24-6341-4eef-99a5-76b21675f805)


P1 port
![image](https://github.com/Ritchie3/-DSMR-reader_P1_espHome/assets/38915268/343186bc-0682-4f4e-bde2-d47c0838caad)


## Software
Use the dsmr-esp8266.yaml file as a template in espHome. No additional files are needed.

![sensors_HA](https://github.com/Ritchie3/-DSMR-reader_P1_espHome/assets/38915268/b54d1bf1-7437-4f43-87cc-427821b67ac0)


![image](https://github.com/Ritchie3/-DSMR-reader_P1_espHome/assets/38915268/06b6e0f8-4e81-4d2f-8344-6f74dda1f93c)

## Limitations
The software is only usable for meters with [8N1](https://en.wikipedia.org/wiki/8-N-1) serial communication. This is the case for newer dsmr protocols. Older procols use 7E1. You can change the software and shift the char one bit (c &= ~(1 << 7);).
Real old dsmr protocols don't have a CRC at the end of a telegram and the dsmr parser that i use, doesn't support these old protocols.

## Experimental board with case

![20230914_144743](https://github.com/Ritchie3/-DSMR-reader_P1_espHome/assets/38915268/0edca32b-7665-41a1-ad3f-a6523922e091)

## Final Build

![smartmeter with dsrm reader](https://github.com/Ritchie3/-DSMR-reader_P1_espHome/assets/38915268/2797e778-fa76-41f4-90e8-3298401b4d52)
