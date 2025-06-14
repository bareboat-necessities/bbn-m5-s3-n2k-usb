
# DIY NMEA N2K to USB gateway in Actisense format on M5AtomS3 Lite

Effectively equivalent of NGT-1.

Powered by USB. CanBus isolated. (Connect H and L only)


<p align="center">
<img src="./images/M5_AtomS3_lite-NMEA2000-to-USB.jpg?raw=true" alt="BBN NMEA-2000 to USB Gateway" style="width: 50%; height: auto;" />
</p>

<p align="center">
<img src="./images/BBN_NMEA2000_to_USB.jpg?raw=true" alt="M5 AtomS3-Lite NMEA-2000 to USB Gateway" style="width: 30%; height: auto;" />

<img src="./images/BBN_AtomS3-lite_n2k_usb_gw.jpg?raw=true" alt="ESP32 NMEA-2000 to USB Gateway" style="width: 30%; height: auto;" />
</p>

## Required Hardware:


- M5AtomS3 Lite:   https://shop.m5stack.com/products/atoms3-lite-esp32s3-dev-kit
- CAN CAIS3050G module for M5Atom (for N2K):   https://shop.m5stack.com/products/atomic-canbus-base-ca-is3050g

## Suggested enclosure and connectors

Waterproof ABS Plastic Enclosure Box Electronic Ip67 Flanged, Clear Cover, Size 100x68x50 (mm)

https://www.aliexpress.us/item/3256806147195874.html

Panel mount USB-C connector. USB-C 3.1 IP67 waterproof cable type c 90 degree male to female panel car ship dashboard installation connector

https://www.aliexpress.us/item/3256801869230308.html

Panel mount NMEA-2000 connector with pig tails. 
M12 5 Pin Male Connector Cable, A Coded Straight Back Mount Cable Waterproof Male Aviation Socket UnShielded Electrical Cable IP67 Sensor Receptacle
Brand: FOWIUNYE

https://www.amazon.com/Connector-Waterproof-UnShielded-Electrical-Receptacle/dp/B0CB6SCTJ1

M3 Standoffs

## Setup in SignalK

To register gateway in SignalK

- Connect to USB 2.0 port on pi (I had drops of N2K data stream when connected to USB 3.0 on external hub)
- find out /dev/tty* USB device of gateway (in your raspberry pi with BBN OS or other Linux). Use a symbolic link to it under /dev/serial/by-id/ when adding a SignalK connection in the next step.
- and add N2K connection with Source Type (Actisense AGT-1 Canboat-js) baud rate: 115200

## Flashing firmware on Bareboat Necessities OS

````
# shutdown signalk
sudo systemctl stop signalk

if [ -f bbn-flash-m5-s3-n2k-usb.sh ]; then rm bbn-flash-m5-s3-n2k-usb.sh; fi
wget https://raw.githubusercontent.com/bareboat-necessities/my-bareboat/refs/heads/master/m5stack-tools/bbn-flash-m5-s3-n2k-usb.sh
chmod +x bbn-flash-m5-s3-n2k-usb.sh
./bbn-flash-m5-s3-n2k-usb.sh -p /dev/ttyACM0
````

## Picture

<p align="center">
<img src="./nmea2000_to_usb_atomS3.jpg?raw=true" alt="BBN NMEA 2000 to USB gateway on atomS3" />
</p>


## Troubleshooting

- Normal working behavior is fast flashing blue status light indicating traffic passed.

## Patches

NMEA2000_esp32 forked from https://github.com/ttlappalainen/NMEA2000_esp32
with mod for TWAI driver (for esp32-S3)
https://github.com/skarlsson/NMEA2000_twai

## Alt versions

For m5stack atom-lite use: 

https://github.com/bareboat-necessities/bbn-nmea200-m5atom/tree/main/bbn-nmea2000-usb-gw-m5atom

## Other Bareboat Necessities Devices

Project Home:  https://bareboat-necessities.github.io/

- Alarms Box: https://github.com/bareboat-necessities/bbn_alarms_A
- Engine Sensors Box: https://github.com/bareboat-necessities/bbn_sensors_hub_C
- Sensors Hub: https://github.com/bareboat-necessities/bbn_sensors_hub_AB
- NMEA N2K to USB: https://github.com/bareboat-necessities/bbn-m5-s3-n2k-usb
- Instruments Displays on esp32: https://github.com/bareboat-necessities/bbn-m5stack-tough
- Boat Heave Sensor: https://github.com/bareboat-necessities/bbn-wave-period-esp32
- I2C over USB for Linux: https://github.com/bareboat-necessities/bbn-i2c-over-usb
- N2K Senders: https://github.com/bareboat-necessities/bbn-m5-s3-n2k-i2c
