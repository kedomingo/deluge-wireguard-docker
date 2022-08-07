# Wireguard + Deluge Torrent docker container

This uses the [binhex/arch-delugevpn](https://hub.docker.com/r/binhex/arch-delugevpn/) image to create a torrent docker container
with a built-in kill switch.

This is a pre-configured docker-compose file for Wireguard users. Put your `.conf` file inside the `config/wireguard/` directory.

### `LAN_NETWORK` CIDR

The only config that you might need to change is the value for the `LAN_NETWORK` under `environment` in the yaml file. Please change
this to the correct CIDR of your local network. If you type `ifconfig | grep netmask`, your machine's IP will be the one that is not `127.0.0.1`

If you are not sure, you can go to the [Wikipedia](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#IPv4_CIDR_blocks) page and find the
netmask displayed from the previous command under the `Mask` column of the table. The CIDR will be your IP but modified to follow the format in the `Address format` column.

For example `ifconfig | grep netmask` results to the following

```
	inet 127.0.0.1 netmask 0xff000000
	inet 192.168.1.188 netmask 0xffffff00 broadcast 192.168.1.255
```

The netmask `0xffffff00` is in hex and can be formatted as `ff.ff.ff.00`. The decimal conversion is `255.255.255.0`

For this netmask, the CIDR format is `a.b.c.0/24` so we get the first 3 parts of the local IP address, use `0` as the fourth component and append `/24`

For this example, the CIDR will be `192.168.1.0/24`.
