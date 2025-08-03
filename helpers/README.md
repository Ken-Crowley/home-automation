## usb-serial-drives.sh 
The Open Thread Border Router docker image didn't support `spinel+tcp`:
  - SLZB-MR1 connected into the local network with a PoE cable.
  - Environment variable: `RADIO_URL=spinel+tcp://<SLZB-MR1 ip>:6638>`
  - Log message shows: `The Spinel interface name "spinel+tcp" is not supported!. CreateSpinelInterface() at spinel_manager.cpp:128: Failure.` 

Therefore, the issue was bypassed using `spinel+hdlc+uart`:
  - SLZB-MR1 connected into the Synology NAS with a USB-C to USB-A cable.
  - Environment variable: `RADIO_URL=spinel+hdlc+uart:///dev/ttyUSB0`

However, Synology DSM 7 didn't have a USB driver out-of-the-box that supports the SLZB-MR1. Thus, requiring `usb-serial-drivers.sh`:
  - This script uses `insmod` to insert a loadable kernel module into the running kernel.
  - `cp210x.ko` is a driver for Silicon Labs USB to UART specifically compatible with the DSM 7.2 geminilake kernel module. The SLZB-MR1 is compatible with `cp210x.ko`.
  - This script was placed in `/usr/local/etc/rc.d` so whenever the Synology NAS boots up, the module is loaded.
  - For more information, visit robertklep's [dsm7-usb-serial-drivers github](https://github.com/robertklep/dsm7-usb-serial-drivers)

## switch_ports.sh
The Open Thread Border Router docker image defaults its web ui to `port 80`. However, Synology DSM occupies `port 80` by default. Therefore, to access the otbr web ui, `port 80` is freed up using `switch_ports.sh`:
  - [simplehomelab's guide](https://www.simplehomelab.com/free-ports-80-and-443-on-synology/)
  - [SimpleHomelab's github `switch_ports.sh` script](https://github.com/SimpleHomelab/Docker-Traefik/blob/master/scripts/ds918/switch_ports.sh.example)
  - This script was placed in `/usr/local/etc/rc.d` so whenever the Synology NAS boots up, the ports are freed.

## tunnel.sh
The Open Thread Border Router docker image wants a volume mount for `/dev/net/tun` to create a virtual network to bridge traffic between Thread and the Host. However, the Synology NAS didn't have the `/dev/net/tun` directory and the `tun.ko` kernel module wasn't loaded. Thus, requiring `tunnel.sh`
  - [synoforum post](https://www.synoforum.com/threads/device-dev-net-tun-not-working-anymore-after-docker-update-18-09-0-0513.3074/post-14157)
  - This script was placed in `/usr/local/etc/rc.d` so whenever the Synology NAS boots up, there will always be a `dev/net/tun` directory and the `tun.ko` kernel module is ensured to be loaded.