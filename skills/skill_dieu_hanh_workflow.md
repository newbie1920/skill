# 🧠 Master Workflow Orchestrator (Điều phối viên)

> **Version:** 2.0 Pro · **Updated:** 2026-04-20 · **Category:** Workflow Management  
> **Trạng thái:** LUÔN HOẠT ĐỘNG ngầm để đánh giá Task.
> **Tính năng v2.0:** Tự động nhận diện độ khó, Cây quyết định skill (Decision Matrix), Pipeline Mermaid 5 Bước.

## 0. Complexity Detection (Tự Động Đánh Giá Độ Khó)
Trước khi tư vấn, AI đánh giá vòng đầu nhanh độ phức tạp:
1. **Low (T-Shirt S):** Sửa lỗi nhỏ, đổi màu, viết 1 file script. ➔ **Bỏ qua Pipeline dài**, code thẳng hoặc gọi nhẹ Debug/Snippet.
2. **Medium (T-Shirt M - L):** Thêm Feature, sửa > 3 file. ➔ **Gọi Pipeline Bước 3 & 4**.
3. **High (T-Shirt XL):** Làm App mới, cấu trúc lại hệ thống, làm Đồ án. ➔ **Chạy Toàn Bộ Chuỗi 5 Bước Nghiêm Ngặt**.

## 1. CƠ CHẾ HOẠT ĐỘNG BẮT BUỘC (CHAIN OF ACTION)
Mỗi khi User đưa ra một yêu cầu lớn (Cấp độ High), AI BẮT BUỘC PHẢI DỪNG LẠI (không được lao vào code ngay) và thực thi chuỗi Pipeline sau:

```mermaid
flowchart LR
    A[Step 1: Ideation & Plan] --> B[Step 2: Boilerplate Code] 
    B --> C[Step 3: Design & Core] 
    C --> D[Step 4: Fix & Upgrade] 
    D --> E[Step 5: Thesis & Docs]
    
    style A fill:#6c63ff,color:#fff
    style C fill:#ff9800,color:#fff
    style E fill:#00c853,color:#fff
```

### Bước 1: Ý tưởng, Kế hoạch & Thiết kế (Planning & Design)
- **Trạng thái user:** "tạo 1 project làm...", "mốc 3 tháng làm xong game..."
- 🛠️ **Hành động AI:** 
  1. Đề xuất bật **`skill_viet_prompt.md`** để làm nét yêu cầu.
  2. Bật ngay **`skill_len_ke_hoach.md`** để lập Timeline, WBS và bắt rủi ro.
  3. Bật **`skill_kien_truc.md`** để sinh kiến trúc Data/Thuật Toán/Topology tương đồng với Timeline. Bắt buộc user duyệt.

### Bước 2: Sinh Code Nền Tảng (Boilerplate)
- **Trạng thái user:** "ok kế hoạch", "duyệt bắt đầu làm đi"
- 🛠️ **Hành động AI:** Dùng **`skill_code_mau.md`** (Snippet Factory) để tạo Base Files, Folder Structures siêu tốc.

### Bước 3: Phát triển Giao diện & Core (Development)
- 🛠️ **Hành động AI:** 
  - Backend/Hardware code theo Core Data Model.
  - Frontend/UI: Kích hoạt **`skill_giao_dien.md`** tạo giao diện hiệu ứng Premium Cinematic / Glassmorphism.

### Bước 4: Review, Sửa Lỗi & Nâng cấp Hệ Thống (Quality Gates & Scale)
- **Trạng thái user:** Log đỏ / Code lag / Thay Server / Update version thư viện
- 🛠️ **Hành động AI:**
  - Lỗi Debug: Bật **`skill_sua_loi.md`** (Debug Detective) điều tra nguyên nhân rễ.
  - Cần Refactor: Bật **`skill_toi_uu.md`** quét smells.
  - Up Version / Migration: Bật **`skill_nang_cap.md`** lập Backup Zone trước khi phá đồ.

### Bước 5: Viết Báo Cáo & Thu Hoạch (Documentation)
- **Trạng thái user:** "mai nộp báo cáo", "làm file word lẹ", "giải thích code"
- 🛠️ **Hành động AI:**
  - Viết README, comment code nhanh: Dùng **`skill_viet_docs.md`**.
  - Phân tích chuyên sâu toàn bộ code & Xuất Luận Văn DOCX (có sơ đồ/toán): Bật siêu kỹ năng **`skill_nghien_cuu_bao_cao.md`**.

---

## 2. Decision Matrix Bảng Chuyển Hướng 

| Yêu Cầu Hiện Tại Của User | AI Phản Xạ Skill Nào |
| --- | --- |
| *"Tao muốn viết 1 App hẹn hò sinh viên"* | ➔ Step 1: `skill_len_ke_hoach` + `skill_kien_truc` |
| *"Anh ơi cái ESP32 nhấp nháy đỏ quài"* | ➔ Step 4: `skill_sua_loi` (Debug) |
| *"Viết giùm tui boilerplate Zustand React"* | ➔ Step 2: `skill_code_mau` (Snippet Factory) |
| *"Nâng cái đồ án này lên NodeJS 20"* | ➔ Step 4: `skill_nang_cap` (Upgrade Guard) |
| *"Chê UI này phèn quá m ơi"* | ➔ Step 3: `skill_giao_dien` (Premium Cinematic) |
| *"Bà GVHD đòi file báo cáo 5 chương :("* | ➔ Step 5: `skill_nghien_cuu_bao_cao` (Deep Thesis) |

> ⚠️ **QUY TẮC CỨNG:** Mỗi session chát, AI LUÔN định hình mình đang ở Step nào của Flow (1 -> 5) và announce để user theo kịp mạch tư duy. Không để rớt nhịp!
