# Commercial Distribution & Update Guide

## Main File for Commercial Use

**`bytelink-usbaio.yaml`** is the primary file for commercial distribution.

This single-file configuration allows you to:
- ✅ Easily update all customer devices from one file
- ✅ Push updates that customers can pull automatically
- ✅ Maintain version control with simple commits
- ✅ Provide simple installation for customers

## Customer Installation (One-Time Setup)

Have your customers install using the GitHub package method:

### In ESPHome (Home Assistant Addon):

1. Customer creates a new device in ESPHome
2. Customer pastes this into the device configuration:
   ```yaml
   packages:
     github: github://bytelink-ai/bytelink-aio-usb-sensor/bytelink-usbaio.yaml@main
   ```
3. Customer adds WiFi secrets and flashes the device
4. Device is set up and ready

**That's it!** The device will now pull updates from your GitHub repository.

## How to Update Customer Devices

### Step 1: Make Your Changes

Edit `bytelink-usbaio.yaml` with your updates:
- Fix bugs
- Add new features
- Update sensor configurations
- Change default settings

### Step 2: Update Version Number (Optional but Recommended)

In `bytelink-usbaio.yaml`, update the version:
```yaml
esphome:
  name: bytelink-usbaio
  friendly_name: usbaio
  name_add_mac_suffix: true
  project:
    name: bytelink.aios_room_sensorHV
    version: "1.0.1"  # ← Increment this (1.0.0 → 1.0.1 → 1.0.2, etc.)
```

### Step 3: Commit and Push

```bash
git add bytelink-usbaio.yaml
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

## Alternative: Using Modular Package Structure

If you prefer to maintain separate files for different components, you can use `package.yaml`:

### Customer Installation:
```yaml
packages:
  github: github://bytelink-ai/bytelink-aio-usb-sensor/package.yaml@main
```

### For Updates:
Update individual module files (e.g., `sensors.yaml`, `base.yaml`) and push. Customers pull updates the same way.

**Note:** The modular approach is better if you frequently update specific components, but requires customers to pull all files. The single-file approach is simpler for most commercial use cases.

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
- **Main file:** `bytelink-usbaio.yaml`
- **Customer setup:** Use GitHub package reference
- **Your updates:** Edit `bytelink-usbaio.yaml` → Commit → Push
- **Customer updates:** Click UPDATE in ESPHome → OTA install

This gives you full control over customer device updates while keeping the process simple for end users.

