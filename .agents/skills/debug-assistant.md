---
id: skill-debug-assistant
name: "Debug Assistant"
tags: [coding, debugging, troubleshooting, problem-solving]
version: "1.0.0"
created: 2026-06-08
updated: 2026-06-08
author: "Personal"
estimated_time: "~20-60 phút"
---

# Debug Assistant

> Hỗ trợ debug lỗi một cách có hệ thống: từ phân tích triệu chứng, tìm nguyên nhân gốc rễ,
> đến đề xuất fix và cách verify.  
> Dùng khi gặp bug không rõ nguyên nhân, error message khó hiểu, hoặc behavior kỳ lạ.

---

## 🎯 Mục Đích (Purpose)

Debug theo kiểu "thử random" rất tốn thời gian và dễ gây ra bugs mới.
Skill này áp dụng phương pháp debug có cấu trúc: reproduce → isolate → identify root cause → fix → verify.
Giúp agent không đoán mò mà suy luận từ evidence cụ thể.

---

## 📥 Input Cần Có (Required Inputs)

### Bắt Buộc (Required)
- `error_description`: Mô tả bug — error message, stack trace, hoặc behavior không mong muốn
- `expected_behavior`: Behavior mong muốn là gì
- `actual_behavior`: Behavior thực tế đang xảy ra

### Tùy Chọn (Optional)
- `code_snippet`: Đoạn code liên quan đến bug
  - Mặc định: Suy luận từ error message
- `environment`: Môi trường xảy ra bug (dev/staging/prod, OS, runtime version)
  - Mặc định: Development environment
- `reproduction_steps`: Các bước để reproduce bug
  - Mặc định: Suy luận nếu có thể
- `already_tried`: Những gì đã thử nhưng không work
  - Mặc định: Không có

---

## ⚙️ Các Bước Thực Hiện (Execution Steps)

**Bước 1: Phân Tích Triệu Chứng (Symptom Analysis)**
- Đọc và hiểu error message / stack trace
- Xác định: bug xảy ra ở layer nào? (UI, business logic, data, network, infra)
- Xác định: bug deterministic (luôn xảy ra) hay intermittent (thỉnh thoảng)?
- List ra các "symptoms" quan sát được

**Bước 2: Tạo Hypotheses**
- Đề xuất 2-4 nguyên nhân có thể (root causes), từ likely nhất đến ít likely nhất
- Với mỗi hypothesis, giải thích logic tại sao nó có thể gây ra symptom đã quan sát
- Không loại bỏ hypothesis nào quá sớm

**Bước 3: Thiết Kế Investigation Plan**
- Với mỗi hypothesis, đề xuất cách test/verify (không phải fix ngay)
- Ưu tiên investigation từ nhanh nhất / ít risk nhất
- Đề xuất các debugging techniques phù hợp:
  - Thêm logging/breakpoints ở đâu
  - Viết test case để isolate
  - Check network requests / database queries
  - Binary search trong code để narrow down

**Bước 4: Xác Định Root Cause**
- Dựa trên investigation plan, xác định root cause (sau khi user confirm evidence)
- Phân biệt: immediate cause vs root cause
  - Immediate: "Function X trả về null"
  - Root cause: "Database connection timeout do connection pool bị exhausted"

**Bước 5: Đề Xuất Fix**
- Đề xuất fix cho root cause, không phải symptom
- Cung cấp code cụ thể nếu có thể
- Cân nhắc: quick fix (patch) vs proper fix (refactor) và trade-offs
- List potential side effects của fix

**Bước 6: Hướng Dẫn Verify**
- Mô tả cách verify bug đã được fix
- Đề xuất test cases cần chạy
- Các regression risks cần monitor

---

## 📤 Output Mong Đợi (Expected Output)

### Format
Markdown có structure rõ ràng, chia theo sections

### Cấu Trúc Output

