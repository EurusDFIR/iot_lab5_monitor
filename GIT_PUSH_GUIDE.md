# 📤 Hướng dẫn Push lên GitHub

## ✅ ĐÃ PUSH THÀNH CÔNG!

Repository: **https://github.com/EurusDFIR/iot_lab5_monitor**

---

## 🚀 Hướng dẫn cho người khác clone và chạy

### Clone repository

```bash
git clone https://github.com/EurusDFIR/iot_lab5_monitor.git
cd iot_lab5_monitor
```

### Cài đặt Python dependencies

```bash
pip install paho-mqtt requests
```

### Khởi động MQTT Broker

```bash
docker run -d \
  --name mosquitto \
  -p 1883:1883 \
  -p 8083:8083 \
  -v $(pwd)/infra/mosquitto.conf:/mosquitto/config/mosquitto.conf \
  eclipse-mosquitto
```

### Chạy các thành phần

**ESP32-C3 Real Hardware (khuyên dùng):**

```bash
# 1. Mở Arduino IDE
# 2. Load file: firmware_esp32c3/esp32c3_iot_demo/esp32c3_iot_demo.ino
# 3. Cấu hình WiFi và MQTT broker IP trong code
# 4. Upload lên ESP32-C3
# Xem chi tiết: firmware_esp32c3/ARDUINO_SETUP.md
```

**ESP32 Simulator (nếu không có hardware):**

```bash
python simulators/esp32_simulator.py
```

**Web Dashboard:**

```bash
cd web/src
python -m http.server 3000
# Mở: http://localhost:3000
```

**Database Logger (Optional):**

```bash
cd database
python mqtt_logger.py

# Xem dữ liệu đã lưu:
python view_database.py all
```

**Temperature Alert (Optional - Discord):**

```bash
# 1. Tạo Discord webhook riêng
# 2. Sửa DISCORD_WEBHOOK_URL trong alerts/temperature_alert.py
cd alerts
python temperature_alert.py
```

**Flutter App (Optional):**

```bash
cd app_flutter
flutter pub get
flutter run
# Lưu ý: Emulator dùng IP 10.0.2.2, physical device dùng IP thật
```

---

## 🔧 Thông tin hệ thống

### Hardware ESP32-C3 Super Mini

```
- DHT11: GPIO 2 (Temperature & Humidity sensor)
- LED Built-in: GPIO 8 (Active-LOW - for testing)
- LED External: GPIO 21 (Active-HIGH - main LED)
- Motor IN1: GPIO 6
- Motor IN2: GPIO 7
- Motor ENA: GPIO 10 (PWM control)
```

### MQTT Broker Configuration

```
- TCP Port: 1883 (ESP32, Database, Alerts)
- WebSocket Port: 8083 (Web Dashboard)
- Host: localhost or your_computer_ip
```

### MQTT Topics

```
demo/room1/sensor/state    - {"temp": 30.0, "hum": 57.0, "rssi": -74}
demo/room1/device/state    - {"light": true, "fan": false}
demo/room1/device/cmd      - {"light": "toggle"} or {"fan": "on"}
demo/room1/sys/online      - {"status": "online", "uptime": 1234}
```

### Database Tables (SQLite)

- **sensor_data**: Temperature, humidity, RSSI logs
- **device_state**: LED and fan state history
- **device_online**: Connection status logs
- **commands**: Command history with timestamps

---

## 🎯 Tính năng hoàn chỉnh

✅ **ESP32-C3 Real Hardware** với DHT11, LED, L298N Motor  
✅ **Web Dashboard** real-time monitoring  
✅ **Flutter Mobile App** cho Android/iOS  
✅ **SQLite Database** logging và analytics  
✅ **Discord Temperature Alerts** (30°C threshold)  
✅ **Multi-network Support** (home/hotspot/TDMU)  
✅ **Comprehensive Documentation**  
✅ **Arduino IDE Compatible** firmware  
✅ **Python Simulator** cho development

---

## 📞 Liên hệ

**Tác giả:** Lê Văn Hoàng, Nguyễn Tuấn Việt, Diệp Đại Lê Hoài  
**Repository:** https://github.com/EurusDFIR/iot_lab5_monitor  
**Institution:** Thủ Dầu Một University (TDMU)  
**Email:** Liên hệ qua GitHub Issues
