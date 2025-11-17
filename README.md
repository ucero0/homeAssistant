# Home Assistant Docker Setup

Complete Docker Compose setup for Home Assistant with Zigbee, MQTT, and automation tools.

## 🏠 What's Included

- **Home Assistant** - Smart home automation platform
- **Mosquitto** - MQTT broker for device communication
- **Zigbee2MQTT** - Zigbee coordinator with web UI
- **Node-RED** - Visual automation builder

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose installed
- Linux system (for USB device access)
- Sonoff Zigbee/Thread USB dongle (or compatible)

### Installation

1. **Clone this repository:**
   ```bash
   git clone <repository-url>
   cd homeAssistant
   ```

2. **Configure USB device path:**
   - Update `docker-compose.yml` with your USB device path
   - Default: `/dev/ttyUSB0` or use persistent path like `/dev/serial/by-id/...`

3. **Start services:**
   ```bash
   docker-compose up -d
   ```

4. **Access services:**
   - Home Assistant: http://localhost:8123
   - Zigbee2MQTT: http://localhost:8080
   - Node-RED: http://localhost:1880
   - Mosquitto: Port 1883 (MQTT)

## 📁 Project Structure

```
homeAssistant/
├── docker-compose.yml          # Main Docker Compose configuration
├── config/                     # Home Assistant configuration (auto-created)
├── mosquitto/                  # Mosquitto MQTT broker
│   ├── config/                 # Mosquitto configuration
│   ├── data/                   # MQTT data (gitignored)
│   └── log/                    # Logs (gitignored)
├── zigbee2mqtt/                # Zigbee2MQTT configuration
│   └── data/                   # Zigbee2MQTT data (gitignored)
└── node-red/                   # Node-RED configuration
    └── data/                   # Node-RED flows (gitignored)
```

## 🔧 Configuration

### USB Device Setup

The setup uses a Sonoff Zigbee/Thread USB dongle. Update the device path in `docker-compose.yml`:

```yaml
devices:
  - /dev/ttyUSB0:/dev/ttyUSB0  # Update with your device path
```

**Recommended:** Use persistent device paths:
```yaml
devices:
  - /dev/serial/by-id/usb-ITEAD_SONOFF_Zigbee_3.0_USB_Dongle_Plus_*-if00:/dev/ttyUSB0
```

### MQTT Authentication

By default, Mosquitto allows anonymous connections. To enable authentication:

1. Create user:
   ```bash
   docker exec -it mosquitto mosquitto_passwd -c /mosquitto/config/passwd username
   ```

2. Edit `mosquitto/config/mosquitto.conf`:
   - Set `allow_anonymous false`
   - Uncomment `password_file /mosquitto/config/passwd`

3. Restart: `docker-compose restart mosquitto`

See `mosquitto/CREATE_USER.md` for details.

## 📚 Documentation

- **[COMPANION_SERVICES.md](COMPANION_SERVICES.md)** - Available companion services
- **[ZHA_VS_ZIGBEE2MQTT.md](ZHA_VS_ZIGBEE2MQTT.md)** - Zigbee coordinator comparison
- **[MATTER_COMPATIBILITY.md](MATTER_COMPATIBILITY.md)** - Matter device support
- **[SONOFF_DONGLE_SETUP.md](SONOFF_DONGLE_SETUP.md)** - Sonoff dongle configuration
- **[mosquitto/README.md](mosquitto/README.md)** - Mosquitto setup guide
- **[zigbee2mqtt/SETUP.md](zigbee2mqtt/SETUP.md)** - Zigbee2MQTT setup
- **[node-red/SETUP.md](node-red/SETUP.md)** - Node-RED setup

## 🔌 Services

### Home Assistant
- **Port:** 8123
- **Access:** http://localhost:8123
- **Config:** `./config/`

### Zigbee2MQTT
- **Port:** 8080
- **Access:** http://localhost:8080
- **MQTT:** Connects to Mosquitto automatically

### Node-RED
- **Port:** 1880
- **Access:** http://localhost:1880
- **Integration:** Connect via Home Assistant → Add Integration → Node-RED

### Mosquitto
- **MQTT Port:** 1883
- **WebSocket Port:** 9001
- **Config:** `./mosquitto/config/`

## 🔒 Security Notes

- Change default passwords before production use
- Enable MQTT authentication for production
- Use persistent USB device paths
- Backup `config/` directory regularly
- Review `secrets.yaml` (not in git)

## 🛠️ Maintenance

### Update Services
```bash
docker-compose pull
docker-compose up -d
```

### View Logs
```bash
docker-compose logs -f [service-name]
```

### Backup Configuration
```bash
# Backup Home Assistant config
cp -r config/ config_backup_$(date +%Y%m%d)/
```

## 📝 License

This project is provided as-is for personal use.

## 🤝 Contributing

Feel free to submit issues or pull requests for improvements.

## ⚠️ Important Notes

- USB device paths may vary - check with `ls -l /dev/tty*`
- First run will create configuration files automatically
- Data directories (data/, log/) are gitignored
- Sensitive files (secrets.yaml, passwd) are gitignored

## 🆘 Troubleshooting

### USB Device Not Found
- Check device path: `ls -l /dev/tty*`
- Verify permissions
- Try persistent path: `/dev/serial/by-id/`

### Services Won't Start
- Check logs: `docker-compose logs [service]`
- Verify ports aren't in use
- Check Docker permissions

### MQTT Connection Issues
- Verify Mosquitto is running
- Check network configuration
- Review authentication settings

## 📞 Support

For issues specific to:
- **Home Assistant:** https://www.home-assistant.io/help/
- **Zigbee2MQTT:** https://www.zigbee2mqtt.io/
- **Node-RED:** https://nodered.org/docs/
- **Mosquitto:** https://mosquitto.org/documentation/

---

**Happy Automating!** 🏠✨

