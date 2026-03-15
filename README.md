# 🌱 IoT Project – Smart Environment Monitoring & Control

## 📌 Introduction

Dự án IoT này được xây dựng nhằm **giám sát và điều khiển môi trường** (nhiệt độ, độ ẩm, áp suất, mưa, …) thông qua hệ thống cảm biến và bộ điều khiển ESP32.  
Dữ liệu thu thập được sẽ được gửi về server NodeJS/ExpressJS, lưu trữ trên **MongoDB Atlas**, đồng thời hiển thị trực quan trên giao diện web (React + TypeScript).  
Ngoài ra, hệ thống cũng có thể điều khiển **máy bơm, động cơ DC**… theo điều kiện thực tế.

---

## 🛠️ Tech Stack

<table>
  <thead>
    <tr>
      <th>Category</th>
      <th>Subcategory</th>
      <th>Technology</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="3"><strong>Development & Version Control</strong></td>
      <td>Môi trường phát triển</td>
      <td>PlatformIO, Visual Studio Code</td>
    </tr>
    <tr>
      <td>Quản lý mã nguồn</td>
      <td>Git/Github Server</td>
    </tr>
    <tr>
      <td>Mạch nguyên lý</td>
      <td>Cirkit Designer</td>
    </tr>
    <tr>
      <td rowspan="6"><strong>Backend / Server & Protocol</strong></td>
      <td>Core</td>
      <td>NodeJS</td>
    </tr>
    <tr>
      <td>Web Framework</td>
      <td>ExpressJS</td>
    </tr>
    <tr>
      <td>Ngôn ngữ</td>
      <td>TypeScript</td>
    </tr>
    <tr>
      <td>Web Protocol</td>
      <td>HTTP</td>
    </tr>
    <tr>
      <td>IoT Protocol</td>
      <td>MQTT Protocol</td>
    </tr>
    <tr>
      <td>Real-time</td>
      <td>Socket.io</td>
    </tr>
    <tr>
      <td rowspan="2"><strong>Database & Cloud</strong></td>
      <td>Database</td>
      <td>MongoDB, MongoDB Atlas (Cloud)</td>
    </tr>
    <tr>
      <td>MQTT Broker</td>
      <td>HiveMQ Cloud</td>
    </tr>
    <tr>
      <td><strong>AI / ML</strong></td>
      <td>Core Model</td>
      <td>XGBoost</td>
    </tr>
    <tr>
      <td rowspan="6"><strong>Hardware</strong></td>
      <td>Vi điều khiển</td>
      <td>ESP32 (DevKit V1)</td>
    </tr>
    <tr>
      <td>Cảm biến</td>
      <td>BME280, DHT22</td>
    </tr>
    <tr>
      <td>Thiết bị điều khiển</td>
      <td>Bơm nước mini 12V</td>
    </tr>
    <tr>
      <td>Module điều khiển</td>
      <td>Module MOSFET</td>
    </tr>
    <tr>
      <td>Nguồn</td>
      <td>12V</td>
    </tr>
    <tr>
      <td>Giao diện người dùng</td>
      <td>ReactJS</td>
    </tr>
  </tbody>
</table>

---

## Project Structure

