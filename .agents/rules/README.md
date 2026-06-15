# 📏 Rules — Quy Tắc Hành Vi Agent

> Rules định nghĩa **ràng buộc và hành vi mặc định** mà AI agent phải tuân theo.  
> Khác với skills (làm gì) hay workflows (làm như thế nào), rules quy định **cách hành xử**.

---

## 🤔 Rule Là Gì? (What is a Rule?)

Một rule là một tập hợp **ràng buộc, tiêu chuẩn hoặc hành vi** mà agent áp dụng **ngầm định** trong suốt quá trình làm việc, không cần nhắc lại mỗi lần.

**Ví dụ:**
- "Luôn dùng tiếng Việt khi giao tiếp với user"
- "Không được xóa code cũ mà không thông báo"
- "Tên hàm phải dùng camelCase"

---

## 🗂️ Phân Loại Rules (Rule Categories)

### 1. Global Rules
Áp dụng **cho mọi dự án** và mọi ngữ cảnh. Thường được đặt ở root level (`GEMINI.md`).

**Ví dụ**: Ngôn ngữ giao tiếp, git commit format, naming conventions.

### 2. Project Rules
Áp dụng **trong một dự án cụ thể**. Đặt trong `rules/` của project đó.

**Ví dụ**: Framework được dùng, kiến trúc cụ thể, team conventions.

### 3. Task Rules
Áp dụng **chỉ trong một task hoặc session cụ thể**. Paste trực tiếp vào chat.

**Ví dụ**: "Trong task này, chỉ dùng Python thuần, không dùng thư viện ngoài".

---

## 📁 Files Trong Thư Mục Này

| File | Mô tả |
|------|-------|
| `_template.md` | Template mẫu — copy để tạo rule mới |
| `coding-standards.md` | Quy tắc viết code (style, naming, formatting) |
| `communication-style.md` | Quy tắc giao tiếp (ngôn ngữ, tone, cách phản hồi) |
| `web-ui-functional-testing-rules.md` | Quy tắc và tiêu chuẩn thiết kế kịch bản kiểm thử chức năng giao diện web |

---

## ✍️ Hướng Dẫn Viết Rule (How to Write a Rule)

### Bước 1: Copy template
```bash
cp rules/_template.md rules/ten-rule-moi.md
```

### Bước 2: Điền metadata
```yaml
id: rule-[số thứ tự hoặc slug ngắn]
name: "Tên rule rõ ràng"
scope: global | project | task
version: "1.0.0"
```

### Bước 3: Viết nội dung theo nguyên tắc

**✅ Viết rule tốt:**
- Cụ thể và không mơ hồ
- Có ví dụ đúng (✅) và sai (❌)
- Ghi rõ lý do (why, not what)
- Có phần ngoại lệ nếu cần

**❌ Tránh:**
- Rule quá chung chung ("viết code tốt")
- Không có ví dụ minh họa
- Mâu thuẫn với rule khác
- Quá nhiều ngoại lệ làm loãng rule

---

## 🏷️ Convention Đặt Tên File

- Dùng `kebab-case` cho tên file: `no-over-engineering.md`
- Tên phản ánh **nội dung** rule, không phải category: `prefer-async-await.md` thay vì `javascript-rule.md`
- Tránh prefix số (`01-`, `02-`) — dùng alphabet tự nhiên

---

## 🔗 Cách Apply Rule Cho Từng Platform

| Platform | Cách áp dụng |
|---------|-------------|
| Gemini/Antigravity | Đặt `GEMINI.md` ở root; paste nội dung rule vào chat |
| Codex | Đặt trong system prompt hoặc `.codex/instructions.md` |
| Cursor | Paste vào `.cursorrules` ở root project |
| Claude Projects | Thêm vào "Project Instructions" |
| Claude Chat | Paste vào đầu conversation |

---

## ⚠️ Lưu Ý Quan Trọng

> [!NOTE]
> Rules **không thay thế** common sense. Nếu một rule dẫn đến kết quả kỳ lạ trong một tình huống cụ thể, hãy ghi nhận và cập nhật phần `exceptions`.

> [!TIP]
> Giữ số lượng rules **tối thiểu nhưng đủ**. Rules nhiều quá → AI khó nhớ hết → hiệu quả giảm. Ưu tiên rules có tác động lớn nhất.

---

*Xem template tại [`_template.md`](./_template.md)*
