# Samyoga

## Under Construction by 0xh3nry
---
Samyoga is a utility of which various combinations can be made/developed to perform certain tasks of car hacking. The starting motto of this project is to control a car using PS4 gaming controller using a physical device implanted/connected to vehicles OBD-II port.But, it is not limited just for that.

### Construction:

This is a device made upof raspberry pi + USBtin + OBD-II male connector, here we need to set up first in Raspberry pi the ability to connect with the gaming controller, so we run ds4drv which checks for the bluetooth gaming controllers and connects with it. Now we need run a script(I wrote a python script) where mapping of the function goes. Basically i am making an automated script which pushes certain CAN command into CAN bus of the connected.

### Tech Required
Things which you need to setup one

* [Raspberry Pi]().
* [USBtin](https://www.fischl.de/usbtin/).
* OBD-II connector.
* USB 2.0 Cable A to Mini B cable.

### Compiling.

we must install some stuff before and prepare Raspberry for the job. We need, 

* [Prepare linux-can and CAN utils](https://www.fischl.de/usbtin/linux_can_socketcan/).
* [Prepare raspberry pi](http://elinux.org/RPi_CANBus).

### Setup.

First make Prepare Raspberry PI for CAN bus,The Raspberry Pi doesn't have CAN bus built in, but it can be added through USB or SPI converters.

Now open terminal in pi and run
```
Load Kernel modules for CAN:
$ sudo modprobe can
$ sudo modprobe can-raw
$ sudo modprobe slcan

compile can-utils:
$ git clone https://github.com/linux-can/can-utils.git
$ cd can-utils
$ make

To coomunicate with vehicle:
$ sudo ./slcan_attach -f -s6 -o /dev/ttyACM0
attached tty /dev/ttyACM0 to netdevice slcan0
$ sudo ./slcand ttyACM0 slcan0
$ sudo ifconfig slcan0 up
```
Here my baud rate is 500k so -s6, after this run the ds4drv connect it controller and run the mapping script. here in mapping script we will map the keys with the command it should execute. 

