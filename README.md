# ESPHome Plant Monitoring System

> **NOTE:**  These setup instructions are based on macOS. Commands may differ for other operating systems.

This ESPHome configuration runs on an ESP32 (M5Stack Atom) to monitor soil moisture, temperature, light, and conductivity using Xiaomi Mi Flora sensors. It provides real-time updates via Slack notifications and includes a web server for remote access.

# Features
- Soil monitoring: Tracks moisture, temperature, light, and conductivity for multiple plants.
- Automated alerts: Sends Slack notifications when a plant needs watering or when conditions improve.
- Scheduled reports: Posts a summary of sensor readings every Monday and Thursday at 10 AM.
- Button-triggered updates: A physical button press sends an instant plant status report.
- Status LED feedback: Indicates successful or failed Slack message delivery.
 -Web server access: View real-time sensor data through a simple web interface.

# Hardware
- ESP32 (M5Stack Atom)
- Xiaomi Mi Flora Sensors
- Wi-Fi Connectivity with fallback AP mode

This project is designed to automate plant care by providing timely insights into soil conditions and reducing manual watering guesswork.

# How to Set Up
1. Find the Serial Port
Identify the ESP32’s serial port by running:
```
ls /dev/cu.*
```
Example output:
```
/dev/cu.Bluetooth-Incoming-Port /dev/cu.debug-console           /dev/cu.usbserial-0000000000
```
2. Detect Sensor MAC Addresses
Each Xiaomi Mi Flora sensor has a unique MAC address. Detect them one by one using `address_detection.yaml`:
```
esphome run address_detection.yaml
```
3. Configure secrets.yaml
- Copy `secrets_template.yaml` to `secrets.yaml`.
- Fill in your Wi-Fi password, Slack webhook URL, and the MAC addresses of each sensor.

4. Compile and Upload the Configuration
Once everything is set, compile and upload the ESPHome configuration:
```
esphome run config.yaml
```
5. Monitor the Web Interface
You can monitor the metrics using a webserver. It can be accessed by `<name>.local`. In this very case it's `http://esp32-mi-flora-3rd-floor.local`. You need to be connected to the same wifi as the esp32 controller.

> **NOTE:**  The ESP32 must be plugged into your computer during flashing. After flashing, it can run independently when connected to a power source.

# TODO:
- [ ] Debug notification frequency to avoid excessive messages.
- [ ] Compare memory efficiency between ESPHome and MicroPython.
- [ ] Scale the system to cover all office floors.
- [ ] Encapsulate IoT Wi-Fi connectivity by setting up a dedicated SSID or VLAN for ESP32 devices to improve security and stability.