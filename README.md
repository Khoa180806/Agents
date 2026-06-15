# 🤖 Personal Agent System

> Bộ **rules**, **skills** và **workflows** cá nhân dùng cho các AI assistant.  
> Thiết kế để dùng chung trên nhiều platform: Gemini/Antigravity, Codex, Cursor, Claude, v.v.

---

## 📖 Mục Đích (Purpose)

Thay vì giải thích lại cách làm việc mỗi khi mở một project mới, bộ này cho phép bạn:

- **Import rules** → AI biết ngay giới hạn và hành vi mong muốn
- **Gọi skills** → AI thực hiện ngay một kỹ năng cụ thể theo chuẩn
- **Chạy workflows** → AI dẫn dắt từng bước cho các task phức tạp

---

## 🗂️ Cấu Trúc Thư Mục (Directory Structure)

```
agent-system/
│
├── README.md                  ← Bạn đang đọc file này
├── GEMINI.md                  ← Quy tắc tổng thể cho AI (toàn dự án)
│
├── rules/                     ← Ràng buộc hành vi của agent
│   ├── README.md              ← Hướng dẫn tạo rules
│   ├── _template.md           ← Template mẫu để copy
│   ├── coding-standards.md    ← Ví dụ: quy tắc viết code
│   └── communication-style.md ← Ví dụ: quy tắc giao tiếp
│
├── skills/                    ← Kỹ năng cụ thể có thể invoke
│   ├── README.md              ← Hướng dẫn tạo skills
│   ├── _template.md           ← Template mẫu để copy
│   ├── code-review.md         ← Ví dụ: skill review code
│   └── debug-assistant.md    ← Ví dụ: skill debug
│
└── workflows/                 ← Quy trình nhiều bước
    ├── README.md              ← Hướng dẫn tạo workflows
    ├── _template.md           ← Template mẫu để copy
    ├── new-feature-development.md ← Ví dụ: phát triển feature
    └── bug-investigation.md   ← Ví dụ: điều tra bug
```

---

## 🧩 Ba Thành Phần Cốt Lõi (Core Components)

### 📏 Rules — Quy Tắc

Định nghĩa **ràng buộc và hành vi mặc định** mà agent phải tuân theo. Rules hoạt động như "luật bất thành văn" — luôn được áp dụng ngầm định.

→ Xem chi tiết tại [`rules/README.md`](./rules/README.md)

### 🛠️ Skills — Kỹ Năng

Mô tả **một khả năng cụ thể** mà agent có thể thực hiện khi được yêu cầu. Mỗi skill có input rõ ràng, các bước thực hiện, và output mong đợi.

→ Xem chi tiết tại [`skills/README.md`](./skills/README.md)

### 🔄 Workflows — Quy Trình

Chuỗi bước **tuần tự và có cấu trúc** để hoàn thành một task phức tạp. Workflows thường kết hợp nhiều skills và áp dụng nhiều rules cùng lúc.

→ Xem chi tiết tại [`workflows/README.md`](./workflows/README.md)

---

## 🛠️ Hướng Dẫn Setup (Setup Instructions)

1. **Cấu hình Global Rules**: Copy file `GEMINI.md` vào thư mục cấu hình toàn cục `~/.gemini` (đối với Windows là `%USERPROFILE%\.gemini` hoặc `C:\Users\<Tên-User>\.gemini`). Tạo thư mục `.gemini` nếu chưa có.
2. **Cấu hình Project-specific Agents**: Copy thư mục `.agents` vào thư mục gốc của dự án của bạn (hãy xóa các file `README.md` và `_template.md` bên trong các thư mục con `.agents/rules/`, `.agents/skills/`, và `.agents/workflows/` đi).

---

## ⚡ Hướng Dẫn Nhanh (Quick Start)

### Dùng với Gemini / Antigravity

1. Đặt `GEMINI.md` vào root của project — AI sẽ tự động đọc
2. Tham chiếu skills/workflows bằng cách paste nội dung vào chat:
   ```
   [Đọc file skills/code-review.md và thực hiện skill này với PR hiện tại]
   ```
3. Hoặc dẫn đường dẫn file khi chat

### Dùng với Codex (OpenAI)

1. Đặt rules vào system prompt hoặc `.codex/instructions.md`
2. Paste nội dung skill/workflow vào đầu conversation
3. Dùng `@file` syntax nếu tool hỗ trợ

### Dùng với Cursor / Windsurf

1. Copy nội dung rules vào `.cursorrules` tại root project
2. Invoke skills/workflows qua chat với đường dẫn tương đối

### Dùng với Claude Projects

1. Đặt rules vào "Project Instructions"
2. Upload file skills/workflows vào Project Knowledge

---

## 📐 Nguyên Tắc Thiết Kế (Design Principles)

| Nguyên tắc | Mô tả |
|-----------|-------|
| **Single Responsibility** | Mỗi file chỉ mô tả một rule/skill/workflow |
| **Self-contained** | Mỗi file có thể đọc độc lập mà không cần context khác |
| **Version-tracked** | Mỗi file có version trong metadata |
| **Platform-agnostic** | Không phụ thuộc vào cú pháp của một tool cụ thể |
| **Bilingual** | Tiêu đề tiếng Anh, mô tả song ngữ Việt–Anh |

---

## 🔧 Tạo File Mới (Creating New Files)

### Tạo Rule Mới
```bash
# Copy template và đặt tên theo kebab-case
cp rules/_template.md rules/ten-rule-moi.md
```

### Tạo Skill Mới
```bash
cp skills/_template.md skills/ten-skill-moi.md
```

### Tạo Workflow Mới
```bash
cp workflows/_template.md workflows/ten-workflow-moi.md
```

---

## 🗃️ Quy Ước Đặt Tên File (File Naming Convention)

| Loại | Convention | Ví dụ |
|------|-----------|-------|
| Rule | `kebab-case.md` | `no-over-engineering.md` |
| Skill | `kebab-case.md` | `write-unit-tests.md` |
| Workflow | `kebab-case.md` | `release-management.md` |
| Template | `_template.md` | `_template.md` |
| Index | `README.md` | `README.md` |

---

## 📦 Versioning

Project này theo **Semantic Versioning**:
- `MAJOR` — Thay đổi cấu trúc thư mục hoặc format file
- `MINOR` — Thêm rule/skill/workflow mới
- `PATCH` — Sửa lỗi hoặc cập nhật nội dung

**Version hiện tại**: `v1.0.0`  
**Cập nhật lần cuối**: 2026-06-08

---

*Mọi thay đổi cấu trúc tổng thể cần được ghi chép tại đây.*
