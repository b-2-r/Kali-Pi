### Install Kali Linux

Look at partition table to identify SD card.

```sh
$ diskutil list
...
...
/dev/disk2 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *15.5 GB    disk2
   1:             Windows_FAT_32 PI                      64.0 MB    disk2s1
   2:                      Linux                         7.3 GB     disk2s2
```

Format SD card to FAT32.

```sh
$ sudo diskutil eraseDisk FAT32 KALI MBRFormat /dev/disk2
```

Image Kali Linux img file to the SD card.

```sh
$ sudo diskutil unmountDisk /dev/disk2 # First unmount
$ sudo dd if=kali-2.1.2-rpi2.img of=/dev/disk2 bs=512k # See status with INFO signal (Ctrl+T)
```

### Setup Kali Linux

***Keyboard layout***

```sh
$ dpkg-reconfigure keyboard-configuration
$ reboot
```

***Wifi***
