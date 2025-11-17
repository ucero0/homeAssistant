# Fix Node-RED Permissions

## 🔧 Quick Fix

Run these commands in your project directory:

```bash
# Navigate to your project
cd /opt/homeAssistant

# Fix Node-RED data directory permissions
sudo chown -R 1000:1000 node-red/data
sudo chmod -R 755 node-red/data

# If the directory doesn't exist, create it first
mkdir -p node-red/data
sudo chown -R 1000:1000 node-red/data
```

## 🔄 Alternative: Use Your User ID

If you want to use your current user instead:

```bash
# Get your user ID
id -u
id -g

# Set permissions to your user (replace 1000 with your UID if different)
sudo chown -R $(id -u):$(id -g) node-red/data
```

## 🚀 After Fixing Permissions

1. **Restart Node-RED:**
   ```bash
   docker compose restart nodered
   ```

2. **Or restart all services:**
   ```bash
   docker compose down
   docker compose up -d
   ```

## ✅ Verify

Check if Node-RED is running:
```bash
docker compose ps nodered
docker compose logs nodered
```

You should see Node-RED starting without permission errors.

