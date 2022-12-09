# VPN torrenting system files and info

## `transmission`

install `transmission-cli` with your package manager

drop `transmission.service` into `/usr/lib/systemd/system/transmission.service`

tinker with the settings in `/var/lib/transmission/.config/transmission-daemon/settings.json`

you need to set the transmission setting `rpc-whitelist-enabled` to `false` in the `settings.json` file if you want to use the transmission web client to manage your torrents

## Surfshark VPN

install `openvpn` with your package manager

follow [this guide](https://support.surfshark.com/hc/en-us/articles/360011051133-How-to-set-up-manual-OpenVPN-connection-using-Linux-Terminal-) to get surfshark's `.ovpn` config files

use the `surfshark.service` `systemd` unit file in this repo, drop it in `/etc/systemd/system/surfshark.service`

## `/etc/fstab` to setup automounting an external drive

user `mkdir` to make the `/var/torrents/` directory

find your external drive with `lsblk`

create partition, and format with `fdisk` and `mkfs.ext4`

use `blkid` to find the disk's UUID

add the following to your `/etc/fstab` file to automount your new partition
```
UUID=<uuid from blkid goes here>       /var/torrents   ext4    noexec,nofail,  0 2
# EXAMPLE: UUID=e10cc9ae-ce54-4fa7-a58a-000fc56eb0f0       /var/torrents   ext4    noexec,nofail,  0 2
```

you can just reboot here, to get it to mount, or `mount` it directly to `/var/torrents` and `systemctl daemon-reload`

## `minidlna`
install `minidlna` with your package manager

in `/etc/minidlna.conf` change `media_dir` to `/var/torrents/complete`

give your minidlna server a friendly name by changing the `friendly_name` setting

sometimes `enable_subtitles` actually works with VLC, go ahead and explicitly enable it

run `systemctl enable --now minidlna.service ` to enable and turn on minidlna

you can test if its working by pulling up VLC on your favorite device, navigating to `Universal Plug'n'Play` and seeing if you friendly named server shows up there