```markdown
## 🐛 Debug Report: [Tên bug ngắn gọn]

### 📍 Symptom Analysis
- **Bug Layer**: [UI / Business Logic / Data / Network / Infra]
- **Frequency**: [Deterministic / Intermittent]
- **Symptoms observed**:
  - [Symptom 1]
  - [Symptom 2]

---

### 🔍 Hypotheses (sắp xếp theo likelihood)

**Hypothesis 1** (Most likely): [Tên giả thuyết]
- **Reasoning**: [Tại sao hypothesis này match với symptoms]
- **How to verify**: [Cách test — không phải fix]

**Hypothesis 2**: [Tên]
- **Reasoning**: [...]
- **How to verify**: [...]

---

### 🗺️ Investigation Plan

**Step 1** (5 phút): [Hành động — ví dụ: "Check logs tại timestamp X"]
**Step 2** (10 phút): [Hành động]
**Step 3** (nếu cần): [Hành động]

---

### 🎯 Root Cause
[Sau khi có evidence từ investigation]

**Root Cause**: [Mô tả chính xác nguyên nhân gốc rễ]

---

### 🔧 Proposed Fix

**Quick Fix** (nếu cần giải quyết ngay):
[Code hoặc mô tả quick fix]

**Proper Fix** (recommended):
[Code hoặc mô tả proper fix]

**Trade-offs**:
- Quick fix: [Ưu/nhược điểm]
- Proper fix: [Ưu/nhược điểm]

---

### ✅ Verification Steps
1. [Bước verify 1]
2. [Bước verify 2]
3. [Regression tests cần chạy]
```

---

## 💡 Ví Dụ Sử Dụng (Usage Examples)

### Ví dụ 1: NullPointerException đơn giản

**Input của bạn:**
```
Error: Cannot read properties of undefined (reading 'name')
  at UserProfile.tsx:42

Expected: Hiển thị tên user
Actual: Trang crash với error trên

Code:
const UserProfile = ({ userId }) => {
  const [user, setUser] = useState();
  
  useEffect(() => {
    fetchUser(userId).then(data => setUser(data));
  }, [userId]);
  
  return <div>{user.name}</div>; // line 42
};
```

**Output của agent:**
```markdown
## 🐛 Debug Report: UserProfile crash khi render

### 📍 Symptom Analysis
- **Bug Layer**: UI (React component)
- **Frequency**: Deterministic (luôn xảy ra khi component mount)
- **Symptoms**: `user` là `undefined` khi render lần đầu

### 🔍 Hypotheses

**Hypothesis 1** (Most likely): Race condition — async data fetch chưa xong mà component đã render
- **Reasoning**: `useState()` không có initial value → `user` = `undefined`.
  `useEffect` chạy sau render đầu tiên → render đầu tiên bị crash trước khi data về.
- **How to verify**: Thêm `console.log('user:', user)` trước return để confirm.

### 🎯 Root Cause
Missing loading state — component cố render `user.name` trước khi data fetch xong.

### 🔧 Proposed Fix

```tsx
const UserProfile = ({ userId }) => {
  const [user, setUser] = useState(null); // explicit null initial state
  
  useEffect(() => {
    fetchUser(userId).then(data => setUser(data));
  }, [userId]);
  
  if (!user) return <div>Loading...</div>; // guard clause
  
  return <div>{user.name}</div>;
};
```

### ✅ Verification Steps
1. Loading state hiển thị khi component mount
2. Tên user hiển thị sau khi fetch xong
3. Không có console errors
```

---

## 🔗 Skills & Rules Liên Quan

- Skills: [`code-review`](./code-review.md) — Review code sau khi fix
- Workflows: [`bug-investigation`](../workflows/bug-investigation.md) — Workflow toàn bộ quy trình fix bug

---

## ⚠️ Lưu Ý & Hạn Chế (Notes & Limitations)

- **Cần càng nhiều context càng tốt**: Stack trace đầy đủ, reproduction steps, và code liên quan giúp chẩn đoán chính xác hơn rất nhiều.
- **Intermittent bugs khó hơn**: Với bugs không ổn định, agent có thể cần nhiều vòng investigation hơn.
- **Root cause analysis**: Agent có thể propose wrong hypothesis — cần user confirm evidence từng bước.
- **Không thể chạy code**: Agent không thể tự execute code, nên investigation plan cần user thực hiện và report back kết quả.

---

## 📝 Lịch Sử Thay Đổi (Changelog)

| Version | Ngày | Thay đổi |
|---------|------|---------|
| 1.0.0 | 2026-06-08 | Khởi tạo |
