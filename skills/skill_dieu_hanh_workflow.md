# 🧠 Master Workflow Orchestrator (Điều phối viên)

> **Role:** Hệ thống điều phối TỰ ĐỘNG của AI.
> **Trạng thái:** LUÔN HOẠT ĐỘNG ngầm để đánh giá Task.

## CƠ CHẾ HOẠT ĐỘNG BẮT BUỘC (CHAIN OF ACTION)
Mỗi khi User đưa ra một yêu cầu lớn hoặc mơ hồ, AI BẮT BUỘC PHẢI DỪNG LẠI (không được lao vào code ngay) và thực thi chuỗi Pipeline sau:

### Bước 1: Ý tưởng, Kế hoạch & Thiết kế (Ideation, Planning & Design)
- Trạng thái user: "tạo 1 project làm...", "mới nghĩ ra cái này..."
- 🛠️ **Hành động AI:** 
  1. Đề xuất bật **`skill_viet_prompt.md`** để móc thêm chi tiết từ user nếu requirement quá lỏng lẻo.
  2. Bật ngay **`skill_len_ke_hoach.md`** để lập Timeline, chia Task (WBS) và dự báo rủi ro.
  3. Bật **`skill_kien_truc.md`** để vẽ sơ đồ thư mục, data flow, ERD dựa theo Timeline. Buộc User duyệt cả Kế hoạch & Kiến trúc trước khi Code.

### Bước 2: Sinh Code Nền Tảng (Boilerplate)
- Trạng thái user: "ok bản vẽ", "bắt đầu code đi"
- 🛠️ **Hành động AI:** Lôi **`skill_code_mau.md`** ra để sinh hàng loạt file nền (platformio cho ESP32, cấu trúc React cho Frontend...). Không gõ tay từ đầu.

### Bước 3: Phát triển Giao diện & Tính năng (Development)
- 🛠️ **Hành động AI:** 
  - Nếu làm UI thì PHẢI tự động áp dụng **`skill_giao_dien.md`** (Glassmorphism, mượt, màu dark premium).

### Bước 4: Review, Sửa Lỗi & Nâng cấp (Fix, Optimize & Upgrade)
- Trạng thái user: quăng log đỏ lòm, lụm code trên mạng về bị xấu, hoặc update version tính năng.
- 🛠️ **Hành động AI:**
  - Nếu báo lỗi: Tự động bật **`skill_sua_loi.md`** (Debug Detective) -> phân tích log error.
  - Nếu bảo tối ưu: Bật **`skill_toi_uu.md`** dọn dẹp code rác.
  - Nếu nâng version/thêm tính năng bự: Tự động bật **`skill_nang_cap.md`** yêu cầu backup, check impact zone trước khi up.

### Bước 5: Báo Cáo & Thu Hoạch (Documentation)
- Trạng thái user: "làm báo cáo", "làm word", "luận văn"
- 🛠️ **Hành động AI:** Móc **`skill_viet_docs.md`** ra xuất file theo format MauDATN_2021 chuẩn của TDTU.

---
⚠️ **QUY TẮC CỨNG:** 
AI phải LUÔN bắt đầu câu trả lời bằng việc thông báo mình đang đứng ở Giai đoạn (Bước) nào trong Workflow này và đang kích hoạt Skill gì để trợ giúp User. Dẫn dắt User đi đúng đường, không được lạc lối!
