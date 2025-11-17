# Zigbee2MQTT Setup Guide

## ✅ Configuration Complete!

Your Zigbee2MQTT is now configured and ready to use.

---

## 🚀 First Time Setup

### 1. **Start the Services**

```bash
docker-compose up -d
```

This will start:
- Mosquitto (MQTT broker)
- Zigbee2MQTT
- Home Assistant

### 2. **Access Zigbee2MQTT Web UI**

Open your browser and go to:
```
http://localhost:8080
```

You should see the Zigbee2MQTT dashboard.

### 3. **Check Configuration**

The configuration file is at: `zigbee2mqtt/data/configuration.yaml`

It's already configured to:
- ✅ Connect to Mosquitto at `mosquitto:1883`
- ✅ Use your USB device at `/dev/ttyUSB0`
- ✅ Enable Home Assistant integration
- ✅ Enable web UI on port 8080

### 4. **Connect Home Assistant to Zigbee2MQTT**

1. Go to **Home Assistant** → **Settings** → **Devices & Services**
2. Click **Add Integration**
3. Search for **MQTT**
4. Enter:
   - **Broker**: `mosquitto` (container name)
   - **Port**: `1883`
   - **Username/Password**: Leave empty (if anonymous allowed) or use your MQTT credentials

5. Zigbee2MQTT devices will automatically appear!

---

## 📱 Adding Your First Device

### **Method 1: Via Zigbee2MQTT Web UI** (Recommended)

1. Open Zigbee2MQTT web UI: `http://localhost:8080`
2. Click **"Permit join"** button (top right)
3. Put your Zigbee device in pairing mode
4. Device will appear in the list
5. Device automatically appears in Home Assistant!

### **Method 2: Via Home Assistant**

1. Go to **Settings** → **Devices & Services** → **MQTT**
2. Click **Configure** → **Add Device**
3. Put device in pairing mode
4. Device should appear

---

## 🔧 Troubleshooting

### **Zigbee2MQTT won't start?**

Check logs:
```bash
docker-compose logs zigbee2mqtt
```

Common issues:
- **USB device not found**: Check `/dev/ttyUSB0` path
- **Can't connect to MQTT**: Ensure Mosquitto is running
- **Permission denied**: Check USB device permissions

### **Devices not appearing in Home Assistant?**

1. Check Zigbee2MQTT web UI - are devices listed there?
2. Check MQTT integration in Home Assistant
3. Verify Mosquitto is running: `docker ps`
4. Check logs: `docker-compose logs homeassistant`

### **Can't access web UI on port 8080?**

- Verify container is running: `docker ps`
- Check if port is already in use
- Try: `http://localhost:8080` or `http://127.0.0.1:8080`

---

## 📝 Configuration File Location

Main config: `zigbee2mqtt/data/configuration.yaml`

You can edit this file to:
- Change MQTT settings
- Adjust serial port
- Enable/disable features
- Configure network settings

**After editing, restart Zigbee2MQTT:**
```bash
docker-compose restart zigbee2mqtt
```

---

## 🔄 Updating Zigbee2MQTT

To update to the latest version:
```bash
docker-compose pull zigbee2mqtt
docker-compose up -d zigbee2mqtt
```

---

## 📚 Useful Links

- **Zigbee2MQTT Documentation**: https://www.zigbee2mqtt.io/
- **Supported Devices**: https://www.zigbee2mqtt.io/supported-devices/
- **MQTT Topics**: Check Zigbee2MQTT web UI → Settings → MQTT

---

## ✅ Next Steps

1. ✅ Start services: `docker-compose up -d`
2. ✅ Access web UI: `http://localhost:8080`
3. ✅ Add MQTT integration in Home Assistant
4. ✅ Start adding Zigbee devices!

**Happy automating!** 🎉

