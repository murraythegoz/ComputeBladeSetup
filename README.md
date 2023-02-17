# ComputeBladeSetup
steps to setup a compute blade


*BOOTLOADER UPDATE and CONF*
this will update the bootloader binary (e.g. to support NVMe and HTTP boot), and configure the boot order

Requirements:

For bootloader updates you need at least a physical pc or VM running linux or Mac.
Windows and WSL DO NOT WORK
1) install usbboot\\
> sudo apt install libusb-1.0-0-dev
> git clone --depth=1 https://github.com/raspberrypi/usbboot
> cd usbboot
>make


2) prepare latest eprom and set boot order
cd recovery
nano boot.conf

> ENABLE_UART=1
according to https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#configuration-properties, this would set (right to left) as NVMe(6),SDCard/eMMC(1),netboot

> BOOT_CONF=0xf216


mv pieeprom.original.bin
curl -L -o pieeprom.original.bin  https://github.com/raspberrypi/rpi-eeprom/raw/master/firmware/stable/pieeprom-2022-12-07.bin
