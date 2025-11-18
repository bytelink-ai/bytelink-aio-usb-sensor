# Commercial Distribution & Update Guide

## Main File for Commercial Use

**`bytelink-usbaio-github.yaml`** is the primary file for commercial distribution.

This file references all modules from your GitHub repository, allowing you to:
- ✅ Update individual modules (sensors, switches, etc.) independently
- ✅ Customers automatically pull module updates from GitHub
- ✅ Maintain modular code structure for easier maintenance
- ✅ Update specific components without touching the entire config

## Customer Installation (One-Time Setup)

Have your customers install using the GitHub package method:

### In ESPHome (Home Assistant Addon):

1. Customer creates a new device in ESPHome
2. Customer pastes this into the device configuration:
   ```yaml
   packages:
     github: github://bytelink-ai/bytelink-aio-usb-sensor/bytelink-usbaio-github.yaml@main
   ```
3. Customer adds WiFi secrets and flashes the device
4. Device is set up and ready

**That's it!** The device will now pull all modules from your GitHub repository and can be updated automatically.

## How to Update Customer Devices

### Option 1: Update Individual Modules (Recommended)

You can update specific modules without touching others:

**Example: Update sensor configuration**
```bash
# Edit sensors.yaml with your changes
git add sensors.yaml
git commit -m "Update sensor configuration - improved calibration"
git push origin main
```

**Example: Update base configuration**
```bash
# Edit base.yaml (WiFi, hardware settings, etc.)
git add base.yaml
git commit -m "Update base config - new WiFi settings"
git push origin main
```

**Example: Update version number**
```bash
# Edit bytelink-usbaio-github.yaml
# Update version: "1.0.0" → "1.0.1"
git add bytelink-usbaio-github.yaml
git commit -m "Bump version to 1.0.1"
git push origin main
```

### Option 2: Update Main File

If you need to change the main configuration (name, version, etc.):

1. Edit `bytelink-usbaio-github.yaml`
2. Update version number:
   ```yaml
   project:
     name: bytelink.aios_room_sensorHV
     version: "1.0.1"  # ← Increment this
   ```
3. Commit and push:
   ```bash
   git add bytelink-usbaio-github.yaml
   git commit -m "Update firmware v1.0.1 - [describe your changes]"
   git push origin main
   ```

### Step 4: Customers Update Their Devices

Customers update via ESPHome:
1. Open ESPHome Web UI
2. Select their device
3. Click **"UPDATE"**
4. ESPHome automatically pulls the latest version from GitHub
5. Click **"INSTALL"** → **"Wirelessly (OTA)"**
6. Device updates without physical access

## Module Files Structure

The main file (`bytelink-usbaio-github.yaml`) references these modules from GitHub:

- `base.yaml` - Core ESP32, WiFi, hardware configuration
- `sensors.yaml` - All sensor definitions
- `binary_sensors.yaml` - Binary sensor definitions  
- `switches.yaml` - Switch and control definitions
- `text_sensors.yaml` - Text sensor definitions
- `numbers.yaml` - Number entity definitions
- `buttons.yaml` - Button definitions
- `scripts.yaml` - Automation scripts
- `external_components.yaml` - External component dependencies

**Update any of these files independently**, and customers can pull the updates automatically.

## Alternative: Single-File Configuration

If you prefer a single monolithic file for simpler updates, use `bytelink-usbaio.yaml`:

### Customer Installation:
```yaml
packages:
  github: github://bytelink-ai/bytelink-aio-usb-sensor/bytelink-usbaio.yaml@main
```

**Note:** The modular approach (`bytelink-usbaio-github.yaml`) is recommended for commercial use as it allows updating individual components without affecting the entire configuration.

## Version Management Best Practices

1. **Use Semantic Versioning:**
   - `1.0.0` - Initial release
   - `1.0.1` - Bug fixes
   - `1.1.0` - New features
   - `2.0.0` - Breaking changes

2. **Create Release Tags (Optional):**
   ```bash
   git tag -a v1.0.1 -m "Release version 1.0.1"
   git push origin v1.0.1
   ```
   Customers can then pin to specific versions:
   ```yaml
   packages:
     github: github://bytelink-ai/bytelink-aio-usb-sensor/bytelink-usbaio.yaml@v1.0.1
   ```

3. **Update Changelog:**
   Create a `CHANGELOG.md` to document updates for customers.

## Customer Communication

When you release an update, notify customers:
- "New firmware update available (v1.0.1)"
- "Update via ESPHome: Click UPDATE on your device"
- Include changelog of what's new/fixed

## Summary

**For Commercial Use:**
- **Main file:** `bytelink-usbaio-github.yaml` (references modules from GitHub)
- **Customer setup:** Use GitHub package reference to main file
- **Your updates:** 
  - Update individual module files (e.g., `sensors.yaml`, `base.yaml`) → Commit → Push
  - Or update main file for version/name changes
- **Customer updates:** Click UPDATE in ESPHome → OTA install → Pulls latest from GitHub

**Benefits:**
- ✅ Update individual components independently
- ✅ Customers automatically get module updates
- ✅ Maintain clean modular code structure
- ✅ Easy to maintain and version control

This gives you full control over customer device updates while keeping the process simple for end users.

