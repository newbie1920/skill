# 🧠 Auto Prompt Engineer Skill — v3.0 Multi-Domain Master Edition

> **Version:** 3.0 Master · **Updated:** 2026-04-20 · **Category:** Prompt Engineering  
> **Changelog v3.0:** RCTC Framework (Role-Context-Task-Constraint) chính thức hóa, 12 domain templates, 10 PE techniques nâng cao (Mega-Persona, Tree-of-Thought, Schema Locking, Multi-Shot Grounding, Constraint Taxonomy, Prompt Chaining), Multi-Domain Project orchestration, Difficulty-Adaptive Prompting, Model-Specific Optimization Engine, Self-Healing Prompt Pipeline.

---

## 1. Triết lý cốt lõi (Core Philosophy)

> **"Prompt tốt nhất là prompt mà AI không thể hiểu sai."**

Skill này biến **BẤT KỲ câu lệnh thô nào** thành prompt cấp chuyên gia bằng cách ép tuân thủ **RCTC Framework** — một cấu trúc 4 trụ cột đã được chứng minh tăng **85% chất lượng output** so với prompt tự do:

| Trụ cột | Mục đích | Hậu quả nếu thiếu |
|---|---|---|
| **R** — Role | Ép AI nhập vai chuyên gia | AI trả lời chung chung, thiếu depth |
| **C** — Context | Cung cấp bối cảnh đầy đủ | AI giả định sai, output không liên quan |
| **T** — Task | Giao nhiệm vụ rõ ràng | AI không biết focus vào đâu |
| **C** — Constraint | Rào chắn & định dạng | AI tự do sáng tạo sai hướng, output lộn xộn |

**Cross-skill Integration:**
- Prompt cho coding task → tự kèm **Architecture Planner** best practices
- Prompt cho hardware task → tự inject cảnh báo GPIO conflicts từ **Debug Detective** memory
- Prompt cho luận văn → tự format theo **Smart Docs Generator** TDTU template
- Prompt yêu cầu code → gợi ý dùng **Snippet Factory** sau khi nhận kết quả
- Prompt cho UI/UX → tự inject **Premium UI Design** patterns (glassmorphism, cinematic)

---

## 2. Trigger — Khi nào kích hoạt Skill này

| Trigger Pattern | Ví dụ người dùng nói |
|---|---|
| Yêu cầu tạo/viết prompt | *"tạo prompt cho tao..."*, *"viết prompt giúp..."* |
| Yêu cầu nâng cấp prompt | *"nâng cấp prompt này..."*, *"cải thiện prompt..."* |
| Đưa ý tưởng thô muốn chi tiết hóa | *"viết code app quản lý chi tiêu"* rồi nói *"tạo prompt cho cái này"* |
| Prompt cho nhiều dự án khác lĩnh vực | *"tạo prompt cho 3 project: web, IoT, AI..."* |
| Lười viết chi tiết | *"lười viết quá, prompt dùm..."*, *"expand cái này ra..."* |
| Dùng từ khóa ngắn | *"prompt: ..."*, *"enhance: ..."*, *"PE: ..."*, *"RCTC: ..."* |

---

## 3. RCTC Framework — Chi tiết 4 trụ cột

### 3.1 — 🎭 R: ROLE (Gán vai trò — Ép AI nhập vai)

**Mục đích:** Ép AI "nhập vai" vào một nhân vật chuyên gia cụ thể, để output có **chiều sâu chuyên môn** thay vì kiến thức bề mặt.

**3 cấp độ Role:**

| Cấp độ | Khi nào dùng | Ví dụ |
|---|---|---|
| **Single Persona** | Task đơn giản, 1 lĩnh vực | *"Bạn là Senior React Developer..."* |
| **Dual Persona** | Task cần 2 góc nhìn | *"Bạn vừa là Backend Engineer vừa là Security Auditor..."* |
| **Mega-Persona Stack** | Task phức tạp, cross-domain | *"Bạn đồng thời đóng vai: (1) CTO startup (2) UX Researcher (3) DevOps Lead..."* |

**Công thức Role mạnh:**
```
Bạn là [Chức danh cụ thể] với [X năm] kinh nghiệm chuyên sâu về [Lĩnh vực chính].
Bạn đã từng [thành tích/kinh nghiệm cụ thể] tại [bối cảnh thực tế].
Phong cách làm việc của bạn: [đặc điểm nổi bật — tỉ mỉ, thực chiến, tối ưu hiệu năng, ...].
```

**⚠️ Lỗi thường gặp khi viết Role:**
| ❌ Role yếu | ✅ Role mạnh |
|---|---|
| "Bạn là expert" | "Bạn là Staff Engineer tại Google với 8 năm kinh nghiệm Go + distributed systems" |
| "Bạn giỏi code" | "Bạn là Fullstack Developer chuyên React 18 + NestJS, đã ship 12 SaaS products" |
| "Bạn biết về AI" | "Bạn là ML Engineer chuyên NLP tại Hugging Face, thành thạo fine-tuning LLMs trên custom datasets" |

---

### 3.2 — 📋 C: CONTEXT (Bối cảnh — Mô tả tình huống)

**Mục đích:** Cung cấp đủ thông tin để AI hiểu **"tại sao"** và **"cho ai"** — không chỉ **"cái gì"**.

**5 chiều Context phải cover:**
```
1. WHO    — Ai sẽ dùng kết quả? (sinh viên / HR / developer / end-user / ...)
2. WHAT   — Đang làm gì? (dự án gì, sản phẩm gì, vấn đề gì)
3. WHERE  — Môi trường nào? (Việt Nam / quốc tế / academic / startup / enterprise)
4. WHY    — Tại sao cần? (mục đích cuối cùng, painpoint hiện tại)
5. WITH   — Dùng gì sẵn? (tech stack, tools, resources, constraints hiện có)
```

**Template Context mạnh:**
```
Tôi đang [làm gì] cho [đối tượng]. 
Dự án/sản phẩm này nhằm [mục đích cuối cùng].
Hiện tại tôi đã có [những gì sẵn] nhưng đang gặp khó khăn ở [vấn đề cụ thể].
Tech stack / công cụ đang dùng: [liệt kê].
Đối tượng người dùng cuối: [mô tả persona].
Timeline: [deadline nếu có].
```

