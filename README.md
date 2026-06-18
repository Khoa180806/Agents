# 🤖 Personal Agent System

> Bộ tài liệu định nghĩa **Rules (Quy tắc)**, **Skills (Kỹ năng)** và **Workflows (Quy trình)** cá nhân dành cho các AI Assistant (Antigravity/Gemini, Cursor, Claude, Codex...). Giúp tối ưu hiệu suất pair programming và duy trì chất lượng codebase đồng bộ.

---

## 📌 Mục Lục (Table of Contents)

- [📖 1. Mục Đích (Purpose)](#-1-mục-đích-purpose)
- [🛠️ 2. Hướng Dẫn Setup (Setup Instructions)](#️-2-hướng-dẫn-setup-setup-instructions)
- [🗂️ 3. Cấu Trúc Thư Mục (Directory Structure)](#️-3-cấu-trúc-thư-mục-directory-structure)
- [🧩 4. Ba Thành Phần Cốt Lõi (Core Components)](#-4-ba-thành-phần-cốt-lõi-core-components)
- [⚡ 5. Hướng Dẫn Nhanh (Quick Start)](#-5-hướng-dẫn-nhanh-quick-start)
- [📐 6. Nguyên Tắc Thiết Kế (Design Principles)](#-6-nguyên-tắc-thiết-kế-design-principles)
- [🔧 7. Tạo File Mới (Creating New Files)](#-7-tạo-file-mới-creating-new-files)
- [🗃️ 8. Quy Ước Đặt Tên File (File Naming Convention)](#️-8-quy-ước-đặt-tên-file-file-naming-convention)
- [📦 9. Versioning & Changelog](#-9-versioning--changelog)

---

## 📖 1. Mục Đích (Purpose)

Thay vì phải lặp lại các chỉ dẫn, giải thích cách thiết lập hoặc phong cách viết code mỗi khi bắt đầu một dự án mới, hệ thống này cung cấp cho AI Assistant một bộ khung chuẩn hóa:

*   **Import Rules** ➔ Định hình ngay hành vi, giới hạn và tiêu chuẩn code mong muốn.
*   **Gọi Skills** ➔ Yêu cầu AI thực hiện nhanh một tác vụ cụ thể theo quy trình chuẩn.
*   **Chạy Workflows** ➔ Dẫn dắt AI thực hiện tuần tự các tác vụ phức tạp hoặc đa bước.

---

## 🛠️ 2. Hướng Dẫn Setup (Setup Instructions)

> [!IMPORTANT]
> Việc thiết lập đúng cấu hình là bắt buộc để AI Assistant nhận diện được các quy tắc toàn cục cũng như các chỉ dẫn riêng biệt của từng dự án.

### Bước 1: Cấu hình quy tắc toàn cục (Global Rules)
Copy file `GEMINI.md` từ thư mục gốc của kho lưu trữ này vào thư mục người dùng của bạn:
*   **Đường dẫn đích**: `~/.gemini`
    *   *Windows*: `%USERPROFILE%\.gemini` (ví dụ: `C:\Users\<Tên-User>\.gemini`)
    *   *macOS / Linux*: `~/.gemini`
*   *Lưu ý*: Hãy tự tạo thư mục `.gemini` nếu nó chưa tồn tại trên hệ thống của bạn.

### Bước 2: Cấu hình quy tắc cho từng dự án (Project-specific Agents)
1.  Copy toàn bộ thư mục `.agents` từ dự án này vào thư mục gốc (root directory) của dự án mà bạn đang làm việc.
2.  Sau khi copy, hãy xóa các file hướng dẫn hoặc template không cần thiết bên trong để giữ cho cấu trúc dự án của bạn sạch sẽ:
    *   Xóa `README.md` và `_template.md` trong `.agents/rules/`
    *   Xóa `README.md` và `_template.md` trong `.agents/skills/`
    *   Xóa `README.md` và `_template.md` trong `.agents/workflows/`

---

## 🗂️ 3. Cấu Trúc Thư Mục (Directory Structure)

```text
agent-system/
│
├── README.md                  ← Hướng dẫn sử dụng hệ thống (File này)
├── GEMINI.md                  ← Quy tắc toàn cục áp dụng cho toàn bộ dự án
│
└── .agents/                   ← Thư mục chứa cấu hình AI Agent
    ├── rules/                 ← Các ràng buộc về hành vi và phong cách code
    │   ├── README.md          ← Hướng dẫn tạo rules
    │   ├── _template.md       ← Mẫu cấu trúc một rule mới
    │   ├── coding-standards.md
    │   └── communication-style.md
    │
    ├── skills/                ← Các kỹ năng cụ thể
    │   ├── README.md
    │   ├── _template.md
    │   ├── code-review.md
    │   └── debug-assistant.md
    │
    └── workflows/             ← Quy trình công việc
        ├── README.md
        ├── _template.md
        ├── new-feature-development.md
        └── bug-investigation.md
```

---

## 🧩 4. Ba Thành Phần Cốt Lõi (Core Components)

### 📏 Rules — Quy Tắc
Định nghĩa các **ràng buộc và hành vi ngầm định** mà Agent bắt buộc phải tuân thủ trong suốt phiên làm việc. Chúng hoạt động như luật khung cho dự án.
*   👉 Chi tiết hướng dẫn: [rules/README.md](./.agents/rules/README.md)

### 🛠️ Skills — Kỹ Năng
Mô tả **khả năng thực hiện tác vụ độc lập** mà Agent có thể kích hoạt khi được yêu cầu. Mỗi skill có định nghĩa dữ liệu đầu vào, các bước xử lý và đầu ra mong đợi rõ ràng.
*   👉 Chi tiết hướng dẫn: [skills/README.md](./.agents/skills/README.md)

### 🔄 Workflows — Quy Trình
Chuỗi các hành động **có cấu trúc và mang tính tuần tự** để giải quyết một mục tiêu phức tạp. Workflows thường sẽ kết hợp nhiều skills và áp dụng đồng thời các rules liên quan.
*   👉 Chi tiết hướng dẫn: [workflows/README.md](./.agents/workflows/README.md)

---

## ⚡ 5. Hướng Dẫn Nhanh (Quick Start)

### Dùng với Gemini / Antigravity
1.  Đặt file `GEMINI.md` vào thư mục gốc của project đang mở (hoặc setup global tại thư mục người dùng như ở phần Setup). AI sẽ tự động đọc và áp dụng rules.
2.  Để kích hoạt skills hoặc workflows, hãy tham chiếu bằng cách copy nội dung hoặc chỉ đường dẫn tương đối trong khung chat:
    ```text
    Đọc file .agents/skills/code-review.md và thực hiện skill này với PR hiện tại.
    ```

### Dùng với Cursor / Windsurf
1.  Copy nội dung các rules bạn muốn áp dụng vào file `.cursorrules` (hoặc `.windsurfrules`) tại thư mục gốc của dự án.
2.  Kêu gọi thực hiện skills/workflows thông qua chat bằng việc tag các file tương ứng (sử dụng `@.agents/skills/code-review.md`).

### Dùng với Claude Projects
1.  Nhập các quy tắc chung (rules) vào mục **Project Instructions**.
2.  Tải các file skill và workflow cần thiết lên phần **Project Knowledge** của Claude.

### Dùng với Codex App
1.  **Global Rules**: Copy file `GEMINI.md` vào thư mục người dùng `~/.codex/` (tương tự như `.gemini`).
2.  **Project Rules**: Copy thư mục `.agents` vào thư mục gốc của dự án.
3.  **System Prompt**: Trong Codex App, vào Settings > Custom Instructions và thêm:
    ```text
    Đọc và áp dụng các quy tắc từ file GEMINI.md và thư mục .agents/
    ```
4.  **Sử dụng Skills/Workflows**: Tag file trực tiếp trong chat:
    ```text
    @.agents/skills/code-review.md - Thực hiện code review cho file hiện tại
    ```

### Dùng với Kiro IDE
1.  **Steering Files (Rules)**: Copy nội dung các rules vào thư mục `.kiro/steering/`:
    ```bash
    mkdir -p .kiro/steering
    cp .agents/rules/*.md .kiro/steering/
    ```
2.  **Skills**: Kiro hỗ trợ skills thông qua thư mục `.kiro/skills/`:
    ```bash
    mkdir -p .kiro/skills
    cp .agents/skills/*.md .kiro/skills/
    ```
3.  **Workflows**: Sử dụng Spec mode của Kiro hoặc tạo custom agents:
    ```bash
    mkdir -p .kiro/agents
    # Tạo custom agent dựa trên workflow
    ```
4.  **Kích hoạt**: 
    *   Rules tự động áp dụng khi đặt trong `.kiro/steering/`
    *   Skills có thể được kích hoạt bằng cách gọi tên trong chat
    *   Workflows thực hiện thông qua Spec session hoặc invoke custom agent

---

## 📐 6. Nguyên Tắc Thiết Kế (Design Principles)

| Nguyên Tắc | Mô Tả Chi Tiết |
| :--- | :--- |
| **Single Responsibility** | Mỗi file Markdown chỉ mô tả duy nhất một Rule, một Skill hoặc một Workflow. |
| **Self-contained** | Mỗi thành phần phải độc lập, tự chứa đủ thông tin để Agent hiểu mà không cần liên kết ngoài phức tạp. |
| **Version-tracked** | Tất cả tài liệu phải ghi rõ số phiên bản (version) trong phần metadata để tiện theo dõi. |
| **Platform-agnostic** | Cấu trúc định nghĩa thuần Markdown, không phụ thuộc vào công cụ hay IDE độc quyền nào. |
| **Bilingual Support** | Ưu tiên viết tiêu đề bằng tiếng Anh, phần mô tả nội dung được trình bày song ngữ Anh-Việt. |

---

## 🔧 7. Tạo File Mới (Creating New Files)

Để thêm mới một quy tắc, kỹ năng hoặc quy trình vào dự án của bạn, hãy copy từ file template tương ứng và đổi tên theo định dạng `kebab-case`:

### Tạo Rule Mới
```bash
cp .agents/rules/_template.md .agents/rules/ten-rule-moi.md
```

### Tạo Skill Mới
```bash
cp .agents/skills/_template.md .agents/skills/ten-skill-moi.md
```

### Tạo Workflow Mới
```bash
cp .agents/workflows/_template.md .agents/workflows/ten-workflow-moi.md
```

---

## 🗃️ 8. Quy Ước Đặt Tên File (File Naming Convention)

| Thành Phần | Quy Ước Đặt Tên (Convention) | Ví Dụ Minh Họa |
| :--- | :--- | :--- |
| **Rule** | `kebab-case.md` | `no-over-engineering.md` |
| **Skill** | `kebab-case.md` | `write-unit-tests.md` |
| **Workflow** | `kebab-case.md` | `release-management.md` |
| **Template** | `_template.md` | `_template.md` |
| **Index / Docs** | `README.md` | `README.md` |

---

## 📦 9. Versioning & Changelog

Dự án tuân thủ tiêu chuẩn quản lý phiên bản **Semantic Versioning (SemVer)**:
*   `MAJOR` — Thay đổi lớn về cấu trúc thư mục hoặc định dạng tệp tin cốt lõi.
*   `MINOR` — Thêm mới các file Rules, Skills hoặc Workflows mà không làm hỏng tính tương thích cũ.
*   `PATCH` — Sửa lỗi chính tả, cải thiện nội dung giải thích hoặc cập nhật tài liệu hướng dẫn.

*   **Phiên bản hiện tại**: `v1.0.1`
*   **Cập nhật lần cuối**: 2026-06-15
*   *Lưu ý: Mọi thay đổi cấu trúc tổng thể cần được ghi nhận trực tiếp tại phần này.*
