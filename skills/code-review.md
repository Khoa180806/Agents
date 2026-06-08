---
id: skill-code-review
name: "Code Review Checklist"
tags: [coding, review, quality, best-practices]
version: "1.0.0"
created: 2026-06-08
updated: 2026-06-08
author: "Personal"
estimated_time: "~15-30 phút"
---

# Code Review Checklist

> Review code theo một checklist chuẩn, phân loại issues theo severity, và đưa ra actionable suggestions.  
> Dùng khi muốn agent review một đoạn code, file, hoặc diff của PR.

---

## 🎯 Mục Đích (Purpose)

Manual code review thường bỏ sót issues do thiếu checklist nhất quán.
Skill này đảm bảo mọi review đều đi qua đầy đủ các tiêu chí — từ correctness,
security, performance đến code style — và output có format chuẩn để dễ action.

---

## 📥 Input Cần Có (Required Inputs)

### Bắt Buộc (Required)
- `code`: Code snippet, nội dung file, hoặc git diff cần review
- `language`: Ngôn ngữ lập trình (TypeScript, Python, Java, v.v.)

### Tùy Chọn (Optional)
- `context`: Mô tả ngắn về mục đích của code (ví dụ: "API endpoint xử lý payment")
  - Mặc định: Suy luận từ code
- `focus_areas`: Các area cần focus đặc biệt: `security` | `performance` | `readability` | `all`
  - Mặc định: `all`
- `severity_filter`: Chỉ hiển thị issues từ mức nào trở lên: `critical` | `major` | `minor`
  - Mặc định: Hiển thị tất cả

---

## ⚙️ Các Bước Thực Hiện (Execution Steps)

**Bước 1: Đọc và hiểu code**
- Đọc toàn bộ code được cung cấp
- Xác định: mục đích, các inputs/outputs, và các dependencies
- Ghi chú context nếu không rõ (sẽ hỏi ở cuối nếu cần)

**Bước 2: Kiểm tra Correctness**
- Logic có đúng với mục đích được mô tả không?
- Có edge cases nào chưa được xử lý? (null/undefined, empty array, negative numbers...)
- Error handling có đầy đủ và đúng chỗ không?
- Async/await được dùng đúng cách không?

**Bước 3: Kiểm tra Security**
- Input validation: user input có được validate trước khi dùng không?
- SQL injection: có dùng parameterized queries không?
- XSS: output có được sanitize không?
- Authentication/Authorization: các route nhạy cảm có được protect không?
- Secrets: có hardcoded credentials, API keys không?

**Bước 4: Kiểm tra Performance**
- Có N+1 query problems không?
- Loops có được tối ưu không? (tránh nested loops với large datasets)
- Có memory leaks tiềm ẩn không? (event listeners không được cleanup, v.v.)
- Caching có được dùng hợp lý không?

**Bước 5: Kiểm tra Code Style & Readability**
- Naming conventions có theo `coding-standards` rule không?
- Functions/methods có quá dài không? (> 50 lines là dấu hiệu cần refactor)
- Duplicate code (DRY violations)?
- Comments: có những chỗ cần comment WHY nhưng chưa có không?

**Bước 6: Tổng hợp và Format Output**
- Phân loại issues theo severity
- Sắp xếp: Critical → Major → Minor → Suggestions
- Đếm tổng số issues mỗi loại
- Đưa ra verdict tổng quan

---

## 📤 Output Mong Đợi (Expected Output)

### Format
Markdown với heading structure rõ ràng

### Cấu Trúc Output

```markdown
## 📋 Code Review: [tên file/function]

**Language**: [ngôn ngữ]  
**Reviewed**: [timestamp]  
**Overall**: ✅ Approved / ⚠️ Approved with suggestions / ❌ Changes required

---

### 🔴 Critical Issues ([số lượng])
<!-- Bugs, security vulnerabilities, data loss risks -->

**[CR-1]** [Tên issue ngắn gọn]
- **File/Line**: `[filename]:[line]`
- **Problem**: [Mô tả vấn đề]
- **Impact**: [Tác động nếu không sửa]
- **Fix**: [Code đề xuất sửa]

---

### 🟠 Major Issues ([số lượng])
<!-- Logic errors, missing error handling, performance problems -->

**[MJ-1]** [Tên issue]
- **File/Line**: `[filename]:[line]`
- **Problem**: [Mô tả]
- **Fix**: [Đề xuất]

---

### 🟡 Minor Issues ([số lượng])
<!-- Style violations, naming, readability -->

**[MN-1]** [Tên issue]
- **Line**: `[line]`
- **Problem**: [Mô tả]
- **Fix**: [Đề xuất]

---

### 💡 Suggestions ([số lượng])
<!-- Optional improvements, không bắt buộc -->

- [Suggestion 1]
- [Suggestion 2]

---

### 📊 Summary

| Category | Count |
|----------|-------|
| 🔴 Critical | X |
| 🟠 Major | X |
| 🟡 Minor | X |
| 💡 Suggestions | X |
| **Total** | **X** |
```

### Tiêu Chí Chất Lượng
- [ ] Mỗi Critical/Major issue phải có code example để sửa
- [ ] Không bỏ sót bước nào trong checklist
- [ ] Overall verdict phải nhất quán với số lượng issues
- [ ] Suggestions là optional, không ảnh hưởng verdict

---

## 💡 Ví Dụ Sử Dụng (Usage Examples)

### Ví dụ 1: Review function đơn giản

**Input của bạn:**
```
Hãy review đoạn code TypeScript sau:
---
async function getUser(id: string) {
  const user = await db.query(`SELECT * FROM users WHERE id = ${id}`);
  console.log('Found user:', user);
  return user;
}
```

**Output của agent:**
```markdown
## 📋 Code Review: getUser function

**Language**: TypeScript  
**Overall**: ❌ Changes required

### 🔴 Critical Issues (1)

**[CR-1]** SQL Injection Vulnerability
- **Line**: 2
- **Problem**: User input `id` được interpolate trực tiếp vào SQL query,
  tạo ra SQL injection vulnerability nghiêm trọng.
- **Impact**: Attacker có thể đọc/xóa toàn bộ database.
- **Fix**:
  ```typescript
  const user = await db.query('SELECT * FROM users WHERE id = $1', [id]);
  ```

### 🟡 Minor Issues (1)

**[MN-1]** Debug statement bị commit
- **Line**: 3
- **Problem**: `console.log` không nên có trong production code.
- **Fix**: Xóa dòng console.log, dùng proper logger nếu cần.

### 📊 Summary
| Category | Count |
|----------|-------|
| 🔴 Critical | 1 |
| 🟡 Minor | 1 |
| **Total** | **2** |
```

---

## 🔗 Skills & Rules Liên Quan

- Rules: [`coding-standards`](../rules/coding-standards.md)
- Workflows: [`new-feature-development`](../workflows/new-feature-development.md) — Dùng skill này ở Phase 3

---

## ⚠️ Lưu Ý & Hạn Chế (Notes & Limitations)

- **Context giúp ích rất nhiều**: Nếu cung cấp context về mục đích của code, review sẽ chính xác hơn đáng kể.
- **Không thay thế unit tests**: Review tìm issues trong code, nhưng không thể kiểm tra runtime behavior.
- **Large files**: Với file > 500 lines, nên chỉ định focus area để tránh output quá dài.

---

## 📝 Lịch Sử Thay Đổi (Changelog)

| Version | Ngày | Thay đổi |
|---------|------|---------|
| 1.0.0 | 2026-06-08 | Khởi tạo |
