# Creating MQTT Users in Mosquitto

## 🔍 Current Status

**Current Configuration:** Anonymous connections are **ALLOWED** (no password required)

This means:
- ✅ No username/password needed to connect
- ⚠️ Less secure (anyone can connect)
- ✅ Good for initial setup and testing

---

## 🔐 Creating a User and Password

### **Step 1: Start Mosquitto Container**

```bash
docker-compose up -d mosquitto
```

### **Step 2: Create a User**

Run this command (replace `mqtt_user` with your desired username):

```bash
docker exec -it mosquitto mosquitto_passwd -c /mosquitto/config/passwd mqtt_user
```

**What this does:**
- `-c` = Create new password file (use `-b` to add to existing file)
- `/mosquitto/config/passwd` = Password file location
- `mqtt_user` = Your username

**You'll be prompted to enter a password twice.**

### **Step 3: Add More Users (Optional)**

To add additional users (without `-c` flag):

```bash
docker exec -it mosquitto mosquitto_passwd /mosquitto/config/passwd another_user
```

### **Step 4: Enable Password Authentication**

Edit `mosquitto/config/mosquitto.conf`:

1. Change:
   ```conf
   allow_anonymous true
   ```
   to:
   ```conf
   allow_anonymous false
   ```

2. Uncomment the password file line:
   ```conf
   password_file /mosquitto/config/passwd
   ```

### **Step 5: Restart Mosquitto**

```bash
docker-compose restart mosquitto
```

---

## 📋 Complete Example

### **Create User "homeassistant" with Password:**

```bash
# 1. Start Mosquitto
docker-compose up -d mosquitto

# 2. Create user
docker exec -it mosquitto mosquitto_passwd -c /mosquitto/config/passwd homeassistant
# Enter password when prompted (e.g., "MySecurePassword123")

# 3. Edit mosquitto/config/mosquitto.conf:
#    - Set allow_anonymous false
#    - Uncomment password_file /mosquitto/config/passwd

# 4. Restart
docker-compose restart mosquitto
```

### **Connect with Credentials:**

- **Username:** `homeassistant`
- **Password:** `MySecurePassword123` (or whatever you set)

---

## 🔧 Quick Commands Reference

### **Create First User:**
```bash
docker exec -it mosquitto mosquitto_passwd -c /mosquitto/config/passwd username
```

### **Add Another User:**
```bash
docker exec -it mosquitto mosquitto_passwd /mosquitto/config/passwd username2
```

### **Delete a User:**
```bash
docker exec -it mosquitto mosquitto_passwd -D /mosquitto/config/passwd username
```

### **List Users:**
```bash
docker exec -it mosquitto cat /mosquitto/config/passwd
```

### **Change Password:**
```bash
docker exec -it mosquitto mosquitto_passwd /mosquitto/config/passwd username
# Enter new password when prompted
```

---

## 🔒 Enable Password Authentication

After creating users, update `mosquitto/config/mosquitto.conf`:

```conf
# Security settings
allow_anonymous false  # Changed from true

# Security - password file
password_file /mosquitto/config/passwd  # Uncommented
```

Then restart:
```bash
docker-compose restart mosquitto
```

---

## 🔗 Connect Home Assistant with Credentials

1. Go to **Home Assistant** → **Settings** → **Devices & Services**
2. Click **Add Integration** → **MQTT**
3. Enter:
   - **Broker:** `mosquitto`
   - **Port:** `1883`
   - **Username:** `homeassistant` (or your username)
   - **Password:** `YourPassword`
4. Click **Submit**

---

## ⚠️ Default Credentials

**There are NO default credentials!**

- If `allow_anonymous true`: No username/password needed
- If `allow_anonymous false`: You must create users (no defaults)

**Security Note:** Always create your own users with strong passwords!

---

## 🆘 Troubleshooting

### **"Permission denied" when creating password file?**

The password file is created inside the container. Make sure:
- Mosquitto container is running
- You're using `docker exec` command
- Volume mount is correct in docker-compose.yml

### **Can't connect after enabling password?**

1. Check password file exists:
   ```bash
   docker exec -it mosquitto ls -l /mosquitto/config/passwd
   ```

2. Verify configuration:
   ```bash
   docker exec -it mosquitto cat /mosquitto/config/mosquitto.conf | grep -E "allow_anonymous|password_file"
   ```

3. Check logs:
   ```bash
   docker-compose logs mosquitto
   ```

### **Forgot password?**

Delete the user and recreate:
```bash
docker exec -it mosquitto mosquitto_passwd -D /mosquitto/config/passwd username
docker exec -it mosquitto mosquitto_passwd /mosquitto/config/passwd username
```

---

## 📝 Summary

**Current State:**
- ✅ Anonymous connections allowed
- ❌ No default username/password
- ⚠️ Less secure (for testing)

**To Enable Security:**
1. Create user: `docker exec -it mosquitto mosquitto_passwd -c /mosquitto/config/passwd username`
2. Set `allow_anonymous false` in config
3. Uncomment `password_file` line
4. Restart: `docker-compose restart mosquitto`

**Recommended Username Examples:**
- `homeassistant`
- `mqtt_user`
- `zigbee2mqtt`
- Your name or custom username

