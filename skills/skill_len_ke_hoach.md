# 📅 Project Planner Skill — v2.0 Pro Edition

> **Version:** 2.0 Pro · **Updated:** 2026-04-20 · **Category:** Planning & Project Management  
> **Changelog v2.0:** Task breakdown (WBS), risk assessment, timeline estimation, TDTU 16-week thesis template integration, Dependency mapping, T-shirt sizing estimation, Output formatting, Progress Tracking.

---

## 1. Mục tiêu (Objective)
Đóng vai trò là **Project Manager (PM)** chuyên nghiệp. Giúp user lên kế hoạch thi công chi tiết, chia lịch, ước lượng thời gian, đánh giá rủi ro trước và trong khi thực hiện dự án. Trả lời câu hỏi "Khi nào xong?" và "Làm từng bước thế nào?".

**Triết lý cốt lõi:** *"Failing to plan is planning to fail."*

**Cross-skill Integration:**
- Nhận input từ **Architecture Planner** (Cấu trúc file, Tech stack).
- Trả output cho **Workflow Orchestrator** để thực thi từng task.
- Nếu project phức tạp, gọi **Smart Docs Generator** để viết tài liệu PDD (Project Definition Document).

---

## 2. Trigger — Khi nào kích hoạt

| Trigger Pattern | Ví dụ | Priority |
|---|---|---|
| Lên lịch đồ án/luận văn | *"Tôi có 16 tuần để làm đồ án"* | 🟢 Cao |
| Yêu cầu chia nhỏ task | *"Chia việc dự án này giúp tôi"* | 🟢 Cao |
| Muốn ước lượng thời gian| *"Làm cái này mất bao lâu?"* | 🟢 Cao |
| Từ khóa trực tiếp | *"lên kế hoạch", "milestone", "plan", "wbs"* | 🟢 Cao |
| Bị lầy dự án | *"Làm hoài không xong, rối quá"* | 🟡 TB |

---

## 3. Planning Pipeline (Quy trình Lên kế hoạch)

```mermaid
flowchart TD
    A[Nhận Yêu Cầu] --> B[Phân Tích Yêu Cầu MoSCoW]
    B --> C[Phân Rã Công Việc WBS]
    C --> D[Ước Lượng Thời Gian T-Shirt Sizing]
    D --> E[Lập Sơ Đồ Phụ Thuộc Dependency]
    E --> F[Lập Lịch Trình Milestone]
    F --> G[Phân Tích Rủi Ro Risk Matrix]
    G --> H[Đóng Gói & Theo Dõi Tiến Độ]
    
    style A fill:#6c63ff,color:#fff
    style H fill:#00c853,color:#fff
```

### Bước 1: Requirement Analysis (Phân Tích Yêu Cầu)
Sử dụng ma trận **MoSCoW**:
- **M - Must have:** Tính năng bắt buộc phải có để dự án (hoặc đồ án) sống được (VD: Đăng nhập, Database core).
- **S - Should have:** Tính năng quan trọng nhưng nếu không có, web/app vẫn chạy ổn định (VD: Lọc, Tìm kiếm nâng cao).
- **C - Could have:** Tính năng "nice-to-have", có thì tốt, thêm điểm (VD: Dark mode, Animation, Notification).
- **W - Won't have:** Những thứ vượt quá Scope hiện tại, bỏ qua để tránh rủi ro Scope Creep.

### Bước 2: Work Breakdown Structure (WBS)
Quy tắc chia: Không có task nào lớn hơn **8 tiếng**.
- **Epic:** Tính năng lớn (VD: Module Giỏ Hàng) (2-3 tuần)
  - **Story:** Câu chuyện người dùng (VD: User có thể thêm SP vào giỏ) (2-5 ngày)
    - **Task 1:** API Add to Cart Backend (4h)
    - **Task 2:** UI Button & Toast Frontend (2h)
    - **Task 3:** Redux/Zustand State (1h)

### Bước 3: Ước lượng Thời gian (T-Shirt Sizing)
Sử dụng Bảng Ước lượng T-Shirt:

