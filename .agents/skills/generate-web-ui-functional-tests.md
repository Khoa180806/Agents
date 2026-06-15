---
id: skill-generate-web-ui-functional-tests
name: "Generate Web UI Functional Test Cases"
tags: [testing, qa, web-ui, functional-testing]
version: "1.0.0"
created: 2026-06-15
updated: 2026-06-15
author: "Antigravity"
estimated_time: "~20 phút"
---

# Generate Web UI Functional Test Cases

> Hướng dẫn chi tiết giúp AI Agent phân tích các tính năng mới vừa làm để tự động viết ra kịch bản kiểm thử chức năng trên giao diện (Web UI) cho team tester.

---

## 🎯 Mục Đích (Purpose)

Đảm bảo AI Agent có thể tạo ra các bộ kịch bản kiểm thử (test scenarios & test cases) đầy đủ, chính xác, bám sát các khía cạnh của một tính năng vừa được phát triển. 
Tester chỉ cần đọc tài liệu output này là có thể trực tiếp thực thi test trên website mà không cần phải tự suy đoán các bước.

---

## 📥 Input Cần Có (Required Inputs)

### Bắt Buộc (Required)
- `feature_description`: Mô tả chi tiết tính năng vừa được triển khai hoặc danh sách các thay đổi vừa làm (PR description, ticket requirements).
- `ui_elements`: Mô tả hoặc hình ảnh về các thành phần giao diện mới (inputs, buttons, tables, links...).

### Tùy Chọn (Optional)
- `user_roles`: Các vai trò người dùng có quyền sử dụng tính năng này (ví dụ: Guest, Member, Admin).
- `mock_data`: Dữ liệu mẫu dùng để test (username, password, mẫu input đúng/sai).

---

## ⚙️ Các Bước Thực Hiện (Execution Steps)

**Bước 1: Phân tích Tính Năng & Luồng Nghiệp Vụ (Analyze Feature & Flow)**
- Đọc kỹ mô tả tính năng để xác định:
  - Ai là người sử dụng tính năng này?
  - Điểm bắt đầu (URL nào) và điểm kết thúc của luồng (User Flow).
  - Có các điều kiện ràng buộc (validation) nào trên form/input không?

**Bước 2: Lập Danh Sách Scenarios Phân Loại (Identify Test Scenarios)**
- Phân nhóm các trường hợp kiểm thử thành 3 loại:
  - **Happy Path (Positive)**: Các trường hợp sử dụng thành công tiêu chuẩn.
  - **Validation & Error Handing (Negative)**: Các trường hợp nhập lỗi, thiếu thông tin để kiểm tra validation thông báo trên màn hình.
  - **Edge Cases**: Các trường hợp biên, các lỗi mạng, bấm submit liên tục, ký tự đặc biệt, độ dài chuỗi...

**Bước 3: Viết Chi Tiết Test Cases Cho Từng Scenario (Write Detailed Test Cases)**
- Đối với mỗi Scenario, viết chi tiết các trường theo quy chuẩn [`web-ui-functional-testing-rules.md`](../rules/web-ui-functional-testing-rules.md).
- Đảm bảo các bước thực hiện mô tả rõ hành động tương tác với UI (Click, Type...).
- Đảm bảo Kết quả mong đợi mô tả rõ sự thay đổi giao diện trực quan.

**Bước 4: Soát Xét & Tinh Lọc (Review & Refine)**
- Đọc lại toàn bộ kịch bản để đảm bảo không viết chung chung.
- Đảm bảo tester có thể chạy test thủ công dễ dàng chỉ bằng cách đọc các bước.

---

## 📤 Output Mong Đợi (Expected Output)

### Format
Tài liệu Markdown chứa danh sách kịch bản kiểm thử chi tiết dạng bảng hoặc cấu trúc đề mục rõ ràng.

### Cấu Trúc Output
```markdown
# Kịch Bản Kiểm Thử Tính Năng: [Tên Tính Năng]

## 1. Kịch Bản Thông Thường (Positive Cases / Happy Paths)
... (Danh sách TC)

## 2. Kịch Bản Kiểm Tra Lỗi & Validation (Negative Cases)
... (Danh sách TC)

## 3. Kịch Bản Đặc Biệt & Biên (Edge Cases)
... (Danh sách TC)
```

### Tiêu Chí Chất Lượng
- [ ] 100% test case có ID và phân biệt rõ loại kịch bản (Positive/Negative/Edge).
- [ ] Các bước thực hiện rõ ràng, chỉ rõ nút nào cần click, ô nào cần nhập.
- [ ] Expected Result mô tả rõ kết quả trên UI (ví dụ: thông báo màu xanh/đỏ hiển thị ở đâu, chuyển hướng trang nào).

