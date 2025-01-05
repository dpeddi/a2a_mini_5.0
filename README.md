#A2A Mini 5.0

https://it.aliexpress.com/item/1005005731655421.html

The firmware isn't the stock one, I've dumped the flash after a firmware upgrade.

# Flash
https://www.lcsc.com/datasheet/lcsc_datasheet_2005251034_XTX-XT25F128BSSIGT_C558844.pdf

# Flash reading with rpi
https://tomvanveen.eu/flashing-bios-chip-raspberry-pi/


git clone https://github.com/flashrom/flashrom.git
cd flashrom

meson setup builddir
meson compile -C builddir

builddir/flashrom -p linux_spi:dev=/dev/spidev0.0,spispeed=20000 
builddir/flashrom -p linux_spi:dev=/dev/spidev0.0,spispeed=20000 -r XT25F128B-20khz.img --progress

builddir/flashrom -p linux_spi:dev=/dev/spidev0.0,spispeed=512
builddir/flashrom -p linux_spi:dev=/dev/spidev0.0,spispeed=512 -r XT25F128B-512.img --progress


Once you get the bootparm partition you can identify all the other partitions:

2048K(boot),2048K(recovery),4352K(rootfs),256K(env),4608K(customer),64K(private),1024K(logo)

# Serial log:
```
U-Boot(09/04/2024-01:46:14)
[ 362.166436] reboot: Restarting system
[ 362.170522] Restarting Linux version 4.9.191 (os@machine) (gcc version 6.4.1 (OpenWrt/Linaro GCC 6.4-2017.11 2017-11) ) #4 PREEMPT Mon Nov 4 11:58:23 UTC 2024
[ 362.170522]

U-Boot(09/04/2024-01:46:14)
```

It seems they muted the serial output. 

In the bootloader argument passed to the kernel I have loglevel=3 (should be warning) so no info related to Linux


