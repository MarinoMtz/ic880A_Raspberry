# LoRa Gateway (ic880A with Raspberry)
Gateway LoRa iC880 with Chirpstack forwader
This repository helps you install a LoRa Gateway using the LoRa iC880 Concentrator (for the EU Region), a Raspberry Pi 3 and the Chirpstack forwarder.

## Hardware Needed

* Raspberry Pi 3.0 with 
* iC880 Concentrator
* SD Card (> 8GB)

## Software Requirements

* Semtech Packet Forwarder
* HAL Gateway Driver 
* MQTT Broker 
* Chripstack Gateway Bridge

## Install

1. Operative System for the Raspberry Pi [Raspbian](https://www.raspberrypi.org/documentation/installation/installing-images/)

    1.1 On a linux machine install the rpi-imager `<sudo apt install rpi-imager>` 
    1.2 Download and install the SO (Raspberry Pi OS 32-bit) `<sudo rpi-imager>` 

2. Configure the WiFi network acces 

    2.1 Open the raspi-config `<sudo raspi-config>`
    
    4.2 Scan for wireless networks `<sudo iwlist wlan0 scan>`
    
    6.3 Open and edit the configuration gile `<sudo nano /etc/wpa_supplicant/wpa_supplicant.conf>`
    
    8.3 `<network={
         ssid="testing"
         psk="testingPassword"
         } >`
    
