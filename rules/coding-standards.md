---
id: rule-coding-standards
name: "Coding Standards & Style Guide"
scope: global
tags: [coding, style, naming, formatting]
version: "1.0.0"
created: 2026-06-08
updated: 2026-06-08
author: "Personal"
---

# Coding Standards & Style Guide

> Quy tắc nhất quán về code style, naming convention và formatting áp dụng cho mọi project.  
> Mục tiêu: Codebase dễ đọc, dễ review, và dễ maintain.

---

## 🎯 Mục Đích (Purpose)

Inconsistent code style là một trong những nguyên nhân hàng đầu khiến codebase trở nên khó maintain theo thời gian.
Rule này đảm bảo AI agent luôn sinh ra code tuân theo cùng một bộ chuẩn — bất kể project nào,
giúp developer đọc code không phải "adjust" mental model liên tục.

---

## 📋 Quy Tắc Chi Tiết (Rules)

### 1. Indentation & Spacing
1. **Indentation**: 2 spaces cho JS/TS/HTML/CSS; 4 spaces cho Java/C#/Python.
2. **Max line length**: 120 ký tự. Wrap dòng nếu vượt quá.
3. **Trailing whitespace**: Không được có trailing whitespace ở cuối dòng.
4. **File ending**: Mỗi file phải kết thúc bằng một dòng trống.

### 2. Naming Conventions

| Loại | Convention | Ngôn ngữ áp dụng |
|------|-----------|------------------|
| Variable / Function | `camelCase` | JS/TS/Java |
| Class / Interface / Type | `PascalCase` | Tất cả |
| Constant | `SCREAMING_SNAKE_CASE` | Tất cả |
| File (Component) | `PascalCase.tsx` | React/Next.js |
| File (Utility) | `kebab-case.ts` | JS/TS |
| CSS Class | `kebab-case` | CSS/SCSS |
| Database Table | `snake_case` | SQL |
| API Endpoint | `kebab-case` | REST API |
| Environment Variable | `SCREAMING_SNAKE_CASE` | Tất cả |

### 3. Comments & Documentation
1. **Comment WHY, không phải WHAT** — code tự mô tả "cái gì", comment giải thích "tại sao".
2. **TODO format**: `// TODO(tên): mô tả — ngày` — phải có context đầy đủ.
3. **Không comment-out code** — Dùng git để lấy lại code cũ nếu cần.
4. **Xóa debug statements** — Không commit `console.log`, `print()`, hay debug output thừa.

### 4. Imports & Dependencies
1. **Nhóm imports** theo thứ tự: built-in → external → internal.
2. **Không import wildcard** (`import * from`) trừ khi thực sự cần thiết.
3. **Tree-shaking friendly**: Import cụ thể thay vì cả library.

---

## ✅ Ví Dụ Đúng (Correct Examples)

```typescript
// ✅ GOOD: Naming conventions và comment WHY
const MAX_RETRY_COUNT = 3; // Prevent infinite loops on transient network failures

function getUserById(userId: string): Promise<User> {
  return userRepository.findOne({ id: userId });
}

class UserAuthService {
  private readonly jwtSecret: string;
  
  constructor(config: AuthConfig) {
    this.jwtSecret = config.jwtSecret;
  }
}
```

```typescript
// ✅ GOOD: Import grouping
// built-in
import { readFileSync } from 'fs';
import { join } from 'path';

// external
import express from 'express';
import { z } from 'zod';

// internal
import { UserService } from '../services/user-service';
import { logger } from '../utils/logger';
```

```typescript
// ✅ GOOD: TODO với context đầy đủ
// TODO(nam): Replace with Redis cache when traffic > 1k req/s — 2026-06-08
const cache = new Map<string, CacheEntry>();
```

---

## ❌ Ví Dụ Sai (Incorrect Examples)

```typescript
// ❌ BAD: Sai naming convention, comment WHAT thay vì WHY
var maxretrycount = 3; // this is the max retry count

function GetUser(ID) { // PascalCase cho function, sai
  return db.find(ID);
}

// ❌ BAD: Debug statement bị commit
console.log('user data:', userData); // KHÔNG được commit cái này
```

```typescript
// ❌ BAD: Comment-out code thay vì xóa
// function oldCalculateTotal(items) {
//   return items.reduce((sum, item) => sum + item.price, 0);
// }

// ❌ BAD: TODO thiếu context
// TODO: fix this later
```

```typescript
// ❌ BAD: Import không cần thiết
import * as _ from 'lodash'; // import toàn bộ khi chỉ dùng 1 function
```

---

## 🔄 Hành Động Khi Vi Phạm (On Violation)

Khi phát hiện vi phạm trong code được review hoặc code tự sinh ra:

- [ ] **Thông báo rõ ràng**: "File X, line Y vi phạm rule [tên rule]"
- [ ] **Giải thích ngắn gọn**: Tại sao đây là vấn đề
- [ ] **Đề xuất sửa**: Cung cấp code đúng thay thế
- [ ] **Tự sửa nếu được phép**: Khi đang generate code, tự áp dụng đúng convention

---

## 🚫 Ngoại Lệ (Exceptions)

- **Generated code**: Code được auto-generated bởi tools (Prisma migrations, OpenAPI stubs...) không cần tuân theo naming convention nếu tool có convention riêng.
- **Third-party files**: Files được copy nguyên vẹn từ library documentation (ví dụ: config mẫu).
- **Legacy code**: Khi sửa file cũ có convention khác, match convention của file đó — không refactor hàng loạt trừ khi được yêu cầu.

---

## 🔗 Tham Chiếu (References)

- Liên quan: [`communication-style`](./communication-style.md)
- ESLint config: Xem `.eslintrc.js` trong từng project
- Prettier config: Xem `.prettierrc` trong từng project

---

## 📝 Lịch Sử Thay Đổi (Changelog)

| Version | Ngày | Thay đổi |
|---------|------|---------|
| 1.0.0 | 2026-06-08 | Khởi tạo từ GEMINI.md |
