# Pre-requisites
- Docker Desktop
- Zigbee2mqtt hub (This uses a SMLight slzb-06 PoE)

# Setup
1. Run `docker compose -f 'docker-compose.yml' up -d --build`
2. Type localhost:8123 in web browser to access home assistant.
3. On home assistant dashboard, go to Settings -> Devices & services -> ADD INTEGRATION
4. Search for MQTT and add MQTT.
5. Enter mqtt as the broker and 1883 for the port.
6. Type localhost:8485 in web browser to access zigbee2mqtt
7. Click Permit join (All) to pair zigbee devices.
8. I've paired a zigbee button and zigbee plug (seen in zigbee2mqtt configuration file)
9. Add automation script! I've created an automation (seen in automations.yaml) to toggle the zigbee plug with the zigbee button