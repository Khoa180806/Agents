---
id: rule-web-ui-functional-testing
name: "Web UI Functional Testing Standards"
scope: global
tags: [testing, qa, web-ui, functional-testing]
version: "1.0.0"
created: 2026-06-15
updated: 2026-06-15
author: "Antigravity"
---

# Web UI Functional Testing Standards

> Tiêu chuẩn thiết kế kịch bản và thực hiện kiểm thử chức năng trực tiếp trên giao diện website (Functional Web UI Testing).
> Giúp team tester dễ dàng thực thi, ghi chép kết quả và xác minh tính đúng đắn của các tính năng mới vừa phát triển.

---

## 🎯 Mục Đích (Purpose)

Kiểm thử chức năng trên giao diện (Web UI Functional Testing) là bước cốt lõi để đảm bảo hệ thống chạy đúng logic nghiệp vụ từ góc nhìn của người dùng cuối. 
Quy chuẩn này được thiết lập để:
- Định hình cấu trúc một Test Case/Scenario rõ ràng, dễ hiểu cho mọi tester.
- Tập trung vào các hành động thực tế của người dùng trên UI (click, nhập liệu, điều hướng).
- Giảm thiểu việc bỏ sót lỗi logic nghiêm trọng khi release tính năng mới.

---

## 📋 Quy Tắc Chi Tiết (Rules)

### 1. Cấu Trúc Bắt Buộc Của Một Test Case
Mỗi kịch bản kiểm thử chức năng trên Web UI phải chứa đầy đủ các trường sau:
- **Test Case ID**: Định danh duy nhất (ví dụ: `TC_AUTH_01`, `TC_CART_05`).
- **Tên Test Case**: Mô tả ngắn gọn mục tiêu kiểm thử.
- **Điều Kiện Tiên Quyết (Prerequisites)**: Trạng thái hệ thống/tài khoản trước khi thực hiện (ví dụ: "Đã đăng nhập tài khoản Admin", "Giỏ hàng đang trống").
- **Các Bước Thực Hiện (Test Steps)**: Các bước tương tác tuần tự trên UI (Click, Type, Hover...).
- **Kết Quả Mong Đợi (Expected Result)**: Trạng thái UI và dữ liệu thay đổi mong đợi sau khi thực hiện các bước.
- **Kết Quả Thực Tế (Actual Result)**: Ghi nhận thực tế khi test (chỉ điền khi thực thi).
- **Trạng Thái (Status)**: `PASS` | `FAIL` | `BLOCKED` (chỉ điền khi thực thi).

### 2. Các Phân Nhóm Kịch Bản Cần Có (Test Scenarios Categorization)
Khi viết test case cho một tính năng vừa hoàn thành, PHẢI bao gồm cả 3 nhóm:
1. **Positive Cases (Kịch bản thông thường)**: Người dùng nhập đúng, thực hiện đúng quy trình chuẩn (Happy Path).
2. **Negative Cases (Kịch bản lỗi/Validation)**: Người dùng nhập sai định dạng, bỏ trống trường bắt buộc, hoặc thực hiện sai luồng nhằm kiểm tra thông báo lỗi trên UI.
3. **Edge Cases (Kịch bản biên/Đặc biệt)**: Các tình huống ít gặp nhưng có thể xảy ra (ví dụ: nhấn nút Submit nhiều lần liên tiếp, nhập chuỗi ký tự quá dài, mất kết nối mạng giữa chừng, giỏ hàng đạt giới hạn số lượng).

### 3. Quy Tắc Viết Bước Thực Hiện (Test Steps Writing)
- Phải dùng ngôn ngữ hành động trên UI rõ ràng: "Click vào nút X", "Nhập 'abc' vào ô Y", "Chọn option Z trong dropdown".
- Không viết chung chung: "Đăng nhập vào hệ thống" -> Phải viết: "1. Nhập username vào ô..., 2. Nhập password vào ô..., 3. Click nút Đăng nhập".
- Mọi thông báo lỗi (Error Message) mong đợi phải được mô tả chính xác nội dung hiển thị trên UI.

