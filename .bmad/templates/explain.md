---
topic: "[Tên topic]"
category: "[core/feature/component]"
related_stories: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# [Topic]: Giải thích chi tiết

> 📚 Document này giải thích [topic] trong dự án

## Tổng quan đơn giản

[Giải thích bằng ngôn ngữ đơn giản nhất có thể. Tưởng tượng bạn đang giải thích cho người không biết lập trình.]

**Ví dụ thực tế:**

[Dùng analogy từ đời thường để giải thích concept này. Ví dụ: "Authentication giống như bảo vệ kiểm tra thẻ nhân viên trước khi cho vào tòa nhà."]

---

## Tại sao cần [topic] này?

- **Vấn đề:** [Vấn đề gì nếu không có feature này]
- **Giải pháp:** [Feature này giải quyết như thế nào]
- **Lợi ích:** [User được gì]

---

## Cách hoạt động

### Flow tổng quan

```
[Bước 1]
    ↓
[Bước 2]
    ↓
[Bước 3]
    ↓
[Kết quả]
```

### Chi tiết từng bước

#### Bước 1: [Tên bước]

[Giải thích chi tiết]

**Điều gì xảy ra:**
1. [Điều 1]
2. [Điều 2]

#### Bước 2: [Tên bước]

[Giải thích chi tiết]

---

## Files liên quan

| File | Vai trò | Quan trọng |
|------|---------|------------|
| `src/path/file.ts` | [Mô tả vai trò] | ⭐⭐⭐ |
| `src/path/file.ts` | [Mô tả vai trò] | ⭐⭐ |

---

## Code explained

### File: `src/path/to/main-file.ts`

```typescript
// [Tên function/component chính]
export const exampleFunction = async (input: string) => {
  // Bước 1: [Giải thích]
  const data = await fetchData(input)
  
  // Bước 2: [Giải thích]
  const processed = processData(data)
  
  // Bước 3: [Giải thích]
  return processed
}
```

**Giải thích từng phần:**

| Dòng | Code | Giải thích |
|------|------|------------|
| 1 | `export const...` | [Giải thích] |
| 3 | `await fetchData...` | [Giải thích] |
| 6 | `processData...` | [Giải thích] |

---

## Câu hỏi thường gặp

### Q: [Câu hỏi 1]?

**A:** [Trả lời đơn giản, dễ hiểu]

### Q: [Câu hỏi 2]?

**A:** [Trả lời]

---

## Nếu muốn thay đổi

### Muốn [thay đổi X]:

1. Mở file `src/path/to/file.ts`
2. Tìm dòng có `[keyword]`
3. Sửa thành:
```typescript
// Code mới
```

### Muốn [thay đổi Y]:

[Hướng dẫn tương tự]

---

## Lỗi thường gặp

### Lỗi: [Tên lỗi]

**Nguyên nhân:** [Tại sao xảy ra]

**Cách fix:** [Hướng dẫn fix]

---

## Links liên quan

- [[explain/related-topic]] - Topic liên quan
- [[docs/architecture#section]] - Architecture reference
- [[stories/epic-xxx/story-xxx]] - Story đã implement

---

## Glossary

| Thuật ngữ | Nghĩa |
|-----------|-------|
| [Term 1] | [Định nghĩa đơn giản] |
| [Term 2] | [Định nghĩa đơn giản] |
