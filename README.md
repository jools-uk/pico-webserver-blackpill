# pico-webserver-blackpill

Webserver example that came with TinyUSB slightly modified to run on a Raspberry Pi Pico.
This version is for a generic Chinese RP2040 board that I'm calling the 'RP2040 Black Pill'. Possibly a clone of the VCC-GND manufactured board.
Lets the Pico pretend to be a USB Ethernet device. Runs a webinterface at http://192.168.7.1/

## Build dependencies

On Debian:

```
sudo apt install git build-essential cmake gcc-arm-none-eabi
```

Your Linux distribution does need to provide a recent CMake (3.13+).
If not, compile [CMake from source](https://cmake.org/download/#latest) first.

## Build instructions

```
git clone --depth 1 https://github.com/maxnet/pico-webserver
cd pico-webserver
git submodule update --init
mkdir -p build
cd build
cmake ..
make
```

Copy the resulting pico_webserver.uf2 file to the Pico mass storage device manually.
Webserver will be available at http://192.168.7.1/

Content it is serving is in /fs
If you change any files there, run ./regen-fsdata.sh

By default it shows a webpage that led you toggle the Pico's led, and allows you to switch to BOOTSEL mode.

## Ubunut note
The USB Ethernet device might not initialize unless, 1 you set NetworkManager to allow all network devices:
https://askubuntu.com/questions/1026358/usb-ethernet-interface-in-virtual-ubuntu-18-04-disabled-after-every-reboot
Or manually bring the interface up (well the dhclient):
sudo dhclient usb0