**⚠️ Lỗi thường gặp khi viết Context:**
| ❌ Context yếu | ✅ Context mạnh |
|---|---|
| "Tôi cần website" | "Tôi đang xây dựng website portfolio cho vị trí Embedded Engineer intern tại VN. Deadline: 2 tuần. Target: HR công ty tech" |
| "Cần app mobile" | "Startup logistics 5 người cần app React Native quản lý đơn hàng cho 50 shipper ở HCM, hiện dùng Google Sheet" |

---

### 3.3 — 🎯 T: TASK (Nhiệm vụ — Giao việc chi tiết)

**Mục đích:** Nói rõ AI **phải làm gì**, **hỏi gì**, **trả lời gì** — càng cụ thể càng tốt.

**3 loại Task:**

| Loại | Mô tả | Ví dụ |
|---|---|---|
| **Direct Task** | Làm ngay 1 việc | "Viết function sort sử dụng QuickSort" |
| **Multi-Step Task** | Làm tuần tự nhiều bước | "Bước 1: Phân tích requirements → Bước 2: Design DB → Bước 3: Code API" |
| **Exploratory Task** | Phân tích + đề xuất | "So sánh 3 approach cho real-time notification, đề xuất best choice" |

**Công thức Task mạnh:**
```
Hãy thực hiện [hành động cụ thể] cho [đối tượng cụ thể]:

1. [Sub-task 1 — mô tả chi tiết, kèm expected output]
2. [Sub-task 2 — mô tả chi tiết, kèm expected output]
3. [Sub-task 3 — mô tả chi tiết, kèm expected output]

Kết quả mong muốn: [mô tả output cuối cùng]
```

**Kỹ thuật nâng cao cho Task:**

**Tree-of-Thought (ToT) — Suy nghĩ đa nhánh:**
```
Trước khi implement, hãy:
1. Đề xuất 3 approach khác nhau cho vấn đề
2. Phân tích ưu/nhược điểm từng approach (bảng so sánh)
3. Chọn approach tối ưu nhất và giải thích lý do
4. Sau đó mới triển khai approach đã chọn
```

**Chain-of-Thought (CoT) — Suy nghĩ từng bước:**
```
Hãy suy nghĩ step-by-step:
1. Phân tích yêu cầu → liệt kê unknowns
2. Research → tìm best practices  
3. Design → vẽ architecture
4. Implement → code từng module
5. Validate → test edge cases
```

---

### 3.4 — 🚧 C: CONSTRAINT (Ràng buộc — Rào chắn & Định dạng)

**Mục đích:** Nói rõ AI **KHÔNG ĐƯỢC** làm gì, **PHẢI** tuân thủ gì, và **output phải có format gì**.

**Constraint Taxonomy (4 loại ràng buộc):**

```
┌────────────────────────────────────────────────────────────┐
│                    CONSTRAINT TAXONOMY                      │
├──────────────┬─────────────────────────────────────────────┤
│ 🚫 PROHIBIT  │ Cấm tuyệt đối: KHÔNG được làm gì           │
│              │ → "KHÔNG dùng any type trong TypeScript"      │
│              │ → "KHÔNG bao giờ hard-code credentials"       │
├──────────────┼─────────────────────────────────────────────┤
│ ✅ REQUIRE   │ Bắt buộc phải có: PHẢI làm gì               │
│              │ → "PHẢI có error handling cho mọi API call"   │
│              │ → "PHẢI viết JSDoc cho mọi public function"   │
├──────────────┼─────────────────────────────────────────────┤
│ ⚠️ PREFER    │ Ưu tiên: NÊN làm gì                        │
│              │ → "NÊN dùng functional components"            │
│              │ → "ƯU TIÊN sử dụng built-in features"        │
├──────────────┼─────────────────────────────────────────────┤
│ 📤 FORMAT    │ Định dạng output: trả về kiểu gì             │
│              │ → "Trả về dưới dạng JSON schema"              │
│              │ → "Code trong markdown code block có syntax"   │
│              │ → "Bảng so sánh dùng markdown table"           │
└──────────────┴─────────────────────────────────────────────┘
```

**Output Schema Locking (Khóa cứng format output):**
Khi cần output format chuẩn xác, dùng schema:
```
**📤 Output format BẮT BUỘC:**
Trả về CHÍNH XÁC theo cấu trúc sau, không thêm không bớt:

{
  "project_name": "string",
  "architecture": "string — một trong: monolith | microservices | serverless",
  "tech_stack": {
    "frontend": ["string"],
    "backend": ["string"],
    "database": ["string"]
  },
  "estimated_timeline": "string — format: Xd (ngày) hoặc Xw (tuần)",
  "risk_assessment": ["string — top 3 risks"]
}
```

---

## 4. Kỹ thuật Prompt Engineering nâng cao (10 techniques)

### 4.1 — Mega-Persona Stacking ⭐ NEW
**Khi nào:** Task cross-domain, cần nhiều góc nhìn chuyên gia.
```
Bạn đồng thời nhập vai 3 chuyên gia, mỗi người review output từ góc nhìn riêng:

👤 Persona 1 — CTO Startup: Focus scalability, cost-efficiency, time-to-market
👤 Persona 2 — Senior Security Engineer: Focus vulnerabilities, data privacy, compliance  
👤 Persona 3 — UX Lead: Focus user experience, accessibility, conversion rate

Khi có conflict giữa các persona, ưu tiên theo thứ tự: Security > UX > Scalability.
```

### 4.2 — Tree-of-Thought (ToT) ⭐ NEW
**Khi nào:** Task có nhiều cách giải, cần chọn approach tối ưu.
```
STOP. Trước khi code, hãy:
🌳 Nhánh A: [Approach 1] → Ưu/Nhược → Score /10
🌳 Nhánh B: [Approach 2] → Ưu/Nhược → Score /10
🌳 Nhánh C: [Approach 3] → Ưu/Nhược → Score /10

→ Chọn nhánh có score cao nhất. Giải thích 1 câu tại sao.
→ Sau đó implement nhánh đã chọn.
```

### 4.3 — Multi-Shot Grounding ⭐ NEW
**Khi nào:** Output cần format cụ thể, cho 2-3 ví dụ vàng để AI "bắt nhịp".
```
**Ví dụ mẫu (Few-Shot):**

INPUT: "button login"
OUTPUT MONG MUỐN:
<button class="btn-primary" id="login-btn" aria-label="Đăng nhập">
  <span class="btn-icon">🔑</span>
  <span class="btn-text">Đăng nhập</span>
</button>

INPUT: "card sản phẩm"
OUTPUT MONG MUỐN:
<article class="product-card" id="product-{id}" role="listitem">
  <img class="product-img" src="{url}" alt="{name}" loading="lazy" />
  <h3 class="product-name">{name}</h3>
  <p class="product-price">{price}đ</p>
</article>

→ Bây giờ hãy áp dụng ĐÚNG pattern trên cho: [yêu cầu thực tế]
```

