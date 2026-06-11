# 🛠️ Skills — Kỹ Năng Agent

> Skills mô tả **một khả năng cụ thể** mà agent có thể thực hiện khi được yêu cầu.  
> Khác với rules (ràng buộc ngầm định) hay workflows (quy trình dài), skill là **một hành động hoàn chỉnh**, có input rõ ràng và output xác định.

---

## 🤔 Skill Là Gì? (What is a Skill?)

Một skill là tài liệu mô tả **cách agent thực hiện một nhiệm vụ cụ thể** theo chuẩn nhất định. Khi bạn invoke một skill, agent biết chính xác:

- Cần **thông tin gì** từ bạn (inputs)
- Thực hiện **các bước nào** (steps)
- Tạo ra **kết quả gì** (expected output)

**Tương tự như**: Function trong lập trình — có signature, body, và return value.

---

## 🆚 Skills vs Rules vs Workflows

| | Rules | Skills | Workflows |
|---|---|---|---|
| **Khi nào áp dụng** | Luôn luôn (ngầm định) | Khi được invoke | Khi được kích hoạt |
| **Độ dài** | Ngắn (constraints) | Trung bình (1 task) | Dài (multi-step process) |
| **Ví dụ** | "Dùng camelCase" | "Review code này" | "Phát triển feature mới" |
| **Input** | Không cần | Cần cụ thể | Cần cụ thể |
| **Output** | Hành vi thay đổi | Artifact cụ thể | Nhiều artifacts |

---

## 📁 Files Trong Thư Mục Này

| File | Mô tả |
|------|-------|
| `_template.md` | Template mẫu — copy để tạo skill mới |
| `code-review.md` | Review code theo checklist chuẩn |
| `debug-assistant.md` | Hỗ trợ debug step-by-step có cấu trúc |

---

## 🔑 Anatomy Của Một Skill

```
Skill = Input Context + Execution Steps + Expected Output
```

**Input Context**: Những gì agent cần biết trước khi bắt đầu
```
- Code snippet / file path
- Ngôn ngữ lập trình
- Mục tiêu cụ thể
```

**Execution Steps**: Các bước thực hiện theo thứ tự
```
1. Phân tích input
2. Xử lý theo tiêu chí
3. Format kết quả
4. Kiểm tra lại
```

**Expected Output**: Mô tả chính xác kết quả trả về
```
- Format (markdown, json, prose...)
- Nội dung phải có
- Nội dung không được có
```

---

## ✍️ Hướng Dẫn Viết Skill (How to Write a Skill)

### Bước 1: Copy template
```bash
cp skills/_template.md skills/ten-skill-moi.md
```

### Bước 2: Xác định rõ boundary
Trước khi viết, hỏi:
- Skill này làm **đúng một việc** không?
- Input **có thể liệt kê đầy đủ** không?
- Output có **định dạng cố định** không?

### Bước 3: Viết steps đủ cụ thể

**✅ Viết step tốt:**
```markdown
**Bước 2**: Kiểm tra naming convention
- Biến/hàm dùng camelCase → nếu vi phạm, ghi vào danh sách issues
- Class dùng PascalCase → nếu vi phạm, ghi vào danh sách issues
```

**❌ Tránh:**
```markdown
**Bước 2**: Kiểm tra code quality
- Xem code có tốt không
```

---

## 🚀 Cách Invoke Skill (How to Invoke)

### Cách 1: Paste nội dung file vào chat
```
[Đọc nội dung sau và thực hiện skill này:]
---
<paste nội dung skill.md>
---
Input: <code/file của bạn>
```

### Cách 2: Dùng đường dẫn file (nếu tool hỗ trợ)
```
Thực hiện skill trong file skills/code-review.md với file src/utils.ts
```

### Cách 3: Tham chiếu tên skill
```
Dùng skill "Code Review" để review PR này: [link]
```

---

## 🏷️ Tổ Chức Skills Theo Domain

Khi số lượng skills tăng, nên tổ chức thành subdirectory:

```
skills/
├── coding/
│   ├── code-review.md
│   ├── write-unit-tests.md
│   └── refactor-guide.md
├── documentation/
│   ├── write-readme.md
│   └── api-doc-generator.md
└── project-management/
    ├── estimate-task.md
    └── write-user-story.md
```

> [!NOTE]
> Chỉ tạo subdirectory khi có **từ 5 skills trở lên** trong một domain. Tránh over-organize sớm.

---

## ⚠️ Lưu Ý Quan Trọng

> [!TIP]
> Một skill nên hoàn thành được trong **một lần chat**. Nếu cần nhiều lần trao đổi phức tạp, cân nhắc tạo workflow thay thế.

> [!WARNING]
> Tránh viết skill quá generic (ví dụ: "improve code"). Skills tốt nhất là những skill có thể **đánh giá kết quả một cách khách quan**.

---

*Xem template tại [`_template.md`](./_template.md)*
