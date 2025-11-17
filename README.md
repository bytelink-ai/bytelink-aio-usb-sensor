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

### Method 1: ESPHome Dashboard (Recommended)

1. Open ESPHome Dashboard
2. Click **"+"** to add a new device
3. Select **"Install from repository"**
4. Enter the repository URL:
   ```
   https://github.com/YOUR_USERNAME/YOUR_REPO_NAME
   ```
5. Select `package.yaml` as the configuration file
6. ESPHome will automatically detect and install the package

### Method 2: Manual Installation

1. Clone or download this repository
2. Copy `secrets.yaml.example` to `secrets.yaml`
3. Edit `secrets.yaml` and add your WiFi credentials:
   ```yaml
   wifi_ssid: "YourWiFiSSID"
   wifi_password: "YourWiFiPassword"
   ```
4. In ESPHome Dashboard, click **"+"** and select **"Upload a YAML file"**
5. Select `package.yaml` from this repository

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

When you update this repository, your customers can easily update their devices:

1. In ESPHome Dashboard, select the device
2. Click **"UPDATE"**
3. ESPHome will automatically pull the latest version from GitHub
4. The device will be updated via OTA

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