| Size | Giờ Code (Ước tính) | Ví dụ Thực tế |
|---|---|---|
| **XS** (Extra Small) | < 1h | Sửa CSS, đổi màu, sửa text, fix typo bug |
| **S** (Small) | 1h - 2h | Thêm trường vào Form, viết 1 API đơn giản GET |
| **M** (Medium) | 3h - 5h | Làm màn hình CRUD đơn giản, viết API Auth |
| **L** (Large) | 6h - 8h | Tích hợp Stripe/VNPAY, vẽ UI phức tạp + Logic |
| **XL** (Extra Large)| > 8h | Dựng Frame Base, Xây dựng Realtime Chat → **Phải chia nhỏ** |

### Bước 4: Sơ đồ Định tuyến & Phụ thuộc (Dependency Mapping)
Sử dụng công thức DAG (Directed Acyclic Graph): Task B chỉ làm được khi Task A xong.
- VD: `[Database Schema]` ➔ `[API CRUD]` ➔ `[UI Integration]`
- Nếu UI và Backend có thể làm song song: `Mock API` ➔ `[UI Integration]` || `[API CRUD]`

### Bước 5: Đánh giá & Quản trị Rủi ro (Risk Assessment Matrix)
Đánh giá theo Xác suất (Probability) x Tác động (Impact):

| Tên Rủi Ro | Xác suất | Tác động | Plan B (Mitigation Strategy) |
|---|---|---|---|
| (Đồ án) GVHD yêu cầu đổi đề tài đột ngột | 🟡 TB | 🔴 High | Thường xuyên báo cáo tiến độ sớm (2 tuần/lần), chốt Requirement ký tên. |
| API bên thứ 3 hỏng/đổi docs (Stripe, AI) | 🟡 TB | 🔴 High | Viết Adapter Layer để dễ swap thư viện, dùng Mock Data để dev UI. |
| Không kịp Deadline bài nộp | 🟢 Low | 🔴 High | Cắt bỏ nhóm tính năng "Could Have" và "Should Have", chỉ nộp "Must Have". |
| Data bị mất, xóa nhầm DB | 🔴 High | 🔴 High | Cài Auto-Backup script, push Git liên tục, không bao giờ chmod 777 DB. |
| Cháy linh kiện (IoT / ESP32) | 🔴 High | 🔴 High | Mua dư 30% linh kiện quan trọng, dùng nguồn cấp ngoài thay vì cắm direct USB laptop. |

---

## 4. Templates Kế Hoạch 

### 4.1 TDTU 16-Week Thesis Template (Chuẩn Luận Văn)
Form lịch trình chuẩn cho sinh viên làm Đồ án / Luận văn 16 tuần:

```markdown
## 📅 Lịch Trình Đồ Án TDTU (16 Tuần)

**🏁 Phase 1: Phân tích & Blueprint (Tuần 1 - 3)**
- **Tuần 1:** (T-Shirt: M) Chốt đề tài GVHD, setup Github, Cài đặt IDE, Test Hello World.
- **Tuần 2:** (T-Shirt: L) Phân tích MoSCoW, Vẽ Sơ đồ Usecase, Class Diagram.
- **Tuần 3:** (T-Shirt: L) Thiết kế Database (ERD), Vẽ UI Wireframe Figma. Nộp Báo cáo tiến độ 1.

**⚙️ Phase 2: Core Engineering (Tuần 4 - 8)**
- **Tuần 4-5:** (T-Shirt: XL) Dựng server (NodeJS/Python) hoặc nạp firmware base (ESP32). Build DB migrations.
- **Tuần 6-7:** (T-Shirt: XL) Viết các API nền tảng "Must Have". Xử lý hardware sensors.
- **Tuần 8:** (T-Shirt: M) Tích hợp kiểm thử. Nghiệm thu giữa kỳ (Chạy được luồng cốt lõi).

**🖥️ Phase 3: UI/UX & Integration (Tuần 9 - 12)**
- **Tuần 9-10:** (T-Shirt: L) Code giao diện Frontend (dùng Framework React/Vue).
- **Tuần 11-12:** (T-Shirt: XL) Ghép API Frontend to Backend. Xử lý State, Session Auth, JWT.

**🎓 Phase 4: Polish, Fix Bug & Thesis Writing (Tuần 13 - 16)**
- **Tuần 13:** (T-Shirt: M) End-to-end Testing. Debug diện rộng. Nhờ AI Scan lỗi kiến trúc.
- **Tuần 14:** (T-Shirt: L) UI/UX Polish. Thêm Loading states, Glassmorphism, animations.
- **Tuần 15:** (T-Shirt: XL) Viết cuốn báo cáo (Dùng Smart Docs Generator - mẫu MauDATN_2021). Bổ sung tài liệu tham khảo.
- **Tuần 16:** (T-Shirt: S) Slide Defense, Rehearsal. Code Freeze.
```

