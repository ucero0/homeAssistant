# Mosquitto MQTT Broker Setup

## Initial Setup

The Mosquitto broker is configured to require authentication. You need to create a password file before starting the container.

### Option 1: Create password file using Docker (Recommended)

1. Start the Mosquitto container temporarily:
   ```bash
   docker-compose up -d mosquitto
   ```

2. Create a password file with a user (replace `mqtt_user` and `mqtt_password` with your desired credentials):
   ```bash
   docker exec -it mosquitto mosquitto_passwd -c /mosquitto/config/passwd mqtt_user
   ```
   (Enter your password when prompted)

3. Restart the container:
   ```bash
   docker-compose restart mosquitto
   ```

### Option 2: Allow anonymous connections (Less secure, for testing)

Edit `mosquitto/config/mosquitto.conf` and change:
```
allow_anonymous false
```
to:
```
allow_anonymous true
```

Then comment out or remove the `password_file` line.

## Connecting Home Assistant to Mosquitto

With bridge networking, Home Assistant connects to Mosquitto using the container name.

1. Go to **Settings** → **Devices & Services** in Home Assistant
2. Click **Add Integration**
3. Search for **MQTT**
4. Enter the following:
   - **Broker**: `mosquitto` (container name, or use `localhost` if accessing from outside Docker)
   - **Port**: `1883`
   - **Username**: Your MQTT username (leave empty if anonymous connections are allowed)
   - **Password**: Your MQTT password (leave empty if anonymous connections are allowed)

**Note**: Since both services are on the same Docker network, use `mosquitto` as the broker hostname. This uses Docker's internal DNS for service discovery.

## Default Ports

- **MQTT**: 1883
- **MQTT over WebSocket**: 9001 (if enabled)

## Logs

Mosquitto logs are stored in `./mosquitto/log/mosquitto.log`

