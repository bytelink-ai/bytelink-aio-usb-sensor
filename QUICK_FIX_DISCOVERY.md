# Quick Fix: Device Not Showing in ESPHome

## Immediate Steps to Get Your Device Visible

### Method 1: Add Device Manually (Fastest)

1. **Find your device's IP address:**
   - Check your router's connected devices list
   - Look for device name starting with `bytelink-usbaio`
   - Note the IP address (e.g., `192.168.1.100`)

2. **In ESPHome Builder Addon:**
   - Click the **"+"** button
   - Enter device name: `bytelink-usbaio` (or use the name with MAC suffix if you know it)
   - Click **"EDIT"**
   - Paste this configuration:
     ```yaml
     packages:
       github: github://bytelink-ai/bytelink-aio-usb-sensor/bytelink-usbaio-github.yaml@main
     ```
   - Click **"SAVE"**

3. **Connect to device:**
   - Click **"INSTALL"** → **"Wirelessly (OTA)"**
   - Enter the IP address you found (e.g., `192.168.1.100`)
   - Or try: `bytelink-usbaio-XXXXXX.local` (replace XXXXXX with MAC suffix)
   - Click **"CONNECT"**

### Method 2: Check if Device is in Access Point Mode

If you see a WiFi network called `AiOHotspot`:

1. **Connect to the access point:**
   - SSID: `AiOHotspot`
   - Password: `SmartHome2025`

2. **Configure WiFi:**
   - A captive portal should open automatically
   - If not, open browser and go to: `http://192.168.4.1`
   - Enter your WiFi credentials
   - Device will connect to your WiFi

3. **After connection:**
   - Wait 30 seconds for device to connect
   - Device should now appear in ESPHome

### Method 3: Use Web Interface to Verify

1. **Find device IP from router**

2. **Open web interface:**
   - Go to: `http://[device-ip]` in your browser
   - You should see ESPHome web interface
   - If you see it, device is working - just needs to be added manually

3. **Add to ESPHome:**
   - Use Method 1 above with the IP address

### Method 4: Check Home Assistant Integration

1. **Go to Home Assistant:**
   - **Settings** → **Devices & Services**

2. **Check ESPHome integration:**
   - Look for **"ESPHome"** integration
   - If device appears here but not in ESPHome addon, that's normal
   - ESPHome addon and Home Assistant integration are separate

3. **Add device to Home Assistant:**
   - Click **"CONFIGURE"** on ESPHome integration
   - Click **"ADD INTEGRATION"**
   - Enter device name or IP address
   - Device will be added to Home Assistant

### Method 5: Re-flash via USB

If device isn't responding at all:

1. **Connect device via USB**

2. **In ESPHome:**
   - Open your device configuration
   - Click **"INSTALL"** → **"Plug into the computer running ESPHome"**
   - Select USB port
   - Click **"INSTALL"**

3. **After flashing:**
   - Device should connect to WiFi
   - Wait 1-2 minutes
   - Try discovery again

## Common Issues

### Issue: Device shows in router but not ESPHome
**Solution:** Add manually using IP address (Method 1)

### Issue: Device creates access point (AiOHotspot)
**Solution:** WiFi credentials wrong - configure via captive portal (Method 2)

### Issue: Device appears in Home Assistant but not ESPHome addon
**Solution:** This is normal - they're separate. Use Home Assistant integration or add manually to ESPHome.

### Issue: Can't find device IP
**Solution:** 
- Check router's connected devices
- Use network scanner app
- Look for device name: `bytelink-usbaio-XXXXXX`

## Still Not Working?

1. **Check ESPHome addon logs:**
   - Settings → Add-ons → ESPHome → Logs
   - Look for errors

2. **Verify WiFi secrets:**
   - Settings → Secrets in ESPHome addon
   - Make sure `wifi_ssid` and `wifi_password` are correct

3. **Check network:**
   - Make sure device and Home Assistant are on same network
   - Some routers have AP isolation - disable it

4. **Try serial monitor:**
   - Connect via USB
   - Use serial monitor to see device status
   - Check for WiFi connection errors

