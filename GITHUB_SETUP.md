# GitHub Repository Setup Guide

## ✅ Git Repository Ready!

Your local git repository has been initialized and all files have been committed.

## 🚀 Next Steps: Create GitHub Repository

### **Option 1: Using GitHub Website** (Easiest)

1. **Go to GitHub:**
   - Visit: https://github.com/new
   - Or: GitHub → Click "+" → New repository

2. **Create Repository:**
   - **Repository name:** `home-assistant-docker-setup` (or your preferred name)
   - **Description:** `Complete Docker Compose setup for Home Assistant with Zigbee, MQTT, Node-RED, and automation tools`
   - **Visibility:** Public or Private (your choice)
   - **⚠️ DO NOT** initialize with README, .gitignore, or license (we already have these)
   - Click **Create repository**

3. **Push Your Code:**
   ```bash
   git remote add origin https://github.com/YOUR_USERNAME/home-assistant-docker-setup.git
   git branch -M main
   git push -u origin main
   ```

   Replace `YOUR_USERNAME` with your GitHub username.

### **Option 2: Using GitHub CLI** (If installed)

```bash
# Install GitHub CLI if not installed:
# Windows: winget install GitHub.cli
# Linux: sudo apt install gh
# macOS: brew install gh

# Login to GitHub
gh auth login

# Create repository and push
gh repo create home-assistant-docker-setup --public --source=. --remote=origin --push
```

### **Option 3: Using GitHub Desktop**

1. Install GitHub Desktop: https://desktop.github.com/
2. File → Add Local Repository
3. Select your `homeAssistant` folder
4. Publish repository to GitHub

## 📋 Quick Commands

After creating the GitHub repository, run these commands:

```bash
# Add remote (replace with your repository URL)
git remote add origin https://github.com/YOUR_USERNAME/home-assistant-docker-setup.git

# Rename branch to main (if needed)
git branch -M main

# Push to GitHub
git push -u origin main
```

## 🔐 Authentication

If you get authentication errors:

### **Using Personal Access Token:**
1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate new token with `repo` scope
3. Use token as password when pushing

### **Using SSH:**
```bash
# Generate SSH key (if you don't have one)
ssh-keygen -t ed25519 -C "your_email@example.com"

# Add to GitHub: Settings → SSH and GPG keys → New SSH key
# Copy public key: cat ~/.ssh/id_ed25519.pub

# Use SSH URL instead:
git remote set-url origin git@github.com:YOUR_USERNAME/home-assistant-docker-setup.git
```

## ✅ What's Included

Your repository includes:
- ✅ `docker-compose.yml` - Main configuration
- ✅ `README.md` - Project documentation
- ✅ `.gitignore` - Excludes sensitive data
- ✅ All documentation files
- ✅ Configuration templates
- ✅ Setup guides

## 🔒 Security Note

The `.gitignore` file excludes:
- `config/` data (Home Assistant database, secrets)
- `mosquitto/config/passwd` (MQTT passwords)
- `node-red/data/` (Node-RED flows)
- `zigbee2mqtt/data/` (Zigbee device data)
- `.env` files

**These sensitive files will NOT be uploaded to GitHub!** ✅

## 📝 Future Updates

To update the repository after making changes:

```bash
git add .
git commit -m "Description of changes"
git push
```

## 🆘 Troubleshooting

### **"Repository not found" error:**
- Check repository name and username are correct
- Verify you have access to the repository

### **"Authentication failed":**
- Use Personal Access Token instead of password
- Or set up SSH keys

### **"Permission denied":**
- Check you're logged into GitHub
- Verify repository permissions

---

**Your code is ready to push!** Just create the GitHub repository and follow the commands above. 🚀

