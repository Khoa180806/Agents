---
# Metadata — điền đầy đủ trước khi sử dụng
id: skill-[slug-ngắn]           # Ví dụ: skill-code-review
name: "[Tên Skill Rõ Ràng]"     # Ví dụ: "Code Review Checklist"
tags: [coding, review]           # Các tag liên quan
version: "1.0.0"
created: YYYY-MM-DD
updated: YYYY-MM-DD
author: "[Tên bạn]"
estimated_time: "~[X] phút"     # Thời gian ước tính để hoàn thành
---

# [Tên Skill]

> **Mô tả ngắn gọn** (1-2 câu): Skill này làm gì và khi nào nên dùng.

---

## 🎯 Mục Đích (Purpose)

<!-- Giải thích bối cảnh và lý do tồn tại của skill này -->
<!-- Tập trung vào GIÁ TRỊ mang lại, không phải cách thực hiện -->

[Điền mục đích và giá trị của skill]

---

## 📥 Input Cần Có (Required Inputs)

<!-- Liệt kê chính xác những gì agent cần từ bạn trước khi bắt đầu -->
<!-- Phân biệt required (bắt buộc) và optional (tùy chọn) -->

### Bắt Buộc (Required)
- `[input_1]`: [Mô tả — ví dụ: "Code snippet hoặc đường dẫn file cần review"]
- `[input_2]`: [Mô tả — ví dụ: "Ngôn ngữ lập trình"]

### Tùy Chọn (Optional)
- `[input_3]`: [Mô tả — ví dụ: "Focus vào area cụ thể (security/performance/readability)"]
  - Mặc định: [giá trị mặc định nếu không cung cấp]

---

## ⚙️ Các Bước Thực Hiện (Execution Steps)

<!-- Liệt kê từng bước theo thứ tự, đủ cụ thể để agent không cần đoán -->
<!-- Mỗi bước nên có: hành động + tiêu chí hoàn thành -->

**Bước 1: [Tên bước]**
- [Hành động cụ thể]
- [Tiêu chí: bước này hoàn thành khi nào?]

**Bước 2: [Tên bước]**
- [Hành động cụ thể]
- [Tiêu chí]

**Bước 3: [Tên bước]**
- [Hành động cụ thể]
- [Tiêu chí]

<!-- Thêm bước nếu cần, giữ số bước tối thiểu nhưng đủ -->

---

## 📤 Output Mong Đợi (Expected Output)

<!-- Mô tả chính xác kết quả agent sẽ tạo ra -->
<!-- Càng cụ thể càng tốt: format, length, nội dung bắt buộc -->

### Format
<!-- Ví dụ: Markdown, JSON, plain text, code block -->
[Mô tả format đầu ra]

### Cấu Trúc Output
<!-- Mô tả các section/thành phần bắt buộc trong output -->
```
[Ví dụ cấu trúc output — có thể là template text]
```

### Tiêu Chí Chất Lượng
- [ ] [Tiêu chí 1 — ví dụ: "Mỗi issue phải có mức độ severity"]
- [ ] [Tiêu chí 2 — ví dụ: "Có ít nhất 1 suggestion cho mỗi issue"]
- [ ] [Tiêu chí 3]

---

## 💡 Ví Dụ Sử Dụng (Usage Examples)

### Ví dụ 1: [Tình huống cơ bản]

**Input của bạn:**
```
[Ví dụ input]
```

**Output của agent:**
```
[Ví dụ output mẫu]
```

### Ví dụ 2: [Tình huống nâng cao]

**Input của bạn:**
```
[Ví dụ input phức tạp hơn]
```

**Output của agent:**
```
[Ví dụ output tương ứng]
```

---

## 🔗 Skills & Rules Liên Quan

<!-- Liệt kê skills/rules khác thường được dùng cùng với skill này -->

- Skills: [`[skill-liên-quan]`](./skill-lien-quan.md)
- Rules: [`[rule-áp-dụng]`](../rules/rule-ap-dung.md)

---

## ⚠️ Lưu Ý & Hạn Chế (Notes & Limitations)

<!-- Ghi chú những điều quan trọng, cạm bẫy, hoặc giới hạn của skill -->

- **[Lưu ý 1]**: [Giải thích]
- **[Hạn chế 1]**: [Giải thích và cách workaround nếu có]

---

## 📝 Lịch Sử Thay Đổi (Changelog)

| Version | Ngày | Thay đổi |
|---------|------|---------|
| 1.0.0 | YYYY-MM-DD | Khởi tạo |
