# Home Assistant Companion Services Guide

This guide explains the optional companion services you can add to your Home Assistant Docker setup.

## 🚀 Quick Start

All services are commented out in `docker-compose.yml`. To enable a service:

1. Uncomment the service block (remove the `#` characters)
2. Create the required directories
3. Run `docker-compose up -d`
4. Configure the service and integrate with Home Assistant

---

## 📊 Available Services

### 1. **Node-RED** (Most Popular!)

**What it does:**
- Visual drag-and-drop automation builder
- More powerful than YAML for complex automations
- Flow-based programming interface

**Port:** `1880`  
**Why use it:**  
- Create complex automations visually
- Better for advanced logic and conditions
- Great for API integrations and webhooks

**Setup:**
1. Uncomment the `nodered` service in docker-compose.yml
2. Run: `docker-compose up -d nodered`
3. Access: `http://localhost:1880`
4. In Home Assistant: Settings → Add Integration → Node-RED
5. Install Home Assistant nodes in Node-RED

**Directory:** `./node-red/data`

---

### 2. **InfluxDB + Grafana** (Metrics & Visualization)

**What they do:**
- **InfluxDB**: Time-series database for storing sensor data
- **Grafana**: Beautiful dashboards and graphs

**Ports:** 
- InfluxDB: `8086`
- Grafana: `3000`

**Why use them:**
- Long-term data storage (beyond Home Assistant's default retention)
- Advanced visualization with custom dashboards
- Historical trend analysis
- Better for analytics and reporting

**Setup:**
1. Uncomment both `influxdb` and `grafana` services
2. Run: `docker-compose up -d influxdb grafana`
3. Access Grafana: `http://localhost:3000` (admin/admin)
4. In Home Assistant: Settings → Add Integration → InfluxDB
5. Configure Grafana to connect to InfluxDB

**Directories:**
- `./influxdb/data`
- `./influxdb/config`
- `./grafana/data`

**⚠️ Important:** Change default passwords in docker-compose.yml before enabling!

---

### 3. **Zigbee2MQTT** (Alternative Zigbee Coordinator)

**What it does:**
- Alternative to ZHA (Zigbee Home Automation)
- More device support
- Better web UI for device management
- Over-the-air firmware updates

**Port:** `8080`  
**Why use it:**
- Supports more Zigbee devices
- Better device pairing experience
- Can update device firmware OTA

**⚠️ Important:** 
- **DO NOT use both ZHA and Zigbee2MQTT at the same time!**
- They both need access to `/dev/ttyUSB0`
- Choose one: either ZHA (via Home Assistant) OR Zigbee2MQTT

**Setup:**
1. Disable ZHA in Home Assistant first
2. Uncomment `zigbee2mqtt` service
3. Configure device path in `zigbee2mqtt/data/configuration.yaml`
4. Run: `docker-compose up -d zigbee2mqtt`
5. Access: `http://localhost:8080`
6. In Home Assistant: Settings → Add Integration → MQTT (Zigbee2MQTT publishes to MQTT)

**Directory:** `./zigbee2mqtt/data`

---

### 4. **ESPHome** (ESP32/ESP8266 Device Management)

**What it does:**
- Manage and program ESP32/ESP8266 devices
- Create custom sensors and devices
- Over-the-air (OTA) firmware updates
- YAML-based device configuration

**Port:** `6052`  
**Why use it:**
- Build custom smart devices
- Program ESP boards remotely
- Integrate DIY sensors and switches
- No need to flash devices manually

**Setup:**
1. Uncomment the `esphome` service
2. Run: `docker-compose up -d esphome`
3. Access: `http://localhost:6052`
4. Create device configurations
5. In Home Assistant: ESPHome devices auto-discover

**Directory:** `./esphome/config`

---

## 🎯 Recommendations

### **Start Here:**
1. **Node-RED** - Most useful for automations
2. **ESPHome** - If you have ESP32/ESP8266 devices

### **For Advanced Users:**
3. **InfluxDB + Grafana** - For data analysis and long-term storage
4. **Zigbee2MQTT** - If you need more Zigbee device support

---

## 🔧 Enabling a Service

1. Edit `docker-compose.yml`
2. Find the service you want (e.g., `# nodered:`)
3. Uncomment all lines for that service (remove `#`)
4. Create directories if needed:
   ```bash
   mkdir -p node-red/data
   ```
5. Start the service:
   ```bash
   docker-compose up -d nodered
   ```
6. Configure and integrate with Home Assistant

---

## 📚 Additional Resources

- **Node-RED**: https://nodered.org/docs/
- **InfluxDB**: https://docs.influxdata.com/influxdb/
- **Grafana**: https://grafana.com/docs/
- **Zigbee2MQTT**: https://www.zigbee2mqtt.io/
- **ESPHome**: https://esphome.io/

---

## 🔐 Security Notes

- **Always change default passwords** before enabling services
- Use environment variables for sensitive data
- Consider adding authentication to web UIs
- Keep services updated: `docker-compose pull && docker-compose up -d`

---

## 🆘 Troubleshooting

### Service won't start?
- Check logs: `docker-compose logs <service-name>`
- Verify directories exist and have correct permissions
- Check port conflicts: `netstat -tuln | grep <port>`

### Can't access web UI?
- Verify the port is correct in docker-compose.yml
- Check firewall settings
- Ensure container is running: `docker ps`

### Integration not working in Home Assistant?
- Verify both services are on the same Docker network
- Check service logs for connection errors
- Restart Home Assistant after adding integration

