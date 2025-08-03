## System Details
- **Host**: [Synology NAS DS224+](https://www.synology.com/en-us/products/DS224+) [DSM 7.2.1-69057 Update 5]
- **Zigbee Coordinator**: [SMLight SLZB-MR1](https://smlight.tech/product/slzb-mr1/) PoE [CC2652P7 20240315] 
  - [Third Reality Zigbee Smart Button](https://3reality.com/product/smart-button/) [3RSB22BZ v1.00.35]
  - [Third Reality Zigbee Smart Plug Gen2](https://3reality.com/product/smart-plug-gen2-with-energy-monitoring/) [3RSP02028BZ v1.00.92]
- **Matter-over-Thread**: [SMLight SLZB-MR1](https://smlight.tech/product/slzb-mr1/) USB [EFR32MG21 20241105]
  - [Level Matter Bolt](https://level.co/smart-lock/smart-deadbolt/) [3.4]
  - _Note_: Matter-over-Thread requires IPv6 enabled on the Host.

### Docker [24.0.2 build 610b8d0]
Start containers: `sudo docker compose -f 'docker-compose.yml' up -d --build`

Stop containers: `sudo docker compose stop`

All containers set to run with `network_mode: host` and `privileged: true`

### Home Assistant [2025.7.2]

Web Frontend: `http://<Host ip>:8123`
  - MQTT integration:
    - `<Host ip>` for broker and `1883` for port
  - SMLIGHT SLZB integration:
    - `<Zigbee Coordinator ip>` for URL
  - Matter integration:
    - `ws://<Host ip>:5580/ws` for URL
    - To add matter device, using phone app go to `Settings > Devices & services > Devices tab > + ADD DEVICE > Add Matter device`
  - Open Thread Border Router integration:
    - `http://127.0.0.1:8081` for URL
  - Thread integration:
    - Set Open Thread Border Router as preferred network
    - Select `Use router for Android + iOS credentials`
    - Using phone app go to `Settings > Companion App > Troubleshooting > Sync Thread credentials`, run sync twice so the message reads "*Home Assistant and this device use the same network*"

### Matter [8.0.0]
Web Frontend: `http://<Host ip>:5580`

### Open Thread Border Router [latest]
Web Frontend: `http://127.0.0.1:80` inside host

Rest API:  `http://127.0.0.1:8081` inside host