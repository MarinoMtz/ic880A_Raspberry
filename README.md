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

    1.1 On a linux machine install the rpi-imager `sudo apt install rpi-imager` 
    
    1.2 Download and install the SO (Raspberry Pi OS 32-bit) `sudo rpi-imager` 

2. Configure the WiFi network acces 

    2.1 Open the raspi-config `sudo raspi-config`
    
    2.2 Scan for wireless networks `sudo iwlist wlan0 scan`
    
    2.3 Open and edit the configuration gile `sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`
    
    2.4 Add the following at the begining of the file with the corresponging parameters
    ```
    network={
    ssid="testing"
    psk="testingPassword"
    }
   ```
    2.5 Get the IP address `hostname -I`
   
3. Enable SSH

    3.1 Open the raspi-config `sudo raspi-config`
    
    3.2 Select `Interfacing Options` > `SSH` > `Yes` > `Ok` > `Finish`
    
    3.3 Conec to to the Raspberry using `ssh pi@<IP>`

4. Clone this repository `git clone https://github.com/MarinoMtz/ic880A_Raspberry.git`

5. Install the HAL Driver `cd /ic880A_Raspberry/lora_gateway` > `sudo make`

6. Install the Semtech Packet Forwarder `cd /ic880A_Raspberry/packet_forwarder ` > `sudo make`

7. Reset the SPI `cd /ic880A_Raspberry/SPI_reset ` > `sh SPI_reset.sh`

8. Edit the .json files

9. Install Chirpstack gateway [chirpstack.io](https://www.chirpstack.io/project/install/requirements/) 

    9.1 Install Mosquitto `sudo apt install mosquitto`
    
    9.2 `sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1CE2AFD36DBCCA00 `
    
    9.3 `sudo echo "deb https://artifacts.chirpstack.io/packages/3.x/deb stable main" | sudo tee /etc/apt/sources.list.d/chirpstack.list `
    
    9.4 `sudo apt update`
    
    9.5 `sudo apt install chirpstack-gateway-bridge`

10. Add the different processes at reboot

    10.1 Edit the `/etc/rc.local` file by adding this at the end of the file:

    ```
    sudo systemctl start chirpstack-gateway-bridge
    (cd /home/pi/ic880A_Raspberry/SPI_reset; sudo sh SPI_reset.sh)
    (cd /home/pi/ic880A_Raspberry/packet_forwarder/lora_pkt_fwd; ./lora_pkt_fwd)
    ```
