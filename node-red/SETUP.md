# Node-RED Setup Guide

## ✅ Node-RED Enabled!

Node-RED is now configured and ready to use in your Home Assistant setup.

---

## 🚀 First Time Setup

### 1. **Start Node-RED**

```bash
docker-compose up -d nodered
```

Or start all services:
```bash
docker-compose up -d
```

### 2. **Access Node-RED Web UI**

Open your browser and go to:
```
http://localhost:1880
```

You'll see the Node-RED editor interface.

### 3. **Install Home Assistant Nodes**

1. Click the **menu icon** (☰) in the top right
2. Select **Manage palette**
3. Go to the **Install** tab
4. Search for: `node-red-contrib-home-assistant-websocket`
5. Click **Install**

This package allows Node-RED to communicate with Home Assistant.

---

## 🔗 Connect Node-RED to Home Assistant

### **Method 1: Via Home Assistant Integration** (Recommended)

1. Go to **Home Assistant** → **Settings** → **Devices & Services**
2. Click **Add Integration**
3. Search for **Node-RED**
4. Click **Configure**
5. Enter:
   - **WebSocket URL**: `ws://nodered:1880` (container name)
   - Or use: `ws://localhost:1880` if accessing from host
6. Click **Submit**

Node-RED will now appear in Home Assistant!

### **Method 2: Manual Configuration in Node-RED**

1. In Node-RED, add a **Home Assistant** node
2. Double-click the node to configure
3. Click the **pencil icon** next to Server
4. Add new server:
   - **Name**: Home Assistant
   - **Base URL**: `http://homeassistant:8123` (container name)
   - **Access Token**: Get from Home Assistant → Profile → Long-Lived Access Tokens
5. Click **Add** and **Deploy**

---

## 📝 Create Your First Flow

### **Simple Example: Turn on Light When Motion Detected**

1. Drag these nodes onto the canvas:
   - **Home Assistant Events** node (trigger)
   - **Switch** node (filter)
   - **Home Assistant Call Service** node (action)

2. Connect them:
   ```
   [Events] → [Switch] → [Call Service]
   ```

3. Configure:
   - **Events node**: Event type = `state_changed`
   - **Switch node**: Check if `entity_id` contains `motion` and `state` is `on`
   - **Call Service node**: Service = `light.turn_on`, Entity = `light.living_room`

4. Click **Deploy** (top right)

5. Test it!

---

## 🎯 Common Use Cases

### **1. Complex Automation Logic**
- Multiple conditions
- Time-based triggers
- State checks
- Loops and delays

### **2. External API Integration**
- Weather data
- Stock prices
- News feeds
- Custom webhooks

### **3. Data Processing**
- Transform data formats
- Calculate averages
- Filter and aggregate
- Store in databases

### **4. Custom Dashboards**
- Create control panels
- Visual displays
- Interactive buttons
- Real-time monitoring

---

## 📚 Useful Node-RED Nodes

### **Essential Nodes:**
- `node-red-contrib-home-assistant-websocket` - Home Assistant integration
- `node-red-dashboard` - Create web dashboards
- `node-red-contrib-mqtt-broker` - MQTT integration (you have Mosquitto!)

### **Popular Nodes:**
- `node-red-contrib-time-range-switch` - Time-based logic
- `node-red-contrib-moment` - Date/time handling
- `node-red-contrib-http-request` - HTTP requests
- `node-red-contrib-stoptimer` - Timers and delays

### **Install Nodes:**
1. Menu → Manage palette → Install
2. Search for node name
3. Click Install

---

## 🔧 Configuration

### **Node-RED Data Location:**
- Config files: `./node-red/data/`
- Flows: Stored in `flows.json`
- Settings: `settings.js`

### **Backup Your Flows:**
Your flows are automatically saved in `node-red/data/flows.json`

To backup:
```bash
cp node-red/data/flows.json node-red/data/flows.json.backup
```

---

## 🆘 Troubleshooting

### **Node-RED won't start?**
```bash
docker-compose logs nodered
```

### **Can't access web UI?**
- Check if port 1880 is available
- Verify container is running: `docker ps`
- Try: `http://127.0.0.1:1880`

### **Home Assistant nodes not working?**
- Verify Home Assistant integration is configured
- Check access token is valid
- Ensure both containers are on the same network

### **Flows not saving?**
- Check `node-red/data/` directory permissions
- Verify volume mount is correct

---

## 📖 Learning Resources

- **Official Docs**: https://nodered.org/docs/
- **Home Assistant Node**: https://github.com/zachowj/node-red-contrib-home-assistant-websocket
- **Node-RED Dashboard**: https://github.com/node-red/node-red-dashboard
- **Examples**: https://flows.nodered.org/

---

## ✅ Next Steps

1. ✅ Access Node-RED: `http://localhost:1880`
2. ✅ Install Home Assistant nodes
3. ✅ Connect to Home Assistant
4. ✅ Create your first flow
5. ✅ Explore and automate! 🎉

**Happy automating!** 🚀

