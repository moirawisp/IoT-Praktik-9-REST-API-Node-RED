# IoT Praktik 9: REST API Node-RED

Sistem monitoring dan kontrol IoT dengan ESP32 (disimulasikan), MQTT, Node-RED sebagai backend REST API, dan dashboard web buatan sendiri.

## Fitur Bonus
- PUT /api/threshold untuk mengatur batas suhu, disertai notifikasi saat suhu melewati batas
- Grafik real-time dengan Chart.js
- Autentikasi sederhana dengan header X-API-Key
- WebSocket di Node-RED untuk update tanpa polling
- Riwayat data disimpan di SQLite

## Kebutuhan
- Node.js dan Node-RED
- Mosquitto (MQTT broker, localhost:1883)
- Python 3 dan paho-mqtt (`pip install paho-mqtt`)
- Palette Node-RED: node-red-node-sqlite

## Cara Menjalankan
1. Jalankan broker: `mosquitto -v`
2. Jalankan Node-RED: `node-red`, lalu import `flows.json` dan Deploy
3. Jalankan simulator: `python simulasi_esp32.py`
4. Buka `dashboard.html` di browser

## Endpoint
| Endpoint | Method | Fungsi |
|---|---|---|
| /api/suhu | GET | Data sensor terakhir |
| /api/history | GET | Riwayat data dari SQLite |
| /api/kontrol | POST | Kirim perintah ke perangkat |
| /api/threshold | GET, PUT | Lihat dan atur batas suhu |

Semua endpoint memerlukan header `X-API-Key`.

## Contoh Penggunaan
```
curl http://localhost:1880/api/suhu -H "X-API-Key: iot-kampus-2026"
curl -X PUT http://localhost:1880/api/threshold -H "Content-Type: application/json" -H "X-API-Key: iot-kampus-2026" -d "{\"batas\": 30}"
```
Tanpa header yang benar, server mengembalikan 401.
API key diatur lewat environment variable API_KEY pada flow REST API IoT (nilai: iot-kampus-2026).

## Screenshot
Dashboard

<img width="766" height="1236" alt="image" src="https://github.com/user-attachments/assets/50921158-6574-4e6e-9006-1cea39c98e10" />

Flow Node-RED

<img width="807" height="638" alt="image" src="https://github.com/user-attachments/assets/4e73a01e-d640-4644-8c0c-913d00ce9003" />

WebSocket
<img width="1090" height="465" alt="image" src="https://github.com/user-attachments/assets/cd779eb9-97a9-4fb9-9f47-5581f50dc69e" />
