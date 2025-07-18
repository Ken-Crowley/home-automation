# Pre-requisites
- Docker
- Zigbee2mqtt hub (I'm using an SMLight SLZB-06 PoE)

# Setup
1. Run `docker compose -f 'docker-compose.yml' up -d --build`
2. Type localhost:8123 in web browser to access home assistant. Go through the onboarding steps.
3. On home assistant dashboard, go to Settings -> Devices & services -> ADD INTEGRATION
4. Search for MQTT and add MQTT.
5. Enter mqtt as the broker and 1883 for the port.
6. Type localhost:8485 in web browser to access zigbee2mqtt. Go through the onboarding procedure.
    - Coordinator/Apater Port/Path: For SMLight SLZB-06, use `tcp://slzb-06.local:6638`.
    - MQQT Server: I had to replace `localhost` with the IP address of the mqqt server.
    - Home assistant enabled?: `True`
7. Within zigbee2mqtt web browser, Click Permit join (All) to pair zigbee devices.
8. I've paired a zigbee button and zigbee plug (this updates the zigbee2mqtt configuration.yml file).
9. Add automation script to home assistant (seen in automations.yaml).