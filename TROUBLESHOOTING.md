# Troubleshooting Guide

## Device Not Appearing in ESPHome Builder Addon

If you've flashed the device but can't see it in ESPHome, try these steps:

### Step 1: Check Device Status

1. **Check if device is on WiFi:**
   - Look for WiFi network: `AiOHotspot` (if device is in AP mode)
   - If you see this network, the device didn't connect to your WiFi
   - Connect to `AiOHotspot` (password: `SmartHome2025`)
   - A captive portal should open - configure WiFi there

2. **Check device IP address:**
   - If device is on WiFi, find its IP address:
     - Check your router's connected devices list
     - Or use a network scanner app
   - The device name should be: `bytelink-usbaio-XXXXXX` (where XXXXXX is MAC address)

### Step 2: Add Device Manually in ESPHome

If auto-discovery doesn't work, add the device manually:

1. **In ESPHome Web UI:**
   - Click the **"+"** button to add a new device
   - Select **"Continue"** 
   - Enter the device name manually (e.g., `bytelink-usbaio`)
   - Click **"EDIT"**
   - Paste your configuration:
     ```yaml
     packages:
       github: github://bytelink-ai/bytelink-aio-usb-sensor/bytelink-usbaio-github.yaml@main
     ```
   - Click **"SAVE"**

2. **Connect to the device:**
   - Click **"INSTALL"** → **"Wirelessly (OTA)"**
   - Enter the device's IP address or hostname
   - Or use: `bytelink-usbaio-XXXXXX.local` (replace XXXXXX with MAC suffix)
   - Click **"CONNECT"**

### Step 3: Check Home Assistant ESPHome Integration

1. **Go to Home Assistant:**
   - **Settings** → **Devices & Services**
   - Look for **"ESPHome"** integration
   - If not there, click **"ADD INTEGRATION"** → Search for **"ESPHome"**

2. **Add device manually:**
   - Click **"CONFIGURE"** on ESPHome integration
   - Click **"ADD INTEGRATION"** or **"Enter Manually"**
   - Enter device name: `bytelink-usbaio-XXXXXX` or IP address
   - Click **"SUBMIT"**

### Step 4: Verify Network Connectivity

1. **Check if device is reachable:**
   ```bash
   # Try to ping the device (replace with your device IP)
   ping bytelink-usbaio-XXXXXX.local
   # Or
   ping [device-ip-address]
   ```

2. **Check web server:**
   - Open browser and go to: `http://[device-ip-address]` or `http://bytelink-usbaio-XXXXXX.local`
   - You should see the ESPHome web interface
   - If you see it, the device is working but ESPHome addon can't discover it

### Step 5: Check mDNS/Bonjour

mDNS might not be working on your network. Try:

1. **Install mDNS tools (if needed):**
   ```bash
   # On macOS/Linux
   brew install avahi  # macOS
   sudo apt-get install avahi-daemon  # Linux
   ```

2. **Test mDNS resolution:**
   ```bash
   # Try to resolve the device name
   ping bytelink-usbaio-XXXXXX.local
   ```

3. **If mDNS doesn't work:**
   - Use IP address instead of hostname
   - Or configure your router to enable mDNS/Bonjour

### Step 6: Check ESPHome Addon Logs

1. **In Home Assistant:**
   - Go to **Settings** → **Add-ons** → **ESPHome**
   - Click **"LOGS"** tab
   - Look for errors or connection attempts

2. **Check for errors:**
   - Look for "Failed to connect" messages
   - Check for mDNS discovery errors
   - Verify network connectivity errors

### Step 7: Re-flash with USB (If Needed)

If nothing works, re-flash via USB:

1. **In ESPHome Web UI:**
   - Open your device configuration
   - Click **"INSTALL"** → **"Plug into the computer running ESPHome"**
   - Connect device via USB
   - Select USB port
   - Click **"INSTALL"**

2. **After flashing:**
   - Device should connect to WiFi automatically
   - Wait 1-2 minutes for device to fully boot
   - Try discovery again

### Step 8: Verify Configuration

Make sure your configuration is correct:

1. **Check WiFi secrets:**
   - In ESPHome addon: **Settings** → **Secrets**
   - Verify `wifi_ssid` and `wifi_password` are correct
   - Make sure there are no typos

2. **Check device name:**
   - Device name should be: `bytelink-usbaio` (MAC suffix added automatically)
   - If you see it in router, note the full name with MAC suffix

### Step 9: Network Firewall/Security

Some networks block mDNS or device discovery:

1. **Check router settings:**
   - Enable mDNS/Bonjour
   - Disable AP isolation
   - Allow device-to-device communication

2. **Check firewall:**
   - Allow port 6053 (ESPHome API)
   - Allow port 80 (Web server)
   - Allow mDNS traffic (port 5353)

### Quick Fix: Use IP Address

The fastest solution is often to use the IP address directly:

1. Find device IP from router
2. In ESPHome, add device manually with IP address
3. Or in Home Assistant ESPHome integration, enter IP manually

## Still Not Working?

If none of these work:

1. **Check device serial output:**
   - Connect via USB
   - Use serial monitor to see device logs
   - Look for WiFi connection status
   - Check for error messages

2. **Verify hardware:**
   - Make sure device is powered properly
   - Check USB connection
   - Verify WiFi antenna is connected (if external)

3. **Contact Support:**
   - Provide device logs
   - Share network configuration details
   - Include ESPHome addon version