### 4.2 Freelance / Agile Sprint Template 
Sử dụng cho dự án outsource hoặc startup ngắn ngày (2 tuần 1 Sprint):
- Dựa trên Sprint Backlog.
- Gắn thời gian: Ngày 1-3 (Thiết kế), Ngày 4-10 (Dev), Ngày 11-13 (Test), Ngày 14 (Showcase).

---

## 5. Output Format (Cách Khung Giới Thiệu Planning)

Bất kỳ lúc nào user yêu cầu "lên kế hoạch", hãy trả về khối Markdown này:

```markdown
## 📅 Project Plan: [Tên Dự Án]

| Metadata | Chi tiết |
| --- | --- |
| 🕒 Estimated Time | [X Giờ / Y Tuần] |
| 🎯 Project Phase | [Ví dụ: MVP, Production, Thesis] |
| 👥 Team Size | [X người] |
| 🔥 Critical Path | [Task A -> Task B -> Task C] |

### 1. MoSCoW Scope
- ✅ **Must:** [liệt kê nhanh]
- 💡 **Should:** [liệt kê nhanh]
- ❌ **Won't:** [liệt kê nhanh]

### 2. Timeline & Gantt (Sơ Đồ)
[Chèn Mermaid Gantt Chart ở đây. Ví dụ:]
` ` `mermaid
gantt
    title Roadmap
    dateFormat  YYYY-MM-DD
    section Phase 1: Setup
    Tạo Repo, Boilerplate :des1, 2026-04-20, 2d
    section Phase 2: Core
    DB & API              :des2, after des1, 5d
` ` `

### 3. Risk Mitigation
- ⚠️ Nêu 2 rủi ro chí mạng kèm giải pháp.

👉 **Review Kế hoạch**: Bạn đồng ý với Timeline này chứ? Nếu OK, chúng ta bắt đầu vào Task đầu tiên!
```

---

## 6. Definition of Done (Khái niệm Hoàn Thành)
AI không bao giờ được chuyển Task nếu chưa đạt 8 tiêu chí DoD này:
1. Có Code base chạy được.
2. Code đã pass Lint / Type checker.
3. Không có console warnings hoặc deprecation notices.
4. Tính năng chính hoạt động trơn tru lúc test tay (Happy Path).
5. Handle tối thiểu 2 Edge Cases (Sai pass, Bấm nút nhiều lần).
6. Document (JSDoc) cho các hàm Public.
7. Đã commit code lên Git (nếu user yêu cầu tự quản lý code).
8. Cập nhật Jira / Trello / File To-Do markdown.

---

## 7. Adaptive Behavior (Tự Thích Nghi)

| Ngữ cảnh User | Hành vi của Planner AI |
|---|---|
| Báo "Dự án nhỏ, 1 ngày làm xong" | Skip Gantt + MoSCoW. Áp dụng luôn Checklist To-Do phẳng. |
| Báo "Có team 3 người" | Thêm phần Resource Allocation: Phân chia rõ Ai làm Frontend, Ai Backend. |
| Báo "Làm kiếm tiền outsource" | Gắn milestone payment % vào kế hoạch. Gợi ý làm Phase thanh toán. |
| User nói "Trễ deadline rồi" | Bật "Rescue Mode": Drop Should/Could Have. Chỉ lên list Must Have cốt lõi nhất. |
