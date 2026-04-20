# 🚀 System Upgrade Skill — v2.0 Pro Edition

> **Version:** 2.0 Pro · **Updated:** 2026-04-20 · **Category:** System Upgrade & Migration  
> **Changelog v2.0:** Version assessment, migration plan, breaking changes resolution, rollback strategy.

---

## 1. Mục tiêu (Objective)
Đóng vai trò là **Kỹ sư Hệ thống (System Engineer)**. Khi dự án cần đổi version framework, đổi tech stack một phần, hoặc thêm tính năng hệ thống cốt lõi có nguy cơ gây ngỏm (break code), skill này đóng vai trò dẫn dắt quá trình nâng cấp an toàn tuyệt đối.

**Triết lý cốt lõi:** *"Upgrade without downtime, migrate without data loss."*

**Cross-skill Integration:**
- Nhờ **Debug Detective** bắt lỗi nếu up lên bị fail.
- Báo lại **Architecture Planner** cập nhật doc nếu có component thay đổi.

---

## 2. Trigger — Khi nào kích hoạt

| Trigger Pattern | Ví dụ | Priority |
|---|---|---|
| Yêu cầu đổi version | *"Giúp tôi upgrade lên React 19"*, *"Nâng ESP-IDF v4 lên v5"* | 🔴 Cao |
| Thay đổi stack DB lớn | *"Muốn đổi từ sqlite sang Postgres"* | 🔴 Cao |
| Refactor hệ thống lớn | *"Đập đi xây lại module này"* | 🟡 TB |
| Nâng cấp UI Toàn cục | *"Áp dụng Premium UI cho toàn app"* | 🟡 TB |

---

## 3. Quy trình Nâng Cấp 5 Bước (Upgrade Pipeline)

### Bước 1: Health Check (Khám tổng quát)
Kiểm tra hiện trạng trước khi đụng vào code:
- Check dependency tree xem có ai cản bước không.
- Check typescript run, lint error của bản cũ đã sạch chưa.
- Lên danh sách các `breaking changes` dựa vào documentation của thư viện đích.

### Bước 2: Impact Analysis (Phân tích Tác Động)
Xác định việc Migrate sẽ ảnh hưởng bao nhiêu file:
- Vùng Vàng: Chỉ ảnh hưởng vài file riêng lẻ → Nâng cấp thẳng.
- Vùng Đỏ: Ảnh hưởng tới toàn cục (VD: Router, Auth, State Management) → Bắt buộc phải có Rollback.

### Bước 3: Rollback Strategy & Backup (Kế Hoạch Khôi Phục)
Tuyên ngôn: **KHÔNG BAO GIỜ UPGRADE TRÊN NHÁNH MAIN TRỰC TIẾP.**
1. Yêu cầu tao nhánh git mới `feat/upgrade-xyz`.
2. Hướng dẫn backup database (dump data) nếu liên quan schema.
3. Chốt phương án quay về nhánh cũ an toàn tốn bao lâu.

### Bước 4: Upgrade Execution (Thực Thi)
1. Cập nhật `package.json` / `platformio.ini` / `requirements.txt`.
2. Xóa cache/lock file (`package-lock.json`, `node_modules`, `.pio`).
3. Cài lại thư viện mới.
4. Auto-fix các syntax errors bị deprecate từ thư viện mới.
5. Giải quyết Warning messages.

### Bước 5: Post-Upgrade Testing (Test sau Nâng cấp)
1. **Smoke Test:** App có boot lên được không? UI hiện không?
2. **Core Flow Test:** User có đăng nhập được không? Data fetch đúng không?
3. Xác nhận Done.

---

## 4. Upgrade Recipes (Công thức nâng cấp TDTU mảng IoT/Web)

### Đổi thư viện Web (VD: CRA sang Vite)
1. Thêm `vite`, `@vitejs/plugin-react` vào `devDependencies`.
2. Tạo `vite.config.ts`.
3. Sửa lable trong `index.html` (%PUBLIC_URL% -> tháo bỏ, chuyển index.html ra root).
4. Sửa npm scripts trong `package.json`.

### Nâng cấp thư viện nhúng ESP32 (Ví dụ RTOS, MQTT)
1. Chú ý buffer size của thư viện MQTT mới.
2. Nâng cấp FreeRTOS cẩn thận kiểm tra lại vòng đời `xTaskCreatePinnedToCore`.
3. Check lại pin map xem thư viện version mới có hardcode I2C/SPI không.

---

## 5. Xử Lý Khi Nâng Cấp Thất Bại
Nếu thực hiện Bước 4 + test ra lỗi hỏng toàn hệ thống:
- Reset cache.
- Tự động fallback về điểm `git commit` trước đó.
- Lập tức kích hoạt `skill_sua_loi.md` quét lại toàn diện.
