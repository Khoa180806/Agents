---
# Metadata — điền đầy đủ trước khi sử dụng
id: rule-[slug-ngắn]          # Ví dụ: rule-no-plaintext-secrets
name: "[Tên Rule Rõ Ràng]"    # Ví dụ: "No Plaintext Secrets in Code"
scope: global                  # global | project | task
tags: [security, coding]       # Các tag liên quan
version: "1.0.0"
created: YYYY-MM-DD
updated: YYYY-MM-DD
author: "[Tên bạn]"
---

# [Tên Rule]

> **Mô tả ngắn gọn** (1-2 câu): Rule này làm gì và tại sao nó tồn tại.

---

## 🎯 Mục Đích (Purpose)

<!-- Giải thích lý do tồn tại của rule này — WHY, không phải WHAT -->
<!-- Ví dụ: "Để đảm bảo tính nhất quán trong codebase và giảm thiểu bugs từ naming conflicts" -->

[Điền lý do tại sao rule này quan trọng]

---

## 📋 Quy Tắc Chi Tiết (Rules)

<!-- Liệt kê các quy tắc cụ thể, rõ ràng, không mơ hồ -->
<!-- Dùng imperative mood: "Phải...", "Không được...", "Luôn luôn..." -->

1. **[Tên quy tắc 1]**: [Mô tả chi tiết]
2. **[Tên quy tắc 2]**: [Mô tả chi tiết]
3. **[Tên quy tắc 3]**: [Mô tả chi tiết]

---

## ✅ Ví Dụ Đúng (Correct Examples)

<!-- Ít nhất 2-3 ví dụ cụ thể, có thể chạy được hoặc áp dụng được -->

```[language]
// ✅ GOOD: [Giải thích tại sao đây là ví dụ đúng]
[code hoặc nội dung đúng]
```

```[language]
// ✅ GOOD: [Ví dụ đúng thứ 2]
[code hoặc nội dung đúng]
```

---

## ❌ Ví Dụ Sai (Incorrect Examples)

<!-- Ví dụ vi phạm rule — giúp AI hiểu ranh giới rõ hơn -->

```[language]
// ❌ BAD: [Giải thích tại sao đây là vi phạm]
[code hoặc nội dung sai]
```

```[language]
// ❌ BAD: [Vi phạm thứ 2]
[code hoặc nội dung sai]
```

---

## 🔄 Hành Động Khi Vi Phạm (On Violation)

<!-- Mô tả agent phải làm gì khi phát hiện vi phạm -->
<!-- Ví dụ: "Dừng lại, thông báo cho user, đề xuất cách sửa" -->

- [ ] [Hành động 1]
- [ ] [Hành động 2]
- [ ] [Hành động 3 — tùy chọn]

---

## 🚫 Ngoại Lệ (Exceptions)

<!-- Các trường hợp rule KHÔNG áp dụng hoặc áp dụng khác đi -->
<!-- Nếu không có ngoại lệ, để: "Không có ngoại lệ." -->

- **[Tình huống ngoại lệ 1]**: [Lý do và cách xử lý]
- **[Tình huống ngoại lệ 2]**: [Lý do và cách xử lý]

---

## 🔗 Tham Chiếu (References)

<!-- Links tới rules liên quan, tài liệu, hoặc standards -->

- Liên quan: [`[rule-khác]`](./rule-khac.md)
- Nguồn tham khảo: [link tới standard/article nếu có]

---

## 📝 Lịch Sử Thay Đổi (Changelog)

| Version | Ngày | Thay đổi |
|---------|------|---------|
| 1.0.0 | YYYY-MM-DD | Khởi tạo |
