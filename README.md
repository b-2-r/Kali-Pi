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

***Change password***

```sh
$ passwd
...
```

***Change SSH host keys***

```sh
$ rm /etc/ssh/ssh_host_*
$ dpkg-reconfigure openssh-server
$ service ssh restart
```

***WIFI***

Generate PSK.

```sh
$ wpa_passphrase [SSID] | grep psk | tail -n1 >> /etc/network/interfaces
```

Add wlan0 to /etc/network/interfaces.

```sh
auto wlan0
iface wlan0 inet dhcp
   wpa-ssid [SSID]
   wpa-psk [Generated PSK]
```

Reboot to apply changes.

```sh
reboot
```

***Vino***

Install vino.

```sh
$ apt-get update
$ apt-get install vino
```

Disable encryption and confirmation.

```sh
$ gsettings set org.gnome.Vino require-encryption false
$ gsettings set org.gnome.Vino prompt-enabled false
```

Create a desktop entry to let vino autostart.

```sh
cd ~/.config && mkdir autostart && cd autostart && touch vino.desktop && vim.tiny vino.desktop 
```

Add the following lines.

```sh
[Desktop Entry]
Type=Application
Name=Vino
Exec=/usr/lib/vino/vino-server
NoDisplay=true
```
