---
id: skill-document-reading
name: "Document Reading and Parsing Skill"
tags: [document, reading, parsing, docx, xlsx, md]
version: "1.0.0"
created: 2026-06-11
updated: 2026-06-11
author: "Personal"
estimated_time: "~10-20 phút"
---

# Document Reading and Parsing Skill

> Kỹ năng hướng dẫn AI Assistant sử dụng các phương pháp kỹ thuật để đọc, parse và trích xuất thông tin có cấu trúc từ các file tài liệu `.docx`, `.xlsx`, `.md`...

---

## 🎯 Mục Đích (Purpose)

Giúp AI Assistant xử lý một cách có hệ thống các tài liệu dự án bằng cách sử dụng các lệnh hoặc script phù hợp, tránh tình trạng đọc file thô sơ làm mất định dạng hoặc gây lỗi bộ nhớ ngữ cảnh khi đối mặt với các tài liệu phức tạp hoặc dung lượng lớn.

---

## 📥 Input Cần Có (Required Inputs)

### Bắt Buộc (Required)
- `file_path`: Đường dẫn tuyệt đối hoặc tương đối của file tài liệu.
- `file_type`: Định dạng file cần xử lý: `docx` | `xlsx` | `md` | `csv`.

### Tùy Chọn (Optional)
- `sheet_name`: Tên Sheet cần đọc (chỉ áp dụng đối với file `xlsx`).
  - Mặc định: Đọc Sheet đầu tiên.
- `range`: Phạm vi dải ô cần đọc, ví dụ `A1:D50` (chỉ áp dụng đối với file `xlsx`).
  - Mặc định: Đọc toàn bộ vùng dữ liệu có nội dung.
- `chunk_size`: Số dòng tối đa cho mỗi lần đọc để chia nhỏ file lớn.
  - Mặc định: `100` dòng cho excel, `1000` từ cho word.
- `encoding`: Bộ mã hóa ký tự (chỉ áp dụng cho text-based files).
  - Mặc định: `utf-8`.

---

## ⚙️ Các Bước Thực Hiện (Execution Steps)

**Bước 1: Phân loại và Kiểm tra Tệp tin**
- Kiểm tra xem file có tồn tại ở đường dẫn `file_path` hay không bằng cách sử dụng các lệnh hệ thống hoặc kiểm tra trong workspace.
- Dựa vào đuôi mở rộng của file để chọn phương thức xử lý thích hợp.

**Bước 2: Lựa chọn Phương pháp Trích xuất**
- **Đối với file Markdown (.md)**:
  - Sử dụng trực tiếp công cụ xem file (ví dụ `view_file`) để đọc nội dung văn bản.
- **Đối với file Word (.docx)**:
  - Nếu có Python trong môi trường, viết một script nhỏ sử dụng thư viện `python-docx` để đọc text và bảng biểu.
  - Hoặc nếu không có thư viện chuyên dụng, sử dụng các công cụ dòng lệnh phù hợp hoặc đề xuất Developer cung cấp file text thô.
- **Đối với file Excel (.xlsx)**:
  - Sử dụng Python với thư viện `pandas` hoặc `openpyxl` để đọc dữ liệu.
  - Cấu hình chỉ đọc các cột/dòng cần thiết hoặc chỉ định `range` để giới hạn dữ liệu.

**Bước 3: Thực hiện Trích xuất dữ liệu**
- Chạy script trích xuất dữ liệu.
- Trong quá trình chạy, nếu gặp lỗi encoding, chuyển đổi thử sang các encoding khác như `latin-1` hoặc `utf-16`.

**Bước 4: Chuẩn hóa dữ liệu đầu ra**
- Định dạng lại các bảng biểu trích xuất được dưới dạng Markdown Table.
- Giữ nguyên cấu trúc phân cấp (head, sub-head) để duy trì tính logic của tài liệu.

**Bước 5: Tạo báo cáo phân tích**
- Tổng hợp các thông tin cốt lõi trích xuất được.
- Đưa ra bản tóm tắt cấu trúc tài liệu cho Developer xem xét.

---

## 📤 Output Mong Đợi (Expected Output)

### Format
Markdown sạch sẽ, có cấu trúc rõ ràng.

### Cấu Trúc Output
```markdown
## 📄 Báo Cáo Trích Xuất Tài Liệu: [Tên File]

**Định dạng**: [docx / xlsx / md]  
**Đường dẫn**: [file_path]  
**Tóm tắt**: [Mô tả ngắn gọn nội dung tài liệu]

---

### 🗂️ Cấu Trúc Tài Liệu
- [Liệt kê các Heading chính hoặc các Sheets hiện có]

### 📊 Dữ Liệu Chi Tiết Trích Xuất

#### 1. [Tên Mục / Tên Sheet]
[Nội dung văn bản hoặc Bảng dữ liệu Markdown]

#### 2. [Tên Mục kế tiếp]
...

---

### 🔑 Các Thông Tin Quan Trọng (Key Takeaways)
- [Cấu hình quan trọng, quy tắc nghiệp vụ, lưu ý đặc biệt]
```

---

## 💡 Ví Dụ Sử Dụng (Usage Examples)

### Ví dụ: Đọc file cấu hình Excel `system_config.xlsx`
**Input:**
```json
{
  "file_path": "d:/HocTap/Agent/docs/system_config.xlsx",
  "file_type": "xlsx",
  "sheet_name": "DatabaseConfig"
}
```

**Script Python chạy ngầm (Agent thực thi qua run_command):**
```python
import pandas as pd
df = pd.read_excel('d:/HocTap/Agent/docs/system_config.xlsx', sheet_name='DatabaseConfig')
print(df.to_markdown())
```

**Output của Agent:**
```markdown
## 📄 Báo Cáo Trích Xuất Tài Liệu: system_config.xlsx

**Định dạng**: xlsx  
**Đường dẫn**: d:/HocTap/Agent/docs/system_config.xlsx

### 📊 Dữ Liệu Chi Tiết Trích Xuất (Sheet: DatabaseConfig)

| Parameter | Value | Description |
| :--- | :--- | :--- |
| `db_host` | `localhost` | Địa chỉ IP Database server |
| `db_port` | `5432` | Cổng kết nối PostgreSQL |

### 🔑 Các Thông Tin Quan Trọng
- Cấu hình kết nối mặc định sử dụng PostgreSQL.
```

---

## 🔗 Skills & Rules Liên Quan

- Rules: [`document-reading`](../rules/document-reading.md)
- Workflows: [`document-reading-workflow`](../workflows/document-reading-workflow.md)

---

## ⚠️ Lưu Ý & Hạn Chế (Notes & Limitations)

- **Thư viện phụ thuộc**: Đọc docx/xlsx qua Python yêu cầu môi trường có cài đặt `pandas`, `openpyxl`, `python-docx` hoặc các thư viện tương đương.
- **Tránh tràn context**: Đối với tệp tin văn bản dài, chia nhỏ nội dung thành các chunk nhỏ hơn (mỗi chunk khoảng 1000-2000 từ) để phân tích lần lượt.

---

## 📝 Lịch Sử Thay Đổi (Changelog)

| Version | Ngày | Thay đổi |
|---------|------|---------|
| 1.0.0 | 2026-06-11 | Khởi tạo |