---

## ✅ Ví Dụ Đúng (Correct Examples)

```markdown
### Scenario: Đăng nhập hệ thống (User Login)

#### TC_LOGIN_01: Đăng nhập thành công với tài khoản hợp lệ (Positive Case)
- **Prerequisites**: Tài khoản `testuser@example.com` đã được kích hoạt. Người dùng đang ở trang đăng nhập `/login`.
- **Test Steps**:
  1. Nhập `testuser@example.com` vào trường "Email".
  2. Nhập `Password123` vào trường "Mật khẩu".
  3. Click vào nút "Đăng nhập".
- **Expected Result**:
  - Hệ thống chuyển hướng người dùng về trang Dashboard `/dashboard`.
  - Hiển thị pop-up thông báo thành công: "Đăng nhập thành công!".
  - Header hiển thị avatar và tên người dùng "Test User".

#### TC_LOGIN_02: Hiển thị lỗi khi để trống mật khẩu (Negative Case)
- **Prerequisites**: Người dùng đang ở trang đăng nhập `/login`.
- **Test Steps**:
  1. Nhập `testuser@example.com` vào trường "Email".
  2. Để trống trường "Mật khẩu".
  3. Click vào nút "Đăng nhập".
- **Expected Result**:
  - Hệ thống không chuyển hướng trang.
  - Trường "Mật khẩu" hiển thị viền đỏ và có thông báo lỗi bên dưới: "Mật khẩu không được để trống".
```

---

## ❌ Ví Dụ Sai (Incorrect Examples)

```markdown
<!-- ❌ BAD: Viết bước quá chung chung, không có ID rõ ràng, không phân biệt Prerequisites và Steps -->
Test đăng nhập:
Vào web rồi đăng nhập bằng tài khoản test. Nếu vào được trang chủ thì là đúng, không vào được là sai.
Nếu nhập sai pass thì phải báo lỗi.
```

```markdown
<!-- ❌ BAD: Thiếu Expected Result cụ thể, không chỉ rõ thông báo lỗi là gì, test case quá gộp -->
#### TC_01: Test điền form liên hệ
- Các bước: Nhập thông tin vào form liên hệ rồi ấn gửi.
- Expected: Gửi thành công hoặc báo lỗi nếu thiếu thông tin.
```

---

## 🔄 Hành Động Khi Vi Phạm (On Violation)

Nếu phát hiện kịch bản test được viết vi phạm các quy tắc trên:
- [ ] Yêu cầu làm rõ các bước cụ thể (hành động Click/Type/Select...).
- [ ] Bổ sung các kịch bản lỗi (Negative) và kịch bản biên (Edge cases) nếu bộ test case chỉ có Happy Path.
- [ ] Điều chỉnh Expected Result để chỉ rõ trạng thái thay đổi trên UI (thông báo lỗi, chuyển hướng trang, đổi màu sắc viền...).

---

## 🚫 Ngoại Lệ (Exceptions)

- **Quick Smoke Test**: Trong trường hợp cần test nhanh một hotfix cực kỳ khẩn cấp, có thể sử dụng checklist các luồng chính dạng bullet-point thay vì viết đầy đủ cấu trúc Test Case chi tiết.

---

## 🔗 Tham Chiếu (References)

- Kỹ năng tạo kịch bản: [`generate-web-ui-functional-tests.md`](../skills/generate-web-ui-functional-tests.md)
- Quy trình phối hợp: [`web-ui-functional-testing-workflow.md`](../workflows/web-ui-functional-testing-workflow.md)

---

## 📝 Lịch Sử Thay Đổi (Changelog)

| Version | Ngày | Thay đổi |
|---------|------|---------|
| 1.0.0 | 2026-06-15 | Khởi tạo tài liệu quy chuẩn kiểm thử chức năng giao diện web |