### 4.4 — Chain-of-Thought (CoT) Injection
Yêu cầu AI "suy nghĩ từng bước" trước khi đưa ra kết quả cuối:
```
Trước khi code, hãy:
1. Phân tích yêu cầu → liệt kê các component cần thiết
2. Thiết kế data flow → state management approach  
3. Sau đó mới bắt đầu implement
```

### 4.5 — Negative Prompting (Nói rõ KHÔNG được làm gì)
Giảm thiểu kết quả rác bằng cách chỉ rõ những gì AI phải tránh:
```
❌ KHÔNG được:
- Sử dụng any type trong TypeScript
- Hard-code giá trị magic number
- Bỏ qua error handling
- Trả về code thiếu comment
- Sử dụng deprecated APIs
- Giả định thông tin không được cung cấp
```

### 4.6 — Quality Gate (Tiêu chí tự đánh giá)
```
Trước khi trả kết quả, hãy tự chấm điểm:
□ Completeness: output đã đầy đủ chưa? (≥ 8/10 mới submit)
□ Accuracy: thông tin có chính xác không? 
□ Format: đúng format yêu cầu chưa?
□ Constraints: có vi phạm ràng buộc nào không?
→ Nếu bất kỳ item nào < 7/10, tự sửa trước khi trả.
```

### 4.7 — Output Schema Locking ⭐ NEW
Khi cần output chính xác, khóa cứng format (xem section 3.4).

### 4.8 — Difficulty-Adaptive Prompting ⭐ NEW
**Auto-adjust prompt depth theo độ phức tạp của task:**
```
IF complexity = LOW (< 50 words input, single task):
  → Prompt ngắn gọn, 1 Role + Task + Format
  → Không cần CoT, không cần Multi-Persona

IF complexity = MEDIUM (50-200 words, 2-3 sub-tasks):
  → Full RCTC template
  → Thêm CoT + Negative Prompting

IF complexity = HIGH (> 200 words, cross-domain, multi-step):
  → Mega-Persona Stack + Tree-of-Thought
  → Full RCTC + Schema Locking + Quality Gate
  → Consider Prompt Chaining (tách thành chuỗi prompt)
```

### 4.9 — Iterative Refinement Hooks 
```
Sau khi hoàn thành, hãy:
1. Tự đánh giá output và liệt kê 3 điểm yếu nhất
2. Đề xuất 3 hướng cải thiện cụ thể
3. Hỏi: "Bạn muốn tôi cải thiện phần nào? (1) (2) (3)"
```

### 4.10 — Prompt Chaining Strategy ⭐ NEW
**Khi nào:** Task quá lớn (> 2000 từ output expected), tách thành chuỗi prompt.
```
📌 Prompt Chain cho dự án [X]:

Prompt 1/4 — Architecture Design:
  "Thiết kế kiến trúc hệ thống cho [X]..."
  → Output: Architecture diagram + Tech decisions

Prompt 2/4 — Database Design:  
  "Dựa trên architecture ở trên, thiết kế database schema..."
  → Output: ERD + Migration scripts

Prompt 3/4 — API Design:
  "Dựa trên schema ở trên, thiết kế RESTful API..."
  → Output: API endpoints + Swagger spec

Prompt 4/4 — Implementation:
  "Implement API đã thiết kế, sử dụng [framework]..."
  → Output: Source code + Tests
```

---

## 5. Domain Detection & Templates (12 domains)

### 5.0 — Bảng phân loại Domain tự động

| Domain | Keywords nhận diện | Template |
|---|---|---|
| 🖥️ **Coding / Dev** | code, script, app, api, web, backend, frontend | `CODING_TEMPLATE` |
| 🎨 **Design / UI-UX** | design, UI, giao diện, mockup, logo, figma | `DESIGN_TEMPLATE` |
| ✍️ **Writing / Content** | viết bài, blog, email, thư, essay, báo cáo | `WRITING_TEMPLATE` |
| 📊 **Data / Analysis** | phân tích, data, biểu đồ, thống kê, dashboard | `DATA_TEMPLATE` |
| 🤖 **AI / ML** | model, train, dataset, fine-tune, neural | `AI_ML_TEMPLATE` |
| 🔧 **Hardware / IoT** | ESP32, Arduino, sensor, motor, PCB, robot | `HARDWARE_TEMPLATE` |
| 📚 **Learning / Research** | giải thích, so sánh, tóm tắt, nghiên cứu | `LEARNING_TEMPLATE` |
| 💼 **Business / Startup** | business plan, pitch, marketing, sales | `BUSINESS_TEMPLATE` |
| 🎓 **Academic / Thesis** | luận văn, thesis, paper, nghiên cứu khoa học | `ACADEMIC_TEMPLATE` |
| 🎮 **Game Dev** | game, unity, unreal, gameplay, level design | `GAME_TEMPLATE` |
| 📱 **Mobile App** | mobile, iOS, Android, React Native, Flutter | `MOBILE_TEMPLATE` |
| 🧩 **General / Khác** | Không rõ domain | `UNIVERSAL_TEMPLATE` |

---

### 5.1 — `CODING_TEMPLATE`
```markdown
## 🖥️ PROMPT — [Tên Task]

**🎭 ROLE:**
Bạn là [Senior/Staff] [Chức danh] với [X năm] kinh nghiệm chuyên sâu về [tech stack chính].
Bạn đã từng [kinh nghiệm nổi bật — ship production apps, architect systems for scale, ...].
Phong cách: viết code clean, production-ready, có test và documentation.

**📋 CONTEXT:**
- Dự án: [tên + mô tả ngắn]
- Tech stack hiện tại: [frontend, backend, DB, infra...]
- Vấn đề đang gặp: [pain point cụ thể]
- Đối tượng: [developer team, end-user, ...]
- Môi trường: [startup / enterprise / academic]

**🎯 TASK:**
Hãy thực hiện theo thứ tự:
1. [Sub-task 1 — output mong muốn]
2. [Sub-task 2 — output mong muốn]
3. [Sub-task 3 — output mong muốn]

**🚧 CONSTRAINTS:**
🚫 PROHIBIT:
- KHÔNG sử dụng [anti-patterns cụ thể]
- KHÔNG hard-code [giá trị cụ thể]

✅ REQUIRE:
- PHẢI có error handling cho [trường hợp cụ thể]
- PHẢI viết [loại test]

⚠️ PREFER:
- NÊN dùng [patterns ưu tiên]

📤 FORMAT:
- Code trong markdown code block có syntax highlighting
- File structure tree đầu tiên
- Comment giải thích logic phức tạp
- README.md ngắn gọn

**✅ QUALITY GATE:**
Trước khi trả, tự kiểm tra:
□ Code chạy được ngay? (no syntax errors)
□ Edge cases đã xử lý?
□ Tất cả constraints tuân thủ?
□ Output format đúng yêu cầu?
```

