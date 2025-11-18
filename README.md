# Bytelink All-in-One USB Sensor

A comprehensive ESPHome-based sensor package for the Bytelink All-in-One USB Sensor device. This package includes environmental monitoring (temperature, humidity, CO2, VOC, IAQ), presence detection via mmWave radar, and Zigbee coordination capabilities.

## Features

- **Environmental Sensors:**
  - BME688: Temperature, Humidity, Pressure, eCO2, VOC, IAQ
  - SCD40: CO2 concentration with pressure compensation
  - BH1750: Illuminance sensor
  - AGS10: TVOC sensor

- **Presence Detection:**
  - LD2412 mmWave radar sensor
  - Moving and still target detection
  - Configurable distance gates (0-13)
  - Breathing detection capability

- **Connectivity:**
  - WiFi with Access Point fallback
  - Bluetooth Proxy support
  - Zigbee coordination (CC2652RB)
  - OTA updates
  - Web server interface

## Installation

### For Home Assistant Users (Recommended)

#### Initial Setup via ESPHome Addon

1. **Install ESPHome Addon** (if not already installed):
   - Go to **Settings** → **Add-ons** → **Add-on Store**
   - Search for "ESPHome" and install it
   - Start the addon and open the Web UI

2. **Add Your Device**:
   - In the ESPHome Web UI, click the **"+"** (plus) button
   - Select **"Continue"** to create a new device
   - Choose **"Skip"** when asked to create a new device (we'll import instead)
   - Click **"EDIT"** on the new device
   - Delete the default content and paste the contents of `bytelink-usbaio.yaml` from this repository
   - Or click **"IMPORT"** and paste the raw GitHub URL:
     ```
     https://raw.githubusercontent.com/bytelink-ai/bytelink-aio-usb-sensor/main/bytelink-usbaio.yaml
     ```

3. **Configure WiFi**:
   - In the ESPHome addon, go to **Settings** → **Secrets**
   - Add your WiFi credentials:
     ```yaml
     wifi_ssid: "YourWiFiSSID"
     wifi_password: "YourWiFiPassword"
     ```

4. **Flash the Device**:
   - Connect your device via USB
   - In ESPHome, click **"INSTALL"** → **"Plug into the computer running ESPHome"**
   - Select your USB port and click **"INSTALL"**
   - Wait for the installation to complete

5. **Auto-Discovery in Home Assistant**:
   - Once flashed and connected to WiFi, the device will automatically appear in Home Assistant
   - Go to **Settings** → **Devices & Services** → **ESPHome**
   - The device should appear automatically via mDNS discovery
   - If it doesn't appear automatically, click **"CONFIGURE"** → **"Enter Manually"** and enter the device IP or hostname

#### Alternative: Using Package Structure (For Updates)

For easier updates, you can use the modular package structure:

1. Download or clone this repository to your Home Assistant ESPHome config directory
2. Copy `secrets.yaml.example` to `secrets.yaml` in the ESPHome config directory
3. Add your WiFi credentials to `secrets.yaml`
4. In ESPHome Web UI, create a new device and use:
   ```yaml
   packages:
     github: github://bytelink-ai/bytelink-aio-usb-sensor/package.yaml@main
   ```

### For Standalone ESPHome Dashboard Users

1. Open ESPHome Dashboard
2. Click **"+"** to add a new device
3. Select **"Upload a YAML file"** or **"Install from repository"** (if available)
4. Use `bytelink-usbaio.yaml` for single-file setup, or `package.yaml` for modular structure

## Configuration

### WiFi Setup

The device uses secrets for WiFi configuration. Create a `secrets.yaml` file in your ESPHome configuration directory with:

```yaml
wifi_ssid: "YourWiFiSSID"
wifi_password: "YourWiFiPassword"
```

If WiFi connection fails, the device will create an access point:
- SSID: `AiOHotspot`
- Password: `SmartHome2025`

### Multiple Devices

Each device automatically uses its MAC address as a suffix for unique naming. For example:
- `bytelink-usbaio-aabbccddeeff`
- `bytelink-usbaio-112233445566`

This allows you to install multiple devices without naming conflicts.

## Customization

The configuration is modular and split into separate files:

- `package.yaml` - Main entry point
- `base.yaml` - Core ESP32, WiFi, and hardware configuration
- `sensors.yaml` - All sensor definitions
- `binary_sensors.yaml` - Binary sensor definitions
- `switches.yaml` - Switch and control definitions
- `text_sensors.yaml` - Text sensor definitions
- `numbers.yaml` - Number entity definitions
- `buttons.yaml` - Button definitions
- `scripts.yaml` - Automation scripts
- `external_components.yaml` - External component dependencies

You can modify any of these files to customize the device behavior. After making changes, compile and upload the firmware via ESPHome.

## Updates

### For Home Assistant Users

When you update this repository, your customers can easily update their devices:

**Method 1: Automatic Update (Recommended)**
1. In Home Assistant, go to **Settings** → **Devices & Services** → **ESPHome**
2. Select your device
3. Click **"UPDATE"** (if using package structure with GitHub source)
4. The device will be updated via OTA

**Method 2: Manual Update**
1. In ESPHome Web UI, open your device configuration
2. Click **"UPDATE"** → **"UPDATE"** (downloads latest from GitHub if using package)
3. Or manually copy the latest `bytelink-usbaio.yaml` content and click **"SAVE"** → **"INSTALL"** → **"Wirelessly (OTA)"**

**Method 3: Using Package with GitHub Source**
If you set up the device using the package structure with GitHub source:
```yaml
packages:
  github: github://YOUR_USERNAME/YOUR_REPO_NAME/package.yaml@main
```
Updates will automatically pull from GitHub when you click **"UPDATE"**.

## Hardware

- **MCU:** ESP32-C6
- **Zigbee:** CC2652RB
- **Sensors:**
  - BME688 (I2C: 0x76)
  - SCD40 (I2C: 0x62)
  - BH1750 (I2C)
  - AGS10 (I2C: 0x1A)
  - LD2412 (UART)

## Pin Configuration

- **I2C:** SDA=GPIO0, SCL=GPIO1
- **Zigbee UART:** RX=GPIO2, TX=GPIO3 (460800 baud)
- **Presence UART:** RX=GPIO16, TX=GPIO17 (115200 baud)
- **Zigbee Reset:** GPIO7
- **Zigbee Flash Mode:** GPIO14

## License

[Add your license here]

## Support

For support, please [add your support contact information]

