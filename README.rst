home-assistant-pi-ssd-setup
###########################

Collection of several configs and command snippets to make our Raspberry Pi 3 B
boot with a X3pro Black 2-USB3.1 250GB SSD.

Since the bootloader does not recognize the USB SSD, run bootloader, kernel+dtb
from SD card, everything else from SSD. Mount SD card to /boot to receive
dtb/kernel updates as usual.

How to SSD
**********

- write Raspbian image to SSD

- remove boot partition (e.g. via gparted) to prevent partuuid confusion

- resize service makes SSD boot scenario fail, so remove it from SSD:

  rm /etc/init.d/resize2fs_once
  rm /etc/rc3.d/S01resize2fs_once

- check if cmdline.txt on SD card needs adaption, see cmdline.txt for a working
  version in this repo (mainly increase loglevel)

- use /etc/fstab from this repo (UUID points to SD card for /boot)

- resize remaining partition to maximum size (e.g. via gparted)

How To SD Card
**************

- write Raspbian image to SSD

- remove all partitions but "boot" from SD

- resize remaining partition, so there is no unallocated space present after
  (e.g. via gparted)

- enable_uart=1 in config.txt for debugging