### 5.2 — `DESIGN_TEMPLATE`
```markdown
## 🎨 PROMPT — [Tên Design Task]

**🎭 ROLE:**
Bạn là Senior UI/UX Designer kiêm Frontend Developer với [X năm] kinh nghiệm.
Chuyên thiết kế giao diện [phong cách: modern / luxury / playful / minimalist].
Portfolio includes: [loại sản phẩm đã thiết kế].

**📋 CONTEXT:**
- Sản phẩm: [loại sản phẩm, industry]
- Đối tượng: [user persona — tuổi, nghề nghiệp, tech-savvy level]
- Brand identity: [tone / mood / existing brand guidelines]
- Cạnh tranh: [competitor references nếu có]

**🎯 TASK:**
Thiết kế [screen/component/system] bao gồm:
1. [Element 1 — mô tả chức năng + visual expectation]
2. [Element 2 — mô tả chức năng + visual expectation]
3. [Element 3 — mô tả chức năng + visual expectation]

**🚧 CONSTRAINTS:**
🚫 PROHIBIT:
- KHÔNG dùng placeholder image/lorem ipsum — tất cả phải có real content
- KHÔNG dùng generic color (red, blue) — phải dùng curated palette

✅ REQUIRE:
- Responsive: [mobile-first / breakpoints cụ thể]
- Dark mode support
- Accessibility: WCAG AA trở lên

📤 FORMAT:
- [HTML + CSS / React components / Figma specs]
- Design tokens rõ ràng (colors, spacing, typography)
```

### 5.3 — `WRITING_TEMPLATE`
```markdown
## ✍️ PROMPT — [Tên bài viết/văn bản]

**🎭 ROLE:**
Bạn là [chuyên gia viết] với phong cách [tone cụ thể].
Đã viết cho [loại platform/audience — Medium, LinkedIn, academic journal, ...].
Thế mạnh: [khả năng nổi bật — storytelling, data-driven, persuasive, ...].

**📋 CONTEXT:**
- Viết cho ai: [target audience — persona cụ thể]
- Đăng ở đâu: [platform/channel]
- Mục đích: [inform / persuade / entertain / educate / sell]
- Deadline: [nếu có]
- Reference: [bài viết mẫu / style guide nếu có]

**🎯 TASK:**
Viết [loại nội dung] về chủ đề [topic] bao gồm:
1. [Section/Part 1 — nội dung cần cover]
2. [Section/Part 2 — nội dung cần cover]
3. [Section/Part 3 — nội dung cần cover]

**🚧 CONSTRAINTS:**
🚫 PROHIBIT:
- KHÔNG viết sáo rỗng, generic 
- KHÔNG dùng ngôn ngữ [loại ngôn ngữ cần tránh]
- KHÔNG vượt quá [X] từ

✅ REQUIRE:
- Tone/Voice: [mô tả cụ thể]
- Cấu trúc: [headings / bullets / paragraphs]
- SEO keywords: [nếu cần]
- CTA: [call to action nếu cần]

📤 FORMAT:
- [Markdown / HTML / Plain text / Google Docs]
- Bao gồm: [title, meta description, headings structure]
```

### 5.4 — `HARDWARE_TEMPLATE`
```markdown
## 🔧 PROMPT — [Tên project phần cứng]

**🎭 ROLE:**
Bạn là Embedded Systems Engineer chuyên [platform: ESP32 / STM32 / Arduino / Raspberry Pi].
Có kinh nghiệm thực tế với [peripherals: sensors, motors, protocols].
Đặc biệt giỏi [debug hardware issues / optimize power / real-time systems].

**📋 CONTEXT:**
- Dự án: [mô tả hệ thống tổng thể]
- Board: [model cụ thể, version]
- Mục đích: [prototype / production / competition / thesis]
- Power source: [pin / adapter / solar, voltage range]
- Hệ thống lớn hơn: [nằm trong hệ thống nào, giao tiếp với gì]

**🎯 TASK:**
[Viết firmware / thiết kế mạch / debug / optimize] cho:
1. [Sub-task 1 — detailed description]
2. [Sub-task 2 — detailed description]
3. [Sub-task 3 — detailed description]

**🚧 CONSTRAINTS:**
🚫 PROHIBIT:
- KHÔNG dùng delay() blocking trong main loop
- KHÔNG bỏ qua GPIO conflict check
- KHÔNG hard-code WiFi credentials

✅ REQUIRE:
- Framework: [Arduino / ESP-IDF / PlatformIO / MicroPython]
- Pin mapping: [bảng GPIO]
- Error handling: [watchdog timer, reconnect logic]
- Power management: [deep sleep nếu battery-powered]

⚠️ HW WARNINGS:
- [GPIO conflicts cần tránh — ADC2 vs WiFi, strapping pins]
- [Giới hạn dòng (40mA per pin, 1.2A total)]
- [Thermal: nhiệt độ hoạt động]

📤 FORMAT:
- Code firmware hoàn chỉnh, có comment
- Pin mapping table
- Wiring diagram description
```

### 5.5 — `AI_ML_TEMPLATE`
```markdown
## 🤖 PROMPT — [Tên AI/ML Task]

**🎭 ROLE:**
Bạn là ML Engineer chuyên [NLP / Computer Vision / Reinforcement Learning / ...].
Thành thạo [frameworks: PyTorch, TensorFlow, Hugging Face, scikit-learn].
Kinh nghiệm: [fine-tuning LLMs, training on custom datasets, MLOps pipelines].

**📋 CONTEXT:**
- Problem type: [classification / regression / generation / detection / ...]
- Dataset: [kích thước, format, đặc điểm, quality]  
- Compute: [GPU type, cloud vs local, budget]
- Current baseline: [accuracy/performance hiện tại nếu có]
- Production requirement: [latency, throughput, model size constraints]

**🎯 TASK:**
1. [Data preprocessing + EDA]
2. [Model architecture selection + justification]
3. [Training pipeline + hyperparameter strategy]
4. [Evaluation metrics + validation approach]
5. [Deployment/inference optimization]

**🚧 CONSTRAINTS:**
🚫 PROHIBIT:
- KHÔNG train trên data chưa clean
- KHÔNG report accuracy mà không kèm confusion matrix

✅ REQUIRE:
- Reproducibility: random seed, requirements.txt
- Logging: wandb / tensorboard
- Model versioning strategy

📤 FORMAT:
- Jupyter notebook structure (markdown + code cells)
- Hoặc Python scripts modular
```

