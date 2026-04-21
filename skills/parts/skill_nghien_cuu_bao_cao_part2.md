# Phần 2/4: Cấu trúc 6 Chương chuẩn TDTU MauDATN_2021
> 💡 **Chú ý cho AI:** Đây là phần 2 của Skill Báo Cáo. Bạn cần đọc 4 phần để hoạt động chính xác.

## 6. Cấu Trúc 6 Chương Chuẩn TDTU

Mẫu từ `MauDATN_2021.docm` + `Báo cáo - BẢN CHÍNH.docm`:

```markdown
# TRANG BÌA
Trường Đại Học Tôn Đức Thắng
Khoa [Tên Khoa]
[TÊN ĐỀ TÀI — IN HOA, Bold, 24pt]
ĐỒ ÁN TỐT NGHIỆP / CHUYÊN NGÀNH NÂNG CAO
TP. Hồ Chí Minh, Năm ...

# LỜI CẢM ƠN | ACKNOWLEDGEMENT
# CAM ĐOAN | DECLARATION OF AUTHORSHIP
# MỤC LỤC | CONTENTS (Tự động từ Word)
# DANH MỤC HÌNH VẼ
# DANH MỤC BẢNG BIỂU  
# DANH MỤC CHỮ VIẾT TẮT

---

## CHƯƠNG 1. GIỚI THIỆU ĐỀ TÀI / OVERVIEW OF THE TOPIC
### 1.1 Giới thiệu đề tài / Topic Introduction
  (Bối cảnh thực tế, lý do chọn đề tài, tính cấp thiết)
### 1.2 Mục tiêu đề tài / Research objectives
  (Các mục tiêu cụ thể, đo lường được)
### 1.3 Đối tượng và phạm vi / Research subjects and scope
  (Phần cứng, phần mềm, giới hạn của đề tài)
### 1.4 Phương pháp tiếp cận / Architectural approach
  (3-layer architecture, pipeline, phương pháp nghiên cứu)

### 1.5 Đặc Tả Chức Năng Phần Mềm / Feature Specification  ← BẮT BUỘC PHẢI CÓ
  AI PHẢI SINH BẢNG USE CASE và danh sách chức năng người dùng từ source code.

  **Mẫu bảng đặc tả chức năng (Use Case Summary):**
  ```python
  add_table_caption(doc, '1.1', 'Đặc tả chức năng hệ thống')
  tbl = doc.add_table(rows=1, cols=4)
  tbl.style = 'Table Grid'
  h = tbl.rows[0].cells
  h[0].text = 'Mã UC'       # UC-01, UC-02...
  h[1].text = 'Tên chức năng'
  h[2].text = 'Tác nhân'    # Người dùng / Admin / System
  h[3].text = 'Mô tả ngắn'

  # AI TỰ SINH danh sách bên dưới bằng cách đọc routes, endpoints, screens từ source code:
  # VD quét thấy /api/booking, BookingScreen.tsx, servo.write → sinh chức năng đặt sân
  for uc in [
      ('UC-01', 'Đăng ký / Đăng nhập', 'Người dùng', 'Quản lý tài khoản, xác thực JWT'),
      ('UC-02', 'Xem danh sách tùy chọn', 'Người dùng', 'Lọc theo loại, tìm kiếm'),
      ('UC-03', 'Thực hiện thao tác chính', 'Người dùng', 'Kích hoạt cơ chế/quy trình'),
      ('UC-04', 'Theo dõi trật thếi thực', 'Người dùng', 'Dashboard real-time WebSocket/MQTT'),
      ('UC-05', 'Quản lý dữ liệu', 'Admin', 'CRUD, xuất báo cáo'),
      ('UC-06', '[Thế mạng chức năng đặc thù của dự án]', 'Người dùng', ''),
  ]:
      r = tbl.add_row().cells
      for i, v in enumerate(uc): r[i].text = v
  ```
  > ⚠️ AI **KHAI SINH** danh sách UC từ routes/endpoints/screens thực trong cód — không dùng VC chung chung.

## CHƯƠNG 2. CƠ SỞS LÝ THUYẾT / THEORETICAL FOUNDATIONS
### 2.1 [Lý thuyết cốt lõi 1] (VD: Kinematics, SLAM, PID...)
  **Yêu cầu:** Mỗi mục Chương 2 PHẢI KẼT THÚC bằng bảng so sánh công nghệ và đoạn "Kết luận lựa chọn".
  Xem mẫu bảng cụ thể tại Bước 5 (phần Deep Research Pipeline ở trên).
### 2.2 [Lý thuyết cốt lõi 2] (VD: Giao thức WebSocket, MQTT...)
### 2.3 [Công nghệ phần mềm] (VD: ROS2, React, NodeJS...)
### 2.4 [Thuật toán đặc biệt] (VD: Virtual Axle, State Machine...)

## CHƯƠNG 3. THIẾT KẾS PHẦN CỨNG / HARDWARE SYSTEM DESIGN
### 3.1 Sơ đồ khối hệ thống / Block Diagrams [Chèn Mermaid]
### 3.2 Sơ đồ nối dây chi tiết / Detailed wiring diagram [Bảng GPIO]
### 3.3 Sơ đồ nguyên lý / Schematic [Chèn ảnh hoặc mô tả]
### 3.4 Tính toán công suất và nguồn điện / Power Analysis
### 3.5 Danh sách linh kiện / Bill of Materials [Bảng BOM]

## CHƯƠNG 4. THIẾT KẾ HỆ THỐNG — TECHNOLOGY DEEP DIVE
*Đây là chương tập trung nhất vào công nghệ. AI PHẢI VIẾT SÂU, không ăn nói chung chung.*

### 4.1 Kiến Trúc Tổng Thể / Overall System Architecture
  - Sơ đồ khối Mermaid tương tác giữa các thành phần
  - Lý do chọn kiến trúc (monolithic / microservice / 3-layer / edge-cloud)
  - Bảng mô tả vai trò từng module

### 4.2 Lớp Firmware / Embedded Layer  [nếu có MCU]
  Bắt buộc nêu:
  - Flowchart vòng lặp chính (setup/loop hoặc RTOS task)
  - State machine (nếu có): vẽ Mermaid stateDiagram
  - Từng ISR / interrupt xử lý gì
  - Các tham số kỹ thuật thực đo được: tần số PWM, bộ lọc, overhead
  - Đoạn code quan trọng (1-2 hàm) + giải thích từng dòng

### 4.3 Lớp Giao Tiếp / Communication Layer  [MQTT / WebSocket / REST / ROS2]
  Bắt buộc nêu:
  - Sequence Diagram Mermaid: thứ tự gửi/nhận message
  - Topic/Endpoint/Action dùng cụ thể (lấy từ code thực tế)
  - Cấu hình QoS, timeout, retry logic
  - Lý do chọn giao thức (bảng so sánh từ Bước 5)
  - Xử lý lỗi kết nối (reconnect, heartbeat, offline queue)

### 4.4 Lớp Ứng Dụng / Application Layer  [Web / Mobile / Desktop]
  Bắt buộc nêu:
  - Component tree hoặc module diagram (Mermaid graph)
  - State management: Redux / Zustand / Context API
  - Các API call quan trọng (endpoint, payload, response format)
  - Authentication flow (nếu có JWT): Sequence Diagram
  - Database schema / ERD (nếu có DB)
  - Ảnh chụp màn hình thực tế + chú thích chức năng từng màn hình

### 4.5 Thuật Toán / Algorithm Implementation
  Bắt buộc nêu:
  - Phương trình toán (dùng `add_equation`) kèm ý nghĩa từng biến
  - Pseudocode hoặc flowchart thuật toán chính
  - Độ phức tạp O(n) nếu liên quan
  - Tham số thực tế đã hiệu chỉnh (VD: K_p=1.2, K_i=0.05, ngưỡng callback=10ms)

## CHƯƠNG 5. TRIỂN KHAI & KIỂM THỬ / IMPLEMENTATION & TESTING
*Chương này PHẢI có số liệu thực đo/chạy thực tế. KHÔNG ĐƯỢC CHUNG CHUNG.*

### 5.1 Môi Trường Triển Khai / Deployment Environment
  - Phần cứng thực tế (tên board, firmware version, thư viện chính)
  - Phần mềm (OS, IDE, package version; lấy từ requirements.txt/package.json)
  - Sơ đồ triển khai Mermaid (ai cài ở đâu, port nào, IP)

### 5.2 Kết Quả Kiểm Thử Chức Năng / Functional Testing
  - Bảng test case: Mã TC, chức năng, đầu vào, kết quả mong muốn, kết quả thực tế, Pass/Fail
  - Ảnh chụp màn hình kết quả thực tế từng chức năng
  - Video demo (nếu có link YouTube/Drive → chèn dưới dạng URL hyperlink)

### 5.3 Phân Tích Hiệu Năng / Performance Benchmarks
  *Số liệu thực tế bắt buộc — AI điền số đo được, không bịa:*
  | Chỉ số | Đo được | Mục tiêu |
  |---|---|---|
  | MQTT latency (avg) | ?? ms | < 50 ms |
  | API response time | ?? ms | < 200 ms |
  | FPS xử lý khung hình | ?? FPS | > 15 FPS |
  | Thời gian pin | ?? giờ | > 5 giờ |

### 5.4 Đánh Giá và Hạn Chế / Evaluation & Limitations
  - So sánh kết quả với mục tiêu đã nêu tại 1.2 (trích dẫn lại)
  - Hạn chế còn tồn tại (trung thực, không giấu giếm)
  - Nguyên nhân và đề xuất cải tiến cho tương lai

## CHƯƠNG 6. KẾT LUẬN / CONCLUSION AND FUTURE DEVELOPMENT
### 6.1 Kết luận / Conclude
### 6.2 Hướng phát triển / Development direction

## TÀI LIỆU THAM KHẢO (Kiểu APA 6th) ← BẮT BUỘC URL THẬT
  *Xem quy tắc chi tiết tại mục 8.2 bên dưới*
## PHỤ LỤC A: MÃ NGUỒN (Code quan trọng)
```

---