---

## 💡 Ví Dụ Sử Dụng (Usage Examples)

### Ví dụ: Tạo test case cho tính năng "Quên mật khẩu"

**Input của bạn:**
> Tạo test case cho tính năng "Quên mật khẩu" vừa làm. Giao diện có 1 ô nhập email, 1 nút "Gửi mã reset", nếu gửi thành công thì hiển thị text thông báo "Chúng tôi đã gửi link đặt lại mật khẩu về email của bạn". Email phải đúng định dạng, nếu để trống hoặc sai định dạng thì báo lỗi.

**Output của Agent:**
```markdown
# Kịch Bản Kiểm Thử Tính Năng: Quên Mật Khẩu (Forgot Password)

## 1. Kịch Bản Thông Thường (Positive Cases)

### TC_FORGOT_01: Yêu cầu reset mật khẩu thành công với email hợp lệ
- **Prerequisites**: Tài khoản email `user@example.com` đã tồn tại trên hệ thống. Người dùng đang ở trang Quên mật khẩu `/forgot-password`.
- **Test Steps**:
  1. Nhập `user@example.com` vào trường "Email".
  2. Click vào nút "Gửi mã reset".
- **Expected Result**:
  - Hệ thống hiển thị biểu tượng loading ngắn.
  - Hiển thị thông báo thành công màu xanh lá: "Chúng tôi đã gửi link đặt lại mật khẩu về email của bạn".
  - Trường nhập email và nút "Gửi mã reset" bị ẩn đi hoặc disabled.

## 2. Kịch Bản Kiểm Tra Lỗi & Validation (Negative Cases)

### TC_FORGOT_02: Hiển thị lỗi khi để trống email
- **Prerequisites**: Người dùng đang ở trang `/forgot-password`.
- **Test Steps**:
  1. Để trống trường "Email".
  2. Click vào nút "Gửi mã reset".
- **Expected Result**:
  - Không gửi yêu cầu reset mật khẩu.
  - Trường "Email" hiển thị thông báo lỗi màu đỏ bên dưới: "Email không được để trống".

### TC_FORGOT_03: Hiển thị lỗi khi nhập sai định dạng email
- **Prerequisites**: Người dùng đang ở trang `/forgot-password`.
- **Test Steps**:
  1. Nhập `user_invalid_email` vào trường "Email".
  2. Click vào nút "Gửi mã reset".
- **Expected Result**:
  - Hệ thống báo lỗi ngay lập tức mà không gửi request lên server.
  - Hiển thị thông báo lỗi: "Vui lòng nhập đúng định dạng email (ví dụ: name@domain.com)".

### TC_FORGOT_04: Gửi mã reset với email chưa đăng ký tài khoản
- **Prerequisites**: Email `unregistered@example.com` chưa đăng ký trên hệ thống. Người dùng đang ở trang `/forgot-password`.
- **Test Steps**:
  1. Nhập `unregistered@example.com` vào trường "Email".
  2. Click vào nút "Gửi mã reset".
- **Expected Result**:
  - Để bảo mật, hệ thống vẫn hiển thị thông báo thành công: "Chúng tôi đã gửi link đặt lại mật khẩu về email của bạn" (hoặc báo lỗi tùy theo business logic thiết kế của dự án).
```

---

## 🔗 Skills & Rules Liên Quan

- Rules: [`web-ui-functional-testing-rules.md`](../rules/web-ui-functional-testing-rules.md)
- Workflows: [`web-ui-functional-testing-workflow.md`](../workflows/web-ui-functional-testing-workflow.md)

---

## ⚠️ Lưu Ý & Hạn Chế (Notes & Limitations)

- **UI thay đổi**: Kịch bản test giao diện phụ thuộc chặt chẽ vào cấu trúc UI thực tế. Khi giao diện đổi thiết kế, các bước kiểm thử cần được cập nhật tương ứng.
- **Dữ liệu test**: Hãy luôn đảm bảo tài khoản test được cung cấp sẵn sàng trước khi tester bắt đầu chạy test.

---

## 📝 Lịch Sử Thay Đổi (Changelog)

| Version | Ngày | Thay đổi |
|---------|------|---------|
| 1.0.0 | 2026-06-15 | Khởi tạo tài liệu kỹ năng sinh kịch bản kiểm thử chức năng web |