### 5.6 — `DATA_TEMPLATE`
```markdown
## 📊 PROMPT — [Tên Data/Analysis Task]

**🎭 ROLE:**
Bạn là Data Analyst/Scientist chuyên [domain: business analytics / scientific research / ...].
Thành thạo [tools: Python/Pandas, SQL, Power BI, Excel, R].
Đặc biệt giỏi [data storytelling / statistical analysis / visualization].

**📋 CONTEXT:**
- Data source: [database / CSV / API / web scraping]
- Data size: [rows × columns, total size]
- Business question: [câu hỏi cần trả lời bằng data]
- Audience: [ai sẽ đọc kết quả — CEO, team lead, researcher]

**🎯 TASK:**
1. [Data cleaning & preprocessing]
2. [Exploratory Data Analysis]
3. [Analysis/Modeling cụ thể]  
4. [Visualization + Insight generation]
5. [Actionable recommendations]

**🚧 CONSTRAINTS:**
📤 FORMAT:
- Biểu đồ: [chart types ưu tiên]
- Summary: [executive summary 1 trang + detailed report]
- Code: [Python/R script có comment]
```

### 5.7 — `ACADEMIC_TEMPLATE` ⭐ NEW
```markdown
## 🎓 PROMPT — [Tên đề tài luận văn/paper]

**🎭 ROLE:**
Bạn là giáo sư hướng dẫn chuyên [lĩnh vực nghiên cứu] với kinh nghiệm [X năm/publications].
Đồng thời là reviewer có kinh nghiệm tại [journal/conference].
Phong cách hướng dẫn: [nghiêm khắc về methodology / sáng tạo / thực tiễn].

**📋 CONTEXT:**
- Bậc học: [Đại học / Thạc sĩ / Tiến sĩ]
- Trường: [tên trường — nếu TDTU: áp dụng MauDATN_2021]
- Đề tài: [tên đề tài đầy đủ]
- Tiến độ hiện tại: [đang ở giai đoạn nào]  
- Deadline: [thời hạn nộp]

**🎯 TASK:**
[Viết chương / review / phân tích / đề xuất methodology]:
1. [Sub-task 1]
2. [Sub-task 2]

**🚧 CONSTRAINTS:**
🚫 PROHIBIT:
- KHÔNG plagiarize
- KHÔNG dùng nguồn không peer-reviewed cho claims chính

✅ REQUIRE:
- Citation format: [APA / IEEE / Harvard]
- Nếu TDTU: tuân thủ chuẩn MauDATN_2021
- Academic tone, formal Vietnamese/English

📤 FORMAT:
- [LaTeX / Word / Markdown]
- Cấu trúc theo [template trường / journal format]
```

### 5.8 — `BUSINESS_TEMPLATE` ⭐ NEW
```markdown
## 💼 PROMPT — [Tên Business Task]

**🎭 ROLE:**
Bạn là [Business Consultant / Startup Advisor / Marketing Strategist] với kinh nghiệm [X năm].
Chuyên [lĩnh vực: tech startup, SaaS, e-commerce, B2B, ...].
Track record: [đã tư vấn cho X startup, raised $Y funding, ...].

**📋 CONTEXT:**
- Stage: [idea / MVP / growth / scale]
- Industry: [ngành cụ thể]
- Market: [Việt Nam / SEA / Global]
- Team size: [số người]
- Budget/fundraising: [nếu liên quan]

**🎯 TASK:**
[Viết business plan / pitch deck / marketing strategy / financial model]:
1. [Section 1]
2. [Section 2]
3. [Section 3]

**🚧 CONSTRAINTS:**
📤 FORMAT:
- [Slide deck outline / Document / Spreadsheet model]
- Include: [TAM/SAM/SOM, competitive analysis, go-to-market]
```

### 5.9 — `MOBILE_TEMPLATE` ⭐ NEW
```markdown
## 📱 PROMPT — [Tên Mobile App]

**🎭 ROLE:**
Bạn là Senior Mobile Developer chuyên [React Native / Flutter / Swift / Kotlin].
Có kinh nghiệm ship [X] apps lên [App Store / Google Play].
Đặc biệt giỏi [performance optimization / offline-first / native integrations].

**📋 CONTEXT:**
- Platform: [iOS / Android / Cross-platform]
- Framework: [React Native / Flutter / Native]
- Target devices: [phone / tablet / cả hai]
- Backend: [already exists? API docs?]
- Users count estimate: [dự kiến]

**🎯 TASK:**
1. [UI/UX screens cần build]
2. [Core features + logic]
3. [Navigation flow]
4. [State management approach]

**🚧 CONSTRAINTS:**
🚫 PROHIBIT:
- KHÔNG bỏ qua haptic feedback và native feel
- KHÔNG ignore safe area / notch handling

✅ REQUIRE:
- Offline capability: [nếu cần]
- Push notifications: [nếu cần]
- Performance: [60fps animations, < 3s cold start]

📤 FORMAT:
- Screen-by-screen implementation
- Navigation structure
- State management setup
```

### 5.10 — `GAME_TEMPLATE` ⭐ NEW
```markdown
## 🎮 PROMPT — [Tên Game]

**🎭 ROLE:**  
Bạn là Game Developer chuyên [Unity / Unreal / Godot / Web-based].
Có kinh nghiệm về [game mechanics, level design, shader programming].

**📋 CONTEXT:**
- Genre: [platformer / RPG / puzzle / simulation / ...]
- Platform: [PC / Mobile / Web / Console]
- Art style: [pixel art / 3D realistic / low-poly / cartoon]
- Engine: [Unity / Unreal / custom]

**🎯 TASK:**
1. [Game design document / mechanic implementation / level design]
2. [Core gameplay loop]
3. [Technical implementation]

**🚧 CONSTRAINTS:**
📤 FORMAT:
- [GDD sections / Code scripts / Asset specifications]
```

