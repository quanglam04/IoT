# 🌱 IoT Project – Smart Environment Monitoring & Control

## 📌 Introduction

Dự án IoT này được xây dựng nhằm **giám sát và điều khiển môi trường** (nhiệt độ, độ ẩm, áp suất, mưa, …) thông qua hệ thống cảm biến và bộ điều khiển ESP32.  
Dữ liệu thu thập được sẽ được gửi về server NodeJS/ExpressJS, lưu trữ trên **MongoDB Atlas**, đồng thời hiển thị trực quan trên giao diện web (React + TypeScript).  
Ngoài ra, hệ thống cũng có thể điều khiển **máy bơm, động cơ DC**… theo điều kiện thực tế.

---

## 🛠️ Tech Stack

### Development Tools

- **Arduino IDE**
- **Visual Studio Code**

### Backend / Server

- **NodeJS (22.17.1)**
- **ExpressJS**
- **Web Service**: HTTP

### Database & Cloud

- **MongoDB**
- **MongoDB Atlas**

### AI / ML

- **TensorFlow.js** (inference trên Node: `@tensorflow/tfjs-node`)
- (Tùy chọn) **TensorFlow (Python)** hoặc **PyTorch** để huấn luyện offline và convert model sang TF.js format.

### Hardware

- **Vi điều khiển:** ESP32
- **Cảm biến:**
  - SHT30 (nhiệt độ, độ ẩm)
  - BMP280, BME280 (áp suất không khí, nhiệt độ, độ ẩm)
  - Cảm biến mưa
- **Thiết bị điều khiển:**
  - Nguồn 12V
  - Module bơm
  - Động cơ DC 1 chiều
  - Linh kiện vỏ, phụ kiện khác
- **Mạch nguyên lý:** Proteus 8

## Project Structure

```
IoT/
│
├── Code/
│   ├── ai/                  # Thư mục AI model (train/inference code)
│   │    └── ...
│   │
│   ├── hardware/            # Code chạy trên ESP32 (C++)
│   │    └── example.cpp     # Ví dụ code kết nối & gửi dữ liệu
│   │
│   └── server/              # Backend server (NodeJS + Express)
│        ├── config/         # Cấu hình (DB connection, env)
│        ├── controllers/    # Xử lý logic cho từng route
│        ├── models/         # Định nghĩa schema cho MongoDB
│        ├── node_modules/   # Thư viện cài từ npm
│        ├── public/         # Static files (CSS, JS, images)
│        ├── routes/         # Khai báo các API endpoint + web routes
│        ├── templates/      # View engine (EJS templates)
│        ├── utils/          # Các hàm tiện ích (gọi AI service, helper)
│        ├── .env            # Config bí mật (DB URI, API key)
│        ├── .gitignore      # File loại trừ khi push Git
│        ├── index.js        # File chính, khởi tạo Express server
│        ├── package.json    # Khai báo dependencies
│        └── package-lock.json
│
├── Documents/               # Tài liệu báo cáo & slide
│    ├── Báo cáo cuối kỳ.docx
│    ├── Báo cáo giữa kỳ.docx
│    └── slide.txt
│
└── README.md                # File mô tả dự án
```

---

## 👨‍💻 Team Members

- Trịnh Quang Lâm
- Cao Thị Thu Hương
- Vũ Thế Văn
- Vũ Nhân Kiên

---
