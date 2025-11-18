# Quick Start Guide for Home Assistant Users

## Step-by-Step Installation

### 1. Install ESPHome Addon (if not already installed)

- Open Home Assistant
- Go to **Settings** → **Add-ons** → **Add-on Store**
- Search for **"ESPHome"**
- Click **"INSTALL"** and wait for installation
- Click **"START"** and then **"OPEN WEB UI"**

### 2. Add Your Device Configuration

**Option A: Import from GitHub (Recommended - Modular)**

1. In ESPHome Web UI, click the **"+"** button
2. Enter a name (e.g., `bytelink-usbaio`)
3. Click **"EDIT"**
4. Delete all default content
5. Paste this:
   ```yaml
   packages:
     github: github://bytelink-ai/bytelink-aio-usb-sensor/bytelink-usbaio-github.yaml@main
   ```
   This pulls all modules from GitHub and allows automatic updates.

**Option B: Single-File Configuration**

1. In ESPHome Web UI, click the **"+"** button
2. Enter a name (e.g., `bytelink-usbaio`)
3. Click **"EDIT"**
4. Delete all default content
5. Paste this:
   ```yaml
   packages:
     github: github://bytelink-ai/bytelink-aio-usb-sensor/bytelink-usbaio.yaml@main
   ```
   This uses a single monolithic file.

### 3. Configure WiFi Secrets

1. In ESPHome Web UI, click the **"Settings"** icon (gear) in the top right
2. Click **"Secrets"**
3. Add your WiFi credentials:
   ```yaml
   wifi_ssid: "YourWiFiSSID"
   wifi_password: "YourWiFiPassword"
   ```
4. Click **"SAVE"**

### 4. Flash the Device

1. Connect your Bytelink USB Sensor to your computer via USB
2. In ESPHome, click **"INSTALL"**
3. Select **"Plug into the computer running ESPHome"**
4. Select your USB port from the dropdown
5. Click **"INSTALL"** and wait for the process to complete

### 5. Auto-Discovery in Home Assistant

Once the device is flashed and connected to WiFi:

1. The device will automatically appear in Home Assistant via mDNS
2. Go to **Settings** → **Devices & Services**
3. Look for **"ESPHome"** integration
4. Your device should appear automatically
5. Click **"CONFIGURE"** if needed

**If the device doesn't appear automatically:**

1. Go to **Settings** → **Devices & Services** → **ESPHome**
2. Click **"ADD INTEGRATION"** or **"CONFIGURE"**
3. Select **"Enter Manually"**
4. Enter the device name (e.g., `bytelink-usbaio-aabbccddeeff`) or IP address
5. Click **"SUBMIT"**

## Multiple Devices

Each device automatically gets a unique name based on its MAC address:
- First device: `bytelink-usbaio-aabbccddeeff`
- Second device: `bytelink-usbaio-112233445566`
- And so on...

You can install multiple devices using the same configuration - ESPHome will automatically handle the naming.

## Updating the Device

### Method 1: OTA Update (Wireless)

1. In ESPHome Web UI, open your device
2. Click **"UPDATE"**
3. Select **"Wirelessly (OTA)"**
4. Click **"INSTALL"**

### Method 2: Update from GitHub (If using package)

If you set up the device using the GitHub package method:
1. In ESPHome Web UI, open your device
2. Click **"UPDATE"**
3. ESPHome will automatically pull the latest version from GitHub
4. Click **"INSTALL"**

## Troubleshooting

### Device not appearing in Home Assistant

1. Check that the device is connected to WiFi (check the access point `AiOHotspot` if needed)
2. Verify mDNS is working on your network
3. Try adding manually using the device IP address
4. Check ESPHome logs for connection issues

### WiFi Connection Issues

1. The device will create an access point if WiFi fails:
   - SSID: `AiOHotspot`
   - Password: `SmartHome2025`
2. Connect to this access point and configure WiFi via the captive portal
3. Or update the secrets in ESPHome and reflash

### Compilation Errors

1. Make sure all external components are accessible
2. Check that your ESPHome version supports all components
3. Review the error messages in ESPHome logs

## Support

For issues or questions, please refer to the main README.md or contact support.