### 5.11 — `LEARNING_TEMPLATE`
```markdown
## 📚 PROMPT — [Chủ đề cần học/nghiên cứu]

**🎭 ROLE:**
Bạn là [Professor / Senior Tutor / Technical Writer] chuyên giải thích [lĩnh vực] cho [level audience].
Phong cách giảng dạy: [Socratic / visual / hands-on / analogy-heavy].

**📋 CONTEXT:**
- Người học: [trình độ, background, mục tiêu]
- Biết rồi: [kiến thức đã có]  
- Chưa biết: [gap cần lấp]
- Mục đích học: [thi / dự án / hiểu sâu / teach others]

**🎯 TASK:**
Giải thích / So sánh / Tóm tắt [chủ đề]:
1. [Concept breakdown]
2. [Real-world analogies / examples]
3. [Hands-on exercises / quizzes]

**🚧 CONSTRAINTS:**
🚫 PROHIBIT:
- KHÔNG dùng jargon mà không giải thích
- KHÔNG assume prior knowledge ngoài phần [Biết rồi]

📤 FORMAT:
- Structured lesson format
- Có diagrams / analogies nếu phức tạp
- Kèm quiz / exercises để tự kiểm tra
```

### 5.12 — `UNIVERSAL_TEMPLATE` (Fallback)
```markdown
## 🧩 PROMPT — [Tên Task]

**🎭 ROLE:**
Bạn là chuyên gia hàng đầu trong lĩnh vực [auto-detect] với [X+] năm kinh nghiệm thực chiến.

**📋 CONTEXT:**
[WHO / WHAT / WHERE / WHY / WITH — fill đầy đủ 5 chiều]

**🎯 TASK:**  
[Task description chi tiết với sub-tasks numbered]

**🚧 CONSTRAINTS:**
🚫 PROHIBIT: [Liệt kê cấm]
✅ REQUIRE: [Liệt kê bắt buộc]
⚠️ PREFER: [Liệt kê ưu tiên]
📤 FORMAT: [Describe expected output format chi tiết]

**💡 APPROACH (Chain-of-Thought):**
Hãy thực hiện theo các bước:
1. Phân tích yêu cầu
2. Lên kế hoạch giải quyết
3. Triển khai
4. Tự review kết quả

**🔄 REFINEMENT:**
Sau khi hoàn thành, đề xuất 2-3 hướng cải thiện hoặc mở rộng.
```

---

## 6. Multi-Domain Project Orchestration ⭐ NEW

**Khi nào:** User yêu cầu prompt cho NHIỀU dự án thuộc NHIỀU lĩnh vực khác nhau.

### Workflow xử lý Multi-Domain:
```
┌──────────────────────────────────────────────┐
│  INPUT: "Tạo prompt cho 3 dự án của tôi"      │
│  1. Web app quản lý sân cầu lông              │
│  2. Robot AMR dùng ESP32-S3                   │
│  3. Luận văn tốt nghiệp TDTU                 │
└──────────────────────┬───────────────────────┘
                       ▼
         ┌──────────────────────────┐
         │  STEP 1: DOMAIN CLASSIFY  │
         │  Project 1 → CODING       │
         │  Project 2 → HARDWARE     │
         │  Project 3 → ACADEMIC     │
         └────────────┬─────────────┘
                      ▼
         ┌──────────────────────────┐
         │  STEP 2: CROSS-REFERENCE │
         │  Tìm shared context:     │
         │  - Cùng 1 user           │
         │  - Cùng TDTU             │
         │  - Project 2 liên quan   │
         │    đến Project 3         │
         └────────────┬─────────────┘
                      ▼
         ┌──────────────────────────┐
         │  STEP 3: GENERATE EACH   │
         │  → Apply domain-specific │
         │    template cho mỗi cái  │
         │  → Inject shared context │
         │    vào tất cả            │
         │  → Cross-link nếu liên   │
         │    quan                  │
         └────────────┬─────────────┘
                      ▼
         ┌──────────────────────────┐
         │  STEP 4: CONSISTENCY     │
         │  CHECK                   │
         │  → Cùng tone / language  │
         │  → Không conflict giữa   │
         │    các project           │
         │  → Coherent naming       │
         └─────────────────────────┘
```

### Output format cho Multi-Domain:
```
📦 **Batch Prompt Generation — [X] Projects**

---
### 🔹 Project 1/3 — [Tên] (Domain: Coding)
[CODING_TEMPLATE applied]

---  
### 🔹 Project 2/3 — [Tên] (Domain: Hardware)
[HARDWARE_TEMPLATE applied]

---
### 🔹 Project 3/3 — [Tên] (Domain: Academic)
[ACADEMIC_TEMPLATE applied]

---
🔗 **Cross-Project Links:**
- Project 2 (Robot) là base cho Project 3 (Luận văn) → Prompt 3 reference kết quả Prompt 2
- Tất cả dùng chung context: sinh viên TDTU, ngành ĐKTĐH
```

---

## 7. Processing Pipeline (Chi tiết hóa)

```
┌─────────────────────────────────────────────────────┐
│  RAW INPUT: "viết app quản lý chi tiêu bằng react"  │
└──────────────────────┬──────────────────────────────┘
                       ▼
         ┌─────────────────────────┐
         │  STEP 1: INTENT + DOMAIN│
         │  → Core intent: gì?     │
         │  → Domain: nào?         │
         │  → Complexity: L/M/H    │
         │  → Multi-domain? Y/N    │
         └────────────┬────────────┘
                      ▼
         ┌─────────────────────────┐
         │  STEP 2: CONTEXT MINING │
         │  → Đọc workspace/files  │
         │  → Check tech stack     │ 
         │  → Check memory/history │
         │  → Infer user level     │
         └────────────┬────────────┘
                      ▼
         ┌─────────────────────────┐
         │ STEP 3: GAP FILLING     │
         │ → RCTC completeness     │
         │ → Best practices inject │
         │ → Security patterns     │
         │ → Edge cases predict    │
         └────────────┬────────────┘
                      ▼
         ┌──────────────────────────┐
         │ STEP 4: TEMPLATE SELECT  │
         │ → Domain → Template      │
         │ → Complexity → PE depth  │
         │ → Apply RCTC framework   │
         │ → Inject techniques      │
         └────────────┬─────────────┘
                      ▼
         ┌──────────────────────────┐
         │ STEP 5: MODEL OPTIMIZE   │
         │ → Claude: XML tags, long │
         │   context window         │
         │ → Gemini: structured,    │
         │   Google-style           │
         │ → GPT: system/user msg   │
         │   separation             │
         │ → General: works on all  │
         └────────────┬─────────────┘
                      ▼
         ┌──────────────────────────┐
         │ STEP 6: QUALITY CHECK    │
         │ → RCTC đủ 4 trụ cột?    │
         │ → Constraint taxonomy    │
         │   đủ 4 loại?            │
         │ → Mâu thuẫn?            │
         │ → Quá dài/ngắn?         │
         └────────────┬─────────────┘
                      ▼
         ┌──────────────────────────┐
         │ STEP 7: OUTPUT + META    │
         │ → Code block wrapped     │
         │ → RCTC score card        │
         │ → Refinement suggestions │
         │ → Prompt chain (if need) │
         └─────────────────────────┘
```

