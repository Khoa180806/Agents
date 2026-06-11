---
id: rule-document-reading
name: "Document Reading & Parsing Guide"
scope: global
tags: [document, reading, parsing, docx, xlsx, md]
version: "1.0.0"
created: 2026-06-11
updated: 2026-06-11
author: "Personal"
---

# Document Reading & Parsing Guide

> Bộ quy tắc hướng dẫn AI Assistant cách tiếp cận, đọc và trích xuất thông tin một cách chuẩn xác từ các file tài liệu phổ biến như `.docx`, `.xlsx`, `.md`... trong dự án.

---

## 🎯 Mục Đích (Purpose)

Khi làm việc với các tài liệu dự án (specs, báo cáo, file dữ liệu), việc đọc không đúng cách dễ dẫn đến bỏ sót thông tin, mất cấu trúc dữ liệu quan trọng (như bảng biểu, danh sách), hoặc thậm chí gây tràn ngữ cảnh (context window). Rule này được thiết lập để đảm bảo AI Assistant:
1. Đọc và phân tích đúng định dạng cấu trúc của từng loại file.
2. Trích xuất thông tin trung thực, chính xác và có tổ chức.
3. Tối ưu hóa việc sử dụng tài nguyên ngữ cảnh bằng cách đọc có chọn lọc.

---

## 📋 Quy Tắc Chi Tiết (Rules)

### 1. Quy Tắc Đọc File Markdown (.md)
1. **Phân tích cấu trúc Heading**: Đọc và hiểu phân cấp nội dung thông qua `#`, `##`, `###`.
2. **Xử lý Front Matter**: Nếu file có phần Front Matter nằm giữa hai cặp đường kẻ `---` ở đầu file, bắt buộc phải parse phần này trước để nắm các thông tin meta (id, tags, version, v.v.).
3. **Giữ nguyên khối mã (Code Blocks)**: Tuyệt đối không thay đổi hoặc lược bỏ code blocks khi trích dẫn tài liệu.
4. **Bảng biểu (Tables) & Danh sách (Lists)**: Đọc kỹ cấu trúc dòng của bảng và các mục phân cấp để tránh hiểu sai quan hệ dữ liệu.

### 2. Quy Tắc Đọc File Word (.docx)
1. **Trích xuất Paragraphs**: Đọc toàn bộ các đoạn văn bản thô theo đúng trình tự xuất hiện từ trên xuống dưới.
2. **Bảo toàn Tables**: Đối với các dữ liệu dạng bảng trong docx, phải trích xuất và ánh xạ thành định dạng bảng Markdown tương ứng để giữ nguyên cấu trúc cột/hàng.
3. **Nhận diện Text Styles**: Chú ý đến các đoạn chữ in đậm (Bold), in nghiêng (Italic) hoặc tô màu nổi bật vì chúng thường chứa các định nghĩa, thuật ngữ cốt lõi hoặc cảnh báo quan trọng.

### 3. Quy Tắc Đọc File Excel (.xlsx)
1. **Tổng quan Workbook**: Trước khi đọc chi tiết, cần xác định danh sách các Sheets hiện có trong file.
2. **Định dạng dữ liệu dòng/cột**: Ánh xạ rõ ràng header (dòng đầu tiên) với dữ liệu tương ứng bên dưới.
3. **Tránh tải thừa dữ liệu**: Với các file excel lớn (> 1000 dòng), không được đọc toàn bộ file một lần. Phải áp dụng kỹ thuật đọc theo dải ô (Range-based reading) hoặc phân trang (chunking).
4. **Công thức (Formulas) và Giá trị (Values)**: Phân biệt rõ giữa công thức tính toán và giá trị thực tế hiển thị trên ô dữ liệu.

### 4. Nguyên Tắc Chung cho Mọi Định Dạng
1. **Tính trung thực (Accuracy)**: Tuyệt đối không tự suy diễn hoặc bịa đặt (hallucinate) dữ liệu bị khuyết thiếu trong tài liệu. Nếu tài liệu mập mờ hoặc thiếu thông tin, phải báo cáo lại cho Developer.
2. **Encoding**: Đảm bảo đọc file ở định dạng mã hóa đúng (mặc định là `UTF-8` cho text-based files).
3. **Bảo mật**: Không được lưu trữ, ghi nhớ hoặc chia sẻ bất kỳ dữ liệu nhạy cảm nào (API keys, passwords, thông tin khách hàng) tìm thấy trong tài liệu.

---

## ✅ Ví Dụ Đúng (Correct Examples)

### Ví dụ 1: Parse và chuyển đổi bảng từ file .docx
*Dữ liệu bảng trong file `.docx` được Agent chuyển đổi về Markdown trong báo cáo:*
| Tên tham số | Kiểu dữ liệu | Ý nghĩa |
| :--- | :--- | :--- |
| `max_connections` | Integer | Số kết nối tối đa cho phép |

### Ví dụ 2: Đọc file Excel lớn bằng cách giới hạn Range
```python
# Đúng: Chỉ đọc sheet 'Config' và giới hạn số dòng cần thiết để tránh tràn ngữ cảnh
data = read_excel_file(path, sheet_name='Config', range='A1:C50')
```

---

## ❌ Ví Dụ Sai (Incorrect Examples)

### Ví dụ 1: Bỏ qua cấu trúc bảng trong tài liệu
*Tài liệu gốc có bảng dữ liệu cấu hình nhưng Agent chỉ đọc text thô làm mất liên kết:*
> "Tham số max_connections là Integer Số kết nối tối đa cho phép" -> ❌ Sai vì làm mất cấu trúc hàng cột, dễ gây hiểu nhầm khi có nhiều tham số.

### Ví dụ 2: Đọc trực tiếp toàn bộ file Excel 100MB vào context
> ❌ Sai vì gây lãng phí tokens nghiêm trọng và dẫn đến lỗi tràn bộ nhớ ngữ cảnh.

---

## 🔄 Hành Động Khi Vi Phạm (On Violation)

Nếu phát hiện việc phân tích tài liệu bị sai lệch hoặc thiếu sót:
- [ ] Dừng quá trình xử lý hiện tại.
- [ ] Xác định phần dữ liệu bị mất cấu trúc hoặc bị đọc thiếu.
- [ ] Sử dụng các tool đọc file chuyên dụng để đọc lại vùng dữ liệu đó.
- [ ] Báo cáo lại cho Developer cấu trúc chính xác của dữ liệu.

---

## 🚫 Ngoại Lệ (Exceptions)

- Đối với các file tài liệu quá cũ hoặc bị lỗi định dạng (corrupted) không thể dùng tool để parse: AI Assistant được phép đề xuất Developer chuyển đổi file sang dạng văn bản thuần `.txt` hoặc `.csv` trước khi xử lý.

---

## 🔗 Tham Chiếu (References)

- Kỹ năng xử lý: [`document-reading-skill`](../skills/document-reading-skill.md)
- Quy trình: [`document-reading-workflow`](../workflows/document-reading-workflow.md)

---

## 📝 Lịch Sử Thay Đổi (Changelog)

| Version | Ngày | Thay đổi |
|---------|------|---------|
| 1.0.0 | 2026-06-11 | Khởi tạo |