```
IoT/
│
├── Code/
│   ├── ai/                       # Thư mục AI model (train/inference code - Python)
│   │    ├── data/                # Dữ liệu huấn luyện và kiểm thử
│   │    ├── models/              # Model đã train (weights, checkpoints)
│   │    ├── src/                 # Code xử lý dữ liệu, tiền xử lý, inference
│   │    ├── train/               # Script huấn luyện model
│   │    ├── .env                 # Config bí mật (API key, đường dẫn model,…)
│   │    └── requirements.txt     # Thư viện Python cần thiết (TensorFlow, scikit-learn,…)
│   │
│   ├── hardware/                 # Code chạy trên ESP32 (C++ / Arduino)
│   │    ├── control/             # Xử lý điều khiển (bơm nước, quạt, relay,…)
│   │    ├── network/             # Cấu hình & quản lý kết nối Wi-Fi, MQTT, HTTP,...
│   │    ├── sensors/             # Đọc dữ liệu cảm biến (nhiệt độ, độ ẩm, ánh sáng,…)
│   │    ├── utils/               # Hàm tiện ích dùng chung (convert, log, delay,…)
│   │    ├── config.h             # File cấu hình (SSID, password, broker, topic,…)
│   │    └── main.ino             # Chương trình chính của ESP32
│   │
│   ├── server/                   # Backend server (NodeJS + Express)
│   │    ├── config/              # Cấu hình (DB connection, env)
│   │    ├── controllers/         # Xử lý logic cho từng route
│   │    ├── middlewares/         # Xử lý logic cho từng route
│   │    ├── models/              # Định nghĩa schema cho MongoDB
│   │    ├── node_modules/        # Thư viện cài từ npm
│   │    ├── public/              # Static files (CSS, JS, images)
│   │    ├── routes/              # Khai báo các API endpoint + web routes
│   │    ├── sockets/             # Khai báo socket giao tiếp real-time
│   │    ├── services/            # Xử lý logic nghiệp vụ
│   │    ├── templates/           # View engine (EJS templates)
│   │    ├── utils/               # Các hàm tiện ích (gọi AI service, helper)
│   │    ├── shared/              # Code tái sử dụng chung
│   │    │    ├── constants/      # Các hằng số cấu hình, giá trị dùng chung
│   │    │    └── types/          # Định nghĩa kiểu dữ liệu, interface
│   │    ├── .env                 # Config bí mật (DB URI, API key)
│   │    ├── .gitignore           # File loại trừ khi push Git
│   │    ├── index.js             # File chính, khởi tạo Express server
│   │    ├── package.json         # Khai báo dependencies
│   │    └── package-lock.json    # File lock dependencies
│   │
│   └── client/                   # Frontend (React + TypeScript, Vite)
│        ├── public/              # Static assets (favicon, images tĩnh,…)
│        ├── src/                 # Source code chính
│        │   ├── app/             # Core app: layout, pages, styles
│        │   │   ├── layout/      # Layout tổng thể (header, sidebar,…)
│        │   │   ├── pages/       # Các trang chính (Home, Dashboard,…)
│        │   │   ├── styles/      # File CSS/SCSS module
│        │   │   ├── index.tsx    # Entry React app
│        │   │   └── router.tsx   # Định nghĩa router (React Router)
│        │   │
│        │   ├── assets/          # Tài nguyên tĩnh dùng trong app
│        │   │   ├── fonts/       # Font chữ
│        │   │   └── images/      # Hình ảnh
│        │   │
│        │   ├── services/        # Các service gọi API, thao tác Socket
│        │   │
│        │   └── shared/          # Code tái sử dụng chung
│        │       ├── components/  # Component tái sử dụng (button, modal,…)
│        │       ├── constants/   # Các hằng số (API endpoint, config,…)
│        │       ├── context/     # React context (state toàn cục)
│        │       ├── hook/        # Custom hooks
│        │       ├── services/    # Service chung (auth, storage,…)
│        │       ├── types/       # Định nghĩa TypeScript types/interface
│        │       └── utils/       # Hàm tiện ích (format date, string,…)
│        │
│        ├── vite-env.d.ts        # Khai báo env cho Vite + TS
│        ├── .editorconfig        # Quy chuẩn code style
│        ├── .env.development     # Biến môi trường (dev)
│        ├── .env.production      # Biến môi trường (prod)
│        ├── .gitignore           # Loại file không push Git
│        ├── .prettierignore      # Loại file không format
│        ├── .prettierrc          # Config Prettier
│        ├── eslint.config.js     # Config ESLint
│        ├── index.html           # HTML template
│        ├── package.json         # Khai báo dependencies frontend
│        └── package-lock.json    # File lock dependencies frontend
│
├── Documents/                    # Tài liệu báo cáo & slide
│    ├── Báo cáo giữa kỳ.docx
│    ├── Báo cáo cuối kỳ.docx
│    └── slide.txt
│
└── README.md                     # File mô tả dự án

```

---

## 👨‍💻 Team Members

- Trịnh Quang Lâm (Leader)
- Cao Thị Thu Hương
- Vũ Thế Văn
- Vũ Nhân Kiên

---

## System Design

<p align="center">
  <img src="./Code/img/Sơ đồ tổng quan.png" alt="Image title_1" />
</p>

## Result

<p align="center">
  <img src="./Code/img/kq1.png" alt="Image title_1" />
  <p align="center">Giao diện Dashboard</p>
</p>
<br>

<p align="center">
  <img src="./Code/img/kq2.png" alt="Image title_1" />
  <p align="center">Giao diện hiển thị thay đổi biểu đồ trong ngày</p>
</p>
<br>

<p align="center">
  <img src="./Code/img/kq3.png" alt="Image title_1" />
  <p align="center">Giao diện lịch tưới tự động</p>
</p>
<br>

<p align="center">
  <img src="./Code/img/kq4.png" alt="Image title_1" />
  <p align="center">Giao diện nhật ký</p>
</p>
<br>

<p align="center">
  <img src="./Code/img/kq5.png" alt="Image title_1" />
  <p align="center">Giao diện báo cáo</p>
</p>
<br>

<p align="center">
  <img src="./Code/img/kq6.png" alt="Image title_1" />
  <p align="center">Giao diện cập nhật firmware</p>
</p>
<br>

<p align="center">
  <img src="./Code/img/kq7.png" alt="Image title_1" />
  <p align="center">Giao diện quản lý người dùng</p>
</p>