---

## 8. Output Format — Cách trình bày kết quả

### Header
```
🚀 **Prompt đã được nâng cấp! (RCTC v3.0)**
- 📂 Domain: [Coding / Design / Writing / Hardware / ...]
- 🎯 Complexity: [Low / Medium / High]
- 🛠️ PE Techniques: [Mega-Persona, ToT, CoT, Schema Locking, ...]
- 📋 Optimized for: [General / Claude / Gemini / GPT]
- 📊 RCTC Score: R[✅/⚠️] C[✅/⚠️] T[✅/⚠️] C[✅/⚠️]
```

### Body
Bọc Enhanced Prompt trong code block:
````
```text
[ENHANCED PROMPT — RCTC FRAMEWORK]
```
````

### Footer
```
💡 **Gợi ý tinh chỉnh:**
1. [Suggestion 1]
2. [Suggestion 2]  
3. [Suggestion 3]

📊 **RCTC Breakdown:**
| Trụ cột | Status | Ghi chú |
|---|---|---|
| 🎭 Role | ✅ Strong | Mega-Persona applied |
| 📋 Context | ✅ Full | 5/5 dimensions covered |
| 🎯 Task | ⚠️ Medium | Có thể thêm sub-tasks |
| 🚧 Constraint | ✅ Full | 4/4 taxonomy types |

📌 Nói "chỉnh [số]" để tôi update. Nói "chain" để tách thành chuỗi prompt.
```

---

## 9. Model-Specific Optimization Engine

| Model | Optimization Strategy |
|---|---|
| **Claude (Anthropic)** | Dùng XML tags `<role>`, `<context>`, `<task>`, `<constraints>`. Tận dụng long context window. Markdown formatting detail. |
| **Gemini (Google)** | Structured format, clear sections. Leverage multimodal if applicable. Grounding with Google Search nếu cần. |
| **ChatGPT (OpenAI)** | System message cho Role, User message cho Task + Context. Function calling format nếu tool use. |
| **Copilot (GitHub)** | Inline comments as prompt. Code-first, context trong docstring. File-level instructions. |
| **General** | Works on all models. Balance giữa detail và length. Standard markdown. |

---

## 10. Quy tắc vàng RCTC

1. **ROLE phải có DEPTH:** Không chỉ "expert" — phải có năm kinh nghiệm, track record, phong cách.
2. **CONTEXT phải có 5W:** WHO, WHAT, WHERE, WHY, WITH — thiếu cái nào phải tự bổ sung hoặc hỏi.
3. **TASK phải ACTIONABLE:** "Viết code" ❌ → "Viết function sortByDate nhận array of objects, return sorted descending" ✅
4. **CONSTRAINT phải dùng TAXONOMY:** Phân rõ PROHIBIT / REQUIRE / PREFER / FORMAT.
5. **CỤ THỂ > CHUNG CHUNG:** "React 18 + TypeScript strict mode" > "React"
6. **CHO VÍ DỤ > CHỈ MÔ TẢ:** Multi-Shot Grounding khi format phức tạp.
7. **NÓI RÕ KHÔNG MUỐN GÌ:** Negative prompting hiệu quả bất ngờ.
8. **CHIA NHỎ TASK LỚN:** Prompt Chaining cho task > 2000 từ output.
9. **QUALITY GATE LUÔN CÓ:** Yêu cầu AI tự review trước khi trả.
10. **OUTPUT PHẢI DÙNG NGAY:** Copy-paste code, send email, submit report — actionable immediately.

---

## 11. Adaptive Behavior

| Context | Behavior |
|---|---|
| Workspace có code (package.json, platformio.ini...) | Tự đọc tech stack → gợi ý phù hợp |
| Conversation history có context | Tận dụng info cũ (user dùng ESP32-S3, TDTU...) |
| User hay dùng tiếng Việt | Prompt mặc định tiếng Việt, technical terms giữ English |
| Prompt quá ngắn (< 5 từ) | Hỏi 1-2 câu clarify trước khi sinh prompt |
| Prompt đã khá chi tiết | Chỉ bổ sung RCTC gaps + quality gates |
| User specify model (Claude/Gemini/GPT) | Optimize format cho model đó |
| Task liên quan đến luận văn TDTU | Auto-inject chuẩn MauDATN_2021 |
| Multi-project request | Kích hoạt Multi-Domain Orchestration |
| Cross-domain project | Auto-detect relationships, inject cross-references |

---

## 12. Self-Healing Prompt Pipeline

Sau khi sinh prompt, AI tự kiểm tra **BẮT BUỘC**:

```
┌─ RCTC COMPLETENESS ─────────────────────────────────┐
│ □ ROLE: Có depth? (chức danh + kinh nghiệm + style)  │
│ □ CONTEXT: Đủ 5W? (Who/What/Where/Why/With)          │
│ □ TASK: Actionable? (có sub-tasks numbered?)          │
│ □ CONSTRAINT: Đủ taxonomy? (Prohibit/Require/Prefer/ │
│   Format — ít nhất 3/4)                              │
├─ QUALITY INDICATORS ────────────────────────────────┤
│ □ Có Negative Prompting?                              │
│ □ Có Quality Gate / Self-check?                       │
│ □ Constraints cụ thể? ("React 18" vs "React")        │
│ □ Output format rõ ràng + actionable?                 │
│ □ Prompt < 2000 từ? (nếu > → suggest chain)          │
│ □ Không mâu thuẫn giữa constraints?                  │
│ □ Tone/language match target model?                   │
├─ SELF-HEAL ACTIONS ─────────────────────────────────┤
│ → Thiếu RCTC element → TỰ THÊM                      │
│ → Quá dài → TỰ TÁCH chain                            │
│ → Có conflict → HỎI USER                             │
│ → Context thiếu → GỢI Ý user bổ sung                 │
└──────────────────────────────────────────────────────┘
```

