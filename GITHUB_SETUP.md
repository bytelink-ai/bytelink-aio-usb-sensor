# GitHub Repository Setup Guide

## Step 1: Create GitHub Repository

1. Go to [GitHub](https://github.com) and sign in
2. Click the **"+"** icon in the top right corner
3. Select **"New repository"**
4. Fill in the repository details:
   - **Repository name:** `bytelink-aio-usb-sensor` (or your preferred name)
   - **Description:** "ESPHome package for Bytelink All-in-One USB Sensor"
   - **Visibility:** Choose Public (for easy customer access) or Private
   - **DO NOT** initialize with README, .gitignore, or license (we already have these)
5. Click **"Create repository"**

## Step 2: Connect Local Repository to GitHub

After creating the repository, GitHub will show you commands. Run these in your terminal:

```bash
cd "/Users/eren/Library/Mobile Documents/com~apple~CloudDocs/Sensors/USB Sensor Github"

# Add the remote (already set up for bytelink-ai/bytelink-aio-usb-sensor)
git remote add origin https://github.com/bytelink-ai/bytelink-aio-usb-sensor.git

# Rename branch to main (if needed)
git branch -M main

# Push to GitHub
git push -u origin main
```

## Step 3: Repository Already Set Up

Your repository is already configured at: `https://github.com/bytelink-ai/bytelink-aio-usb-sensor`

All documentation files have been updated with the correct repository URL.

## Step 4: Customer Installation

Your customers can now install the package in two ways:

### Option A: ESPHome Dashboard (Easiest)
1. Open ESPHome Dashboard
2. Click **"+"** to add new device
3. Select **"Install from repository"**
4. Enter: `https://github.com/bytelink-ai/bytelink-aio-usb-sensor`
5. Select `package.yaml`
6. ESPHome will automatically detect and install

### Option B: Manual Installation
1. Download or clone the repository
2. Copy `secrets.yaml.example` to `secrets.yaml`
3. Add WiFi credentials to `secrets.yaml`
4. Upload `package.yaml` via ESPHome Dashboard

## Updating the Package

When you make updates:

```bash
# Make your changes to the YAML files
# Then commit and push:
git add .
git commit -m "Description of your changes"
git push
```

Customers can update their devices by clicking **"UPDATE"** in ESPHome Dashboard, which will pull the latest version from GitHub.

## Version Management

To update the version number, edit `package.yaml`:
```yaml
project:
  name: bytelink.aios_room_sensorHV
  version: "1.0.1"  # Increment this for each release
```

Then commit and push the update.

