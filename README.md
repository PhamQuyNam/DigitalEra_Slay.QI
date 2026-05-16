# 🌫️ AirGuard BN - Hệ thống Giám sát & Dự báo Chất lượng Không khí

> **Đồ án tốt nghiệp Kỹ thuật phần mềm**  
> Ứng dụng mô hình Hybrid **LSTM** và **XGBoost-SHAP** để giám sát, dự báo và giải thích nguyên nhân ô nhiễm không khí tại 18 làng nghề tỉnh Bắc Ninh.

---

## 📖 Giới thiệu dự án

Bắc Ninh là khu vực tập trung nhiều làng nghề công nghiệp, đối mặt với thách thức lớn về ô nhiễm môi trường. **AirGuard BN** là giải pháp công nghệ toàn diện giúp:
- 📍 **Giám sát thời gian thực**: Bản đồ GIS hiển thị chỉ số AQI của 18 làng nghề trọng điểm.
- 🔮 **Dự báo tương lai**: Sử dụng mạng **LSTM** để dự báo diễn biến AQI trong 6-24 giờ tới.
- 🔍 **Giải thích nguyên nhân**: Ứng dụng **SHAP (SHapley Additive exPlanations)** để phân tích các yếu tố (Bụi mịn, Khí thải, Khí hậu) ảnh hưởng đến mức độ ô nhiễm.
- 🔔 **Cảnh báo thông minh**: Tự động gửi thông báo đến người dân khi chất lượng không khí đạt mức nguy hại.

---

## 🏗️ Kiến trúc công nghệ

| Thành phần | Công nghệ sử dụng |
|---|---|
| **Frontend** | React.js (Vite), TailwindCSS, Framer Motion, Leaflet (GIS Map) |
| **Backend** | FastAPI (Python), SQLModel, APScheduler (Tự động nạp dữ liệu) |
| **Database** | PostgreSQL + **TimescaleDB** (Tối ưu hóa dữ liệu chuỗi thời gian) |
| **AI Models** | **LSTM** (Dự báo), **XGBoost** + **SHAP** (Phân tích nguyên nhân) |
| **DevOps** | Docker, Docker Compose |

---

## 🚀 Hướng dẫn cài đặt nhanh

### 1. Yêu cầu tiên quyết
- **Docker & Docker Compose** (Khuyến nghị dùng Docker Desktop).
- **Node.js** (Phiên bản 18 trở lên).
- Các file mô hình AI đã huấn luyện (được cung cấp trong thư mục dự án).

### 2. Các bước cài đặt

#### Bước 1: Chuẩn bị mô hình AI
Đảm bảo các file mô hình đã nằm đúng vị trí trong thư mục dự án:
- `models/lstm/best_lstm_model.h5`
- `models/xgboost/xgboost_aqi_6h.pkl`

#### Bước 2: Khởi động Backend & Database (Docker)
Mở terminal tại thư mục gốc và chạy:
```powershell
docker-compose up -d
```
*Lệnh này sẽ tự động thiết lập Database, nạp bù dữ liệu 48h gần nhất và kích hoạt bộ não AI chạy ngầm.*

#### Bước 3: Khởi động Frontend
Mở một terminal mới:
```powershell
cd frontend
npm install
npm run dev
```

### 3. Truy cập hệ thống
- **Giao diện người dùng**: [http://localhost:5173](http://localhost:5173)
- **Tài liệu API (Swagger)**: [http://localhost:8000/docs](http://localhost:8000/docs)
- **Tài khoản Admin mặc định**:
  - Email: `admin@airguard.vn`
  - Mật khẩu: `admin123`

---

## 🧠 Cơ chế vận hành AI

Hệ thống được thiết kế để hoạt động hoàn toàn tự động:
- **Tự động cập nhật**: Cứ mỗi **5 phút**, hệ thống tự động thu thập dữ liệu mới, chạy dự báo AI và cập nhật biểu đồ SHAP.
- **Chạy AI thủ công**: Nếu bạn muốn cập nhật kết quả AI ngay lập tức, hãy sử dụng lệnh:
  ```powershell
  docker-compose run backend python -c "from app.services.inference_service import inference_service; inference_service.run_forecast_all()"
  ```
- **Lazy Loading**: Backend khởi động cực nhanh nhờ cơ chế nạp mô hình khi cần, tránh làm treo hệ thống khi gặp lỗi tương thích file `.h5`.

---

## 📊 Danh sách 18 làng nghề giám sát

Dự án tập trung vào 18 làng nghề tiêu biểu tại Bắc Ninh:
1. **Phong Khê** (Giấy) | 2. **Đồng Kỵ** (Gỗ) | 3. **Đa Hội** (Thép) | 4. **Đại Bái** (Đúc đồng) | 5. **Văn Môn** (Nhôm) | 6. **Phù Lãng** (Gốm)... và các làng nghề khác theo bản đồ GIS.

---

## 👨‍💻 Thông tin tác giả

- **Sinh viên thực hiện**: Phạm Qúy Nam
- **Giáo viên hướng dẫn**: ThS. Nguyễn Thái Cường
- **Trường**: Đại học Công Nghiệp Hà Nội (HaUI)
- **Năm hoàn thành**: 2026

---
<div align="center">
  <strong>AirGuard BN</strong> — Vì một môi trường sống trong lành và bền vững 🌿
</div>
