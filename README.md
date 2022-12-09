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
