# Home Assistant Configuration Directory

## 📁 What is this folder?

This is the **main configuration directory** for Home Assistant. It stores all your Home Assistant settings, automations, devices, and data.

## ✅ Already Configured!

Your `docker-compose.yml` already mounts this folder:
```yaml
volumes:
  - ./config:/config
```

## 🚀 First Run

**You don't need to create this folder manually!**

Home Assistant will automatically create it when you first start:
```bash
docker-compose up -d homeassistant
```

It will automatically generate:
- `configuration.yaml` - Main config file
- `secrets.yaml` - Sensitive data (API keys, passwords)
- `automations.yaml` - Your automations
- `scripts.yaml` - Scripts
- `.storage/` - Internal data (devices, integrations, etc.)
- `www/` - Custom files (images, icons, etc.)
- And more...

## 📋 What's Stored Here?

### **Configuration Files:**
- `configuration.yaml` - Main configuration
- `automations.yaml` - Automations
- `scripts.yaml` - Scripts
- `scenes.yaml` - Scenes
- `secrets.yaml` - API keys, passwords
- `blueprints/` - Blueprint automations

### **Data:**
- `.storage/` - Device registry, integration data, etc.
- `home-assistant_v2.db` - SQLite database (if using default recorder)
- `custom_components/` - Custom integrations
- `custom_panels/` - Custom UI panels
- `www/` - Custom static files

### **Logs:**
- `home-assistant.log` - Log files

## 🔧 Manual Configuration (Optional)

If you want to pre-configure Home Assistant before first run, you can create:

### **Basic `configuration.yaml`:**
```yaml
# Basic Home Assistant configuration
default_config:

# Enable integrations
homeassistant:
  name: Home
  latitude: 40.4168
  longitude: -3.7038
  elevation: 0
  unit_system: metric
  time_zone: Europe/Madrid
  country: ES
```

But **it's not required** - Home Assistant will create a default one!

## 💡 Important Notes

1. **Backup this folder regularly!** It contains all your configuration.

2. **Permissions:** Make sure Docker can read/write to this folder.

3. **Don't delete** - Contains all your Home Assistant data!

4. **Sync across devices:** This folder can be synced to backup all settings.

## 🔄 Backup

To backup your Home Assistant configuration:
```bash
# Copy entire config folder
cp -r config/ config_backup/
```

Or use Home Assistant's built-in backup feature in the UI.

## ✅ Summary

- ✅ **Already configured** in docker-compose.yml
- ✅ **Created automatically** on first run
- ✅ **No manual setup needed**
- ⚠️ **Backup regularly!**

Just run `docker-compose up -d homeassistant` and Home Assistant will set everything up automatically!