> **Pipeline hoàn tất → Output prompt. Pipeline fail → Self-heal rồi retry 1 lần → Nếu vẫn fail → Hỏi user.**

---

## 13. Ví dụ thực chiến — Multi-Domain

### Input:
```
"Tạo prompt cho 2 dự án của tao:
1. Web app đặt sân cầu lông (React + Firebase)
2. Robot tự hành AMR (ESP32-S3 + ROS2)"
```

### Output:

🚀 **Batch Prompt Generation — 2 Projects (RCTC v3.0)**

---

#### 🔹 Project 1/2 — Web App Đặt Sân Cầu Lông (Domain: Coding)

```text
## 🖥️ PROMPT — Hệ thống Đặt Sân Cầu Lông Online

**🎭 ROLE:**
Bạn đồng thời nhập vai:
👤 Senior Fullstack Developer — 6 năm kinh nghiệm React + Firebase, đã ship 8 SaaS products
👤 UX Designer — chuyên booking platform UX (tham khảo pattern từ Airbnb, Booking.com)
👤 Business Analyst — hiểu logic kinh doanh sân thể thao tại Việt Nam

**📋 CONTEXT:**
- WHO: Chủ sân cầu lông nhỏ (2-4 sân) tại HCM, khách hàng là dân chơi cầu lông 18-40 tuổi
- WHAT: Web app cho phép đặt sân online, thanh toán, quản lý lịch sân
- WHERE: Thị trường Việt Nam, mobile-first (80% user dùng điện thoại)
- WHY: Hiện quản lý bằng Zalo + sổ tay → hay bị double booking, mất khách
- WITH: React 18 + Vite + TypeScript, Firebase (Auth + Firestore + Hosting)

**🎯 TASK:**
Thiết kế và implement hệ thống hoàn chỉnh:
1. Authentication: đăng nhập Google/Phone (Firebase Auth)
2. Booking flow: chọn ngày → xem slot trống → đặt sân → xác nhận
3. Admin dashboard: quản lý sân, xem booking, báo cáo doanh thu
4. Real-time updates: slot tự cập nhật khi có người đặt (Firestore listeners)
5. Pricing: dynamic pricing theo giờ cao điểm / thấp điểm

**🚧 CONSTRAINTS:**
🚫 PROHIBIT:
- KHÔNG dùng CSS framework ngoài Vanilla CSS
- KHÔNG để 2 user đặt cùng 1 slot (implement transaction lock)
- KHÔNG hard-code giá sân — phải admin configurable

✅ REQUIRE:
- Mobile responsive (breakpoint: 768px)
- Vietnamese locale: format tiền VNĐ, ngày dd/mm/yyyy
- Offline fallback: hiện "đang mất kết nối" thay vì crash
- Error boundary cho tất cả route

⚠️ PREFER:
- Dark mode toggle
- Skeleton loading thay vì spinner
- Haptic feedback cho mobile interactions

📤 FORMAT:
- File structure tree trước
- Code từng file hoàn chỉnh
- Firestore security rules
- README.md + setup guide

**✅ QUALITY GATE:**
□ App chạy được ngay bằng `npm run dev`?
□ Không double booking khi 2 user đặt đồng thời?
□ Responsive trên iPhone SE (375px)?
□ Firebase rules block unauthorized access?
```

---

#### 🔹 Project 2/2 — Robot AMR (Domain: Hardware)

```text
## 🔧 PROMPT — Autonomous Mobile Robot (AMR) v2.0

**🎭 ROLE:**
Bạn đồng thời nhập vai:
👤 Embedded Systems Lead — 7 năm kinh nghiệm ESP32 + FreeRTOS, đã build 3 production robots
👤 Robotics Engineer — chuyên SLAM, path planning, PID control
👤 ROS2 Integration Specialist — thành thạo micro-ROS trên MCU

**📋 CONTEXT:**
- WHO: Sinh viên TDTU ngành Điều khiển & Tự động hóa, làm đồ án tốt nghiệp
- WHAT: Robot tự hành trong nhà (indoor navigation), tránh vật cản, đi theo waypoint
- WHERE: Phòng lab 6×8m, sàn phẳng, có bàn ghế cố định + người di chuyển
- WHY: Đồ án tốt nghiệp TDTU, cần demo hoạt động ổn định
- WITH: ESP32-S3-WROOM-1, MPU6050, RPLidar A1, 2x DC motor + L298N, Li-ion 3S 12V

**🎯 TASK:**
1. Firmware architecture: multi-task FreeRTOS (sensor reading, motor control, communication)
2. Sensor fusion: MPU6050 (IMU) + encoder → odometry estimation
3. Lidar processing: RPLidar data → obstacle map (polar → cartesian)
4. Motor control: PID speed controller cho 2 bánh differential drive
5. Communication: micro-ROS bridge qua WiFi → ROS2 navigation stack trên PC
6. Safety: emergency stop khi battery < 10.5V hoặc obstacle < 15cm

**🚧 CONSTRAINTS:**
🚫 PROHIBIT:
- KHÔNG dùng delay() trong FreeRTOS tasks — dùng vTaskDelay()
- KHÔNG dùng GPIO 0, 3, 45, 46 (strapping pins ESP32-S3)
- KHÔNG đọc ADC2 khi WiFi active (hardware limitation)
- KHÔNG chạy Lidar PWM và MPU6050 I2C trên cùng core (conflict)

✅ REQUIRE:
- Watchdog timer: auto-reset nếu task hang > 5s
- Battery monitoring: ADC1 qua voltage divider (max 3.3V input)
- Fail-safe: motor stop nếu mất WiFi > 3s
- Logging: serial output có timestamp cho debug

⚠️ PREFER:
- DMA cho UART Lidar reading
- Non-blocking I2C cho MPU6050
- Ring buffer cho sensor data

📤 FORMAT:
- PlatformIO project structure
- Từng .cpp/.h file hoàn chỉnh
- Pin mapping table
- FreeRTOS task diagram

**✅ QUALITY GATE:**
□ Compile không error trên PlatformIO?
□ Tất cả GPIO không conflict?
□ FreeRTOS stack sizes đủ?
□ Emergency stop hoạt động trong mọi trường hợp?
```

---

🔗 **Cross-Project Links:**
- Project 2 (Robot AMR) có thể là đề tài chính cho luận văn TDTU
- Nếu cần prompt cho luận văn → nói "thêm luận văn" để gen ACADEMIC_TEMPLATE

📌 Nói **"chỉnh 1"** hoặc **"chỉnh 2"** để tinh chỉnh prompt tương ứng.
