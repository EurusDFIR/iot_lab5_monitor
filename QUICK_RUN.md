# 🚀 IoT Lab 5 Monitor - Quick Start

Hệ thống giám sát IoT hoàn chỉnh với ESP32-C3, Web Dashboard, Mobile App và Database.

## ⚡ 3 Bước để chạy ngay

### 1. Clone & Setup
```bash
git clone https://github.com/EurusDFIR/iot_lab5_monitor.git
cd iot_lab5_monitor
pip install paho-mqtt requests
```

### 2. Khởi động MQTT Broker
```bash
docker run -d --name mosquitto -p 1883:1883 -p 8083:8083 eclipse-mosquitto
```

### 3. Chạy các thành phần

**Terminal 1 - Web Dashboard:**
```bash
cd web/src
python -m http.server 3000
```
Mở: http://localhost:3000

**Terminal 2 - ESP32 Simulator (hoặc upload firmware lên hardware):**
```bash
python simulators/esp32_simulator.py
```

**Terminal 3 - Database Logger (tùy chọn):**
```bash
cd database
python mqtt_logger.py
```

**Terminal 4 - Temperature Alert (tùy chọn):**
```bash
cd alerts
# Sửa DISCORD_WEBHOOK_URL trong temperature_alert.py trước
python temperature_alert.py
```

**Terminal 5 - Flutter App (tùy chọn):**
```bash
cd app_flutter
flutter run
```

## 🔧 Cấu hình Hardware (ESP32-C3)

Nếu có ESP32-C3 hardware:

1. Mở `firmware_esp32c3/esp32c3_iot_demo/esp32c3_iot_demo.ino` trong Arduino IDE
2. Sửa WiFi credentials:
```cpp
const char *WIFI_SSID = "YOUR_WIFI_NAME";
const char *WIFI_PASSWORD = "YOUR_WIFI_PASS";
const char *MQTT_HOST = "YOUR_COMPUTER_IP";  // IP của máy tính chạy Mosquitto
```
3. Upload lên ESP32-C3

## 📊 Kiểm tra hoạt động

- **Web Dashboard:** http://localhost:3000 - hiển thị nhiệt độ, độ ẩm real-time
- **Database:** Chạy `python database/view_database.py all` để xem dữ liệu
- **MQTT Topics:** `demo/room1/sensor/state`, `demo/room1/device/state`

## 🛠️ Troubleshooting

### Không kết nối được?
- Kiểm tra Docker: `docker ps` (phải có mosquitto container)
- Kiểm tra IP: ESP32 phải cùng mạng WiFi với máy tính
- Android Emulator: Dùng `10.0.2.2` thay vì `localhost`

### ESP32 không kết nối WiFi?
- ESP32 chỉ hỗ trợ WiFi 2.4GHz
- Kiểm tra Serial Monitor trong Arduino IDE

### Web không hiển thị dữ liệu?
- Đảm bảo ESP32/Simulator đang chạy
- Kiểm tra Console Browser (F12) xem có lỗi WebSocket

## 📋 Yêu cầu hệ thống

- Python 3.8+
- Docker
- Arduino IDE (cho ESP32 hardware)
- Flutter SDK (cho mobile app)

## 🎯 Tính năng

✅ ESP32-C3 với DHT11, LED, Motor  
✅ Web Dashboard real-time  
✅ Flutter Mobile App  
✅ SQLite Database logging  
✅ Discord Temperature Alerts  
✅ Multi-network support  

**Repository:** https://github.com/EurusDFIR/iot_lab5_monitor