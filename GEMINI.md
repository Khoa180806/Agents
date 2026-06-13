# 📋 GEMINI.md — Bộ Quy Tắc Dự Án (Project Rules)

> Tài liệu này định nghĩa các quy tắc áp dụng cho **toàn bộ dự án**, bao gồm cả AI assistant (Antigravity/Gemini) và developer.
> **Ngôn ngữ**: Song ngữ Việt–Anh. Comments trong code dùng tiếng Anh; giao tiếp với AI và tài liệu nội bộ dùng tiếng Việt.

---

## 🤖 1. Quy Tắc Dành Cho AI Assistant

> Các quy tắc này có **ưu tiên cao nhất** và AI phải tuân theo tuyệt đối.

### 1.1 Nguyên Tắc Chung
- **LUÔN LUÔN** đọc thư mục `.agents/` khi bắt đầu để nắm rõ các quy tắc (rules), kỹ năng (skills) và quy trình (workflows) đã được định nghĩa cho dự án.
- **TỰ ĐỘNG ÁP DỤNG WORKFLOW**: Khi người dùng chọn hoặc chỉ định một workflow cụ thể (trong thư mục `.agents/workflows/`), AI Assistant phải đọc và tuân thủ workflow đó, đồng thời tự động tìm đọc và áp dụng các rules (trong `.agents/rules/`) và skills (trong `.agents/skills/`) được liên kết hoặc tham chiếu bởi workflow đó. Quy định này áp dụng đồng thời với `GEMINI.md`.
- **LUÔN** đưa ra **Implementation Plan** hoặc **Task checklist** trước khi bắt đầu code bất kỳ tính năng nào không tầm thường. Chờ xác nhận từ người dùng.
- **KHÔNG** tự ý xóa, ghi đè, hay thay thế code cũ mà không thông báo rõ ràng.
- **PHẢI** giải thích lý do kỹ thuật cụ thể trước khi thực hiện bất kỳ refactor lớn nào.
- **PHẢI** hỏi người dùng trước khi thay đổi cấu trúc thư mục (folder structure) hoặc kiến trúc tổng thể.
- Ưu tiên giải pháp **đơn giản nhất** có thể hoạt động đúng (nguyên tắc KISS — Keep It Simple, Stupid).
- **KHÔNG** over-engineer: không thêm abstraction layer, design pattern, hay framework nếu chưa có nhu cầu thực sự.

### 1.2 Khi Gợi Ý Code
- Chỉ **đề xuất** thay đổi; không áp đặt. Người dùng là người quyết định cuối cùng.
- Luôn **tuân theo architecture patterns** đã được thiết lập trong dự án.
- Khi có nhiều cách giải quyết, trình bày **trade-offs** của từng cách trước khi đề xuất.
- Giữ nguyên **docstrings và comments** hiện có, trừ khi được yêu cầu thay đổi.
- **LUÔN** chủ động gợi ý commit message tương ứng (tuân thủ định dạng Conventional Commits ở mục 3.2) sau khi đề xuất hoặc thực hiện các thay đổi (thêm/sửa/xóa) file hoặc code.

### 1.3 Ngôn Ngữ Giao Tiếp
- Giao tiếp với người dùng bằng **tiếng Việt**.
- Code, comments trong source code, commit messages dùng **tiếng Anh**.
- Tên biến, hàm, class dùng **tiếng Anh** hoàn toàn.

---

## 🎨 2. Code Style & Formatting

### 2.1 Quy Tắc Chung (Mọi Ngôn Ngữ)
- **Indentation**: 2 spaces cho JS/TS/HTML/CSS; 4 spaces cho Java/C#.
- **Max line length**: 120 ký tự.
- **Trailing commas**: Bật (multiline arrays, objects, parameters).
- **Semicolons**: Bắt buộc trong Java, C#; optional trong JS/TS (theo config dự án).
- Không commit code có **console.log**, **System.out.println**, hay debug statements thừa.

### 2.2 Đặt Tên (Naming Conventions)
| Loại | Convention | Ví dụ |
|------|-----------|-------|
| Variable / Function | camelCase | `getUserById`, `isLoading` |
| Class / Interface / Type | PascalCase | `UserService`, `ApiResponse` |
| Constant | SCREAMING_SNAKE_CASE | `MAX_RETRY_COUNT` |
| File (JS/TS Component) | PascalCase | `UserProfile.tsx` |
| File (JS/TS Utility) | kebab-case | `date-formatter.ts` |
| File (Java/C#) | PascalCase | `UserController.java` |
| CSS Class | kebab-case | `.nav-bar`, `.btn-primary` |
| Database Table | snake_case | `user_profiles`, `order_items` |
| API Endpoint | kebab-case | `/api/user-profiles`, `/api/order-items` |

### 2.3 Comments & Documentation
- Comment giải thích **"Tại sao"** (why), không phải **"Cái gì"** (what) — code đã tự mô tả cái gì.
- TODO comments phải có format: `// TODO(tên): mô tả vấn đề — ngày`
- Xóa code cũ thay vì comment out (dùng git để lấy lại nếu cần).

---

## 🌿 3. Git Workflow

### 3.1 Branch Strategy — Git Flow
```
main          ← Production-ready code. Chỉ merge qua PR được review.
├── develop   ← Integration branch. Tất cả features merge vào đây.
│   ├── feature/[ticket-id]-[mô-tả-ngắn]
│   ├── bugfix/[ticket-id]-[mô-tả-ngắn]
│   └── chore/[mô-tả-ngắn]
├── release/[version]    ← Chuẩn bị release
└── hotfix/[mô-tả-ngắn] ← Fix khẩn cấp trên production
```

### 3.2 Commit Message — Conventional Commits
Format: `<type>(<scope>): <mô tả ngắn gọn bằng tiếng Anh>`

| Type | Khi nào dùng |
|------|-------------|
| `feat` | Thêm tính năng mới |
| `fix` | Sửa lỗi |
| `refactor` | Refactor không thêm tính năng, không sửa lỗi |
| `style` | Thay đổi formatting, không ảnh hưởng logic |
| `docs` | Cập nhật tài liệu |
| `test` | Thêm hoặc sửa tests |
| `chore` | Cập nhật build tools, dependencies... |
| `perf` | Cải thiện performance |
| `ci` | Thay đổi CI/CD pipeline |
| `revert` | Revert commit trước |

**Ví dụ:**
```
feat(auth): add JWT refresh token rotation
fix(api): handle null response from payment gateway
refactor(user-service): extract email validation to shared utility
```

**Quy tắc:**
- Subject line: tối đa 72 ký tự, dùng **imperative mood** ("add" không phải "added").
- Body (nếu có): giải thích *tại sao* thay đổi, không phải *cái gì*.
- Breaking changes: thêm `BREAKING CHANGE:` vào footer.

### 3.3 Pull Request
- **Bắt buộc** có ít nhất 1 reviewer approve trước khi merge.
- PR title theo format Conventional Commits.
- PR nhỏ và focused: không merge PR > 400 dòng thay đổi mà không có lý do.
- Squash merge vào `develop`; merge commit vào `main`.

### 3.4 Versioning — Semantic Versioning
- Format: `v<MAJOR>.<MINOR>.<PATCH>` (ví dụ: `v1.4.2`)
  - **MAJOR**: Breaking changes.
  - **MINOR**: Tính năng mới, backward-compatible.
  - **PATCH**: Bug fix, backward-compatible.

---

## 🚫 4. Những Điều Tuyệt Đối Không Được Làm

1. ❌ Commit secrets, API keys, passwords vào git
2. ❌ Force push lên `main` hoặc `develop` branch
3. ❌ Merge code chưa được review vào `main`
4. ❌ Tắt security headers hoặc CORS protection trong production
5. ❌ Lưu plaintext password vào database
6. ❌ Expose internal error details / stack traces cho end users
7. ❌ Dùng user input trực tiếp trong SQL query mà không sanitize
8. ❌ Deploy code mà không test trên môi trường staging trước (khi có staging)
9. ❌ Xóa audit logs hoặc production data mà không có approval
10. ❌ Over-engineer: thêm complexity không cần thiết

---

*Cập nhật lần cuối: 2026-06-13 | Phiên bản: 1.0.2*
*Mọi thay đổi với file này phải được thảo luận và đồng ý bởi toàn bộ team.*
