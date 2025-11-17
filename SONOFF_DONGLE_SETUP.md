# Sonoff Multi-Protocol Dongle Setup Guide

## 🔍 Understanding Your Sonoff Dongle

Your Sonoff dongle (likely Zigbee 3.0 USB Dongle Plus) supports **both Zigbee and Thread** protocols. However, there are important limitations:

### **Key Points:**
1. ✅ **Both services CAN access the same USB device** (configured in docker-compose.yml)
2. ⚠️ **Typically can't use both protocols simultaneously** (unless special firmware)
3. 🔄 **May need to switch firmware** depending on which protocol you want to use

---

## 🏗️ Current Configuration

Your `docker-compose.yml` is now configured so **both services can access the dongle**:

```yaml
homeassistant:
  devices:
    - /dev/ttyUSB0:/dev/ttyUSB0  # Sonoff dongle

zigbee2mqtt:
  devices:
    - /dev/ttyUSB0:/dev/ttyUSB0  # Same dongle
```

**Both containers have access, but only one can actively use it at a time.**

---

## 📡 Protocol Usage Options

### **Option 1: Use for Zigbee Only** (Current Setup)
- Zigbee2MQTT uses the dongle for Zigbee
- Home Assistant Matter integration not using the dongle
- **Works perfectly** ✅

### **Option 2: Use for Thread/Matter Only**
- Stop Zigbee2MQTT
- Use Home Assistant Matter integration with Thread
- Flash dongle with Thread firmware (if needed)
- **Switch between protocols** 🔄

### **Option 3: Use Both (Advanced)**
- Requires special firmware that supports both protocols simultaneously
- Or use protocol switching
- **Complex setup** ⚠️

---

## 🔧 How to Use for Both Protocols

### **Method 1: Protocol Switching** (Recommended)

You can switch between Zigbee and Thread by:

1. **For Zigbee:**
   - Keep Zigbee2MQTT running
   - Home Assistant Matter integration disabled or not using dongle
   - Dongle in Zigbee mode

2. **For Thread:**
   - Stop Zigbee2MQTT: `docker-compose stop zigbee2mqtt`
   - Enable Matter integration in Home Assistant
   - Configure Thread border router
   - Dongle in Thread mode

3. **Switch back:**
   - Stop Matter Thread usage
   - Start Zigbee2MQTT: `docker-compose start zigbee2mqtt`

### **Method 2: Firmware Configuration**

Some Sonoff dongles support dual-mode firmware:

1. **Check your dongle model:**
   - Sonoff Zigbee 3.0 USB Dongle Plus (E variant)
   - May support OpenThread Border Router firmware

2. **Flash appropriate firmware:**
   - Zigbee firmware for Zigbee2MQTT
   - OpenThread firmware for Matter/Thread
   - Or dual-mode firmware (if available)

3. **Configure in each service:**
   - Zigbee2MQTT: Uses Zigbee protocol
   - Home Assistant Matter: Uses Thread protocol

---

## 🎯 Recommended Setup

### **For Most Users:**

**Use the dongle for Zigbee** (current setup):
- ✅ Zigbee2MQTT handles all Zigbee devices
- ✅ Works great with your current configuration
- ✅ For Matter devices, use Wi-Fi Matter or standalone Thread border router

**Why?**
- Simpler setup
- No protocol switching needed
- Better reliability
- Both protocols can work simultaneously (Zigbee via dongle, Matter via Wi-Fi/standalone router)

### **If You Need Thread Support:**

**Option A: Use standalone Thread border router** (easiest)
- HomePod Mini, Echo Dot, etc.
- No dongle configuration needed
- Works alongside Zigbee

**Option B: Switch protocols** (advanced)
- Use dongle for Zigbee most of the time
- Switch to Thread when needed
- Requires stopping/starting services

---

## 🔄 Switching Between Protocols

### **Switch from Zigbee to Thread:**

1. **Stop Zigbee2MQTT:**
   ```bash
   docker-compose stop zigbee2mqtt
   ```

2. **Enable Matter integration in Home Assistant:**
   - Settings → Devices & Services → Add Integration → Matter
   - Configure Thread border router
   - Select your Sonoff dongle

3. **Use Thread devices**

### **Switch back to Zigbee:**

1. **Disable Thread in Home Assistant Matter settings**

2. **Start Zigbee2MQTT:**
   ```bash
   docker-compose start zigbee2mqtt
   ```

3. **Use Zigbee devices**

---

## 📋 Configuration Checklist

### **Current Setup (Zigbee):**
- ✅ Zigbee2MQTT has USB access
- ✅ Home Assistant has USB access (for future Thread)
- ✅ Both services configured
- ✅ Zigbee2MQTT using dongle for Zigbee

### **To Use Thread:**
1. ✅ USB access already configured
2. ⚠️ Stop Zigbee2MQTT (or use standalone Thread router)
3. ⚠️ Enable Matter integration in Home Assistant
4. ⚠️ Configure Thread border router
5. ⚠️ Flash Thread firmware if needed

---

## 🛠️ Troubleshooting

### **"Device busy" or "Permission denied" errors:**

This means both services are trying to use the dongle simultaneously:

**Solution:**
- Stop one service before using the other
- Or use standalone Thread router instead

### **Thread not working:**

1. **Check firmware:**
   - Sonoff dongle may need Thread firmware
   - Check Sonoff documentation for your model

2. **Verify USB access:**
   ```bash
   docker exec -it homeassistant ls -l /dev/ttyUSB0
   ```

3. **Check Matter integration:**
   - Settings → Devices & Services → Matter
   - Verify Thread border router configuration

---

## 💡 Best Practice Recommendation

**For your setup, I recommend:**

1. **Keep using dongle for Zigbee** (current setup) ✅
2. **For Matter devices:**
   - Use **Wi-Fi Matter devices** (no dongle needed)
   - OR use **standalone Thread border router** (HomePod, Echo, etc.)
3. **This way:**
   - ✅ Zigbee works via dongle
   - ✅ Matter works via Wi-Fi/standalone router
   - ✅ Both protocols work simultaneously
   - ✅ No protocol switching needed
   - ✅ Simpler and more reliable

---

## 📚 Additional Resources

- **Sonoff Dongle Documentation**: Check Sonoff website for your specific model
- **Zigbee2MQTT**: https://www.zigbee2mqtt.io/
- **Home Assistant Matter**: https://www.home-assistant.io/integrations/matter/
- **OpenThread**: https://openthread.io/

---

## ✅ Summary

**Can both services access the USB dongle?**
✅ **YES** - Both are configured to access `/dev/ttyUSB0`

**Can they use it simultaneously?**
⚠️ **Typically NO** - Only one protocol at a time (unless special firmware)

**Recommended approach:**
- Use dongle for Zigbee (current setup)
- Use Wi-Fi Matter or standalone Thread router for Matter
- Both protocols work together without conflicts! 🎉

