# Pre-requisites
- Docker
- Zigbee2mqtt hub (I'm using an SMLight SLZB-06 PoE)

# Setup
1. Run `docker compose -f 'docker-compose.yml' up -d --build`
2. Type `localhost:8123` in web browser to access home assistant. Go through the onboarding steps.
3. On home assistant dashboard, go to Settings -> Devices & services -> ADD INTEGRATION
4. Search for MQTT and add MQTT.
5. Enter mqtt as the broker and 1883 for the port.
6. Type `localhost:8485` in web browser to access zigbee2mqtt. Go through the onboarding procedure.
    - Coordinator/Apater Port/Path: For SMLight SLZB-06, use `tcp://slzb-06.local:6638`.
    - MQQT Server: I had to replace `localhost` with the IP address of the mqqt server. Using hostname of mqqt doesn't seem to work.
    - Home assistant enabled?: `True`
7. The onboarding procedure will automatically update the zigbee2mqtt `configuration.yml` file
8. Within zigbee2mqtt web browser (`localhost:8485`), Click Permit join (All) to pair zigbee devices.
9. Pairing zigbee devices will update the zigbee2mqtt `configuration.yml` file.
10. Now you can add automation scripts (`automations.yml` file) to home assistant using zigbee devices.
    - See the `zigbee-button-toggle-plug` branch I made that connects the zigbee button and zigbee plug devices and grabs their states in the automation script so the button toggles the plug.