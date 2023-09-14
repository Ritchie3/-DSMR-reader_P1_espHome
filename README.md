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
![image](https://github.com/Ritchie3/-DSMR-reader_P1_espHome/assets/38915268/2ac84993-d76a-437d-9c02-53222dd9e1bc)

## Software
Use the .yaml file as a template in espHome. No additional files are needed.

## Limitations
The software is only usable for meters with [8N1](https://en.wikipedia.org/wiki/8-N-1) serial communication. This is the case for newer dsmr protocols. Older procols use 7E1. You can change the software and shift the char one bit (c &= ~(1 << 7);).
Real old dsmr protocols don't have a CRC at the end of a telegram and the dsmr parser that i use, doesn't support these old protocols.

## Experimental board with case

![20230914_144743](https://github.com/Ritchie3/-DSMR-reader_P1_espHome/assets/38915268/0edca32b-7665-41a1-ad3f-a6523922e091)
