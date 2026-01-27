# 📚 Code Explanations

> Tài liệu giải thích code trong dự án - viết bằng tiếng Việt, cho người không chuyên technical

## Mục đích

Folder này chứa các tài liệu giải thích cách code hoạt động. Mỗi khi implement feature mới, `@reviewer` sẽ tạo documentation ở đây để:

1. **Giúp bạn hiểu code** - Giải thích bằng ngôn ngữ đơn giản
2. **Reference sau này** - Khi cần sửa/mở rộng feature
3. **Onboard nhanh** - Nếu có người mới tham gia

---

## Cách đọc

### Mới bắt đầu?
1. Đọc [[explain/project-structure]] để hiểu cấu trúc dự án
2. Đọc [[explain/data-flow]] để hiểu data chạy như thế nào

### Muốn hiểu feature cụ thể?
- Tìm doc tương ứng trong list bên dưới
- Hoặc chạy `@reviewer explain [topic]`

### Muốn sửa code?
- Đọc doc của feature đó
- Xem section "Files liên quan" và "Nếu muốn thay đổi"

---

## Mục lục

### 🏗️ Core Concepts

> Hiểu nền tảng trước khi đi vào chi tiết

```dataview
LIST
FROM "explain"
WHERE category = "core" AND file.name != "_index"
SORT file.name ASC
```

*Sẽ được thêm sau khi bắt đầu development*

### ⚡ Features

> Giải thích từng feature trong app

```dataview
LIST
FROM "explain"
WHERE category = "feature" AND file.name != "_index"
SORT file.name ASC
```

*Sẽ được thêm sau khi implement features*

### 🧩 Components

> Giải thích các UI components quan trọng

```dataview
LIST
FROM "explain"
WHERE category = "component" AND file.name != "_index"
SORT file.name ASC
```

*Sẽ được thêm sau khi tạo components*

---

## Câu hỏi thường gặp

### Không hiểu một phần code?

Chạy:
```
@reviewer explain [topic hoặc file name]
```

### Muốn biết file nào làm gì?

Xem [[explain/project-structure]] hoặc hỏi:
```
@reviewer explain project structure
```

### Doc chưa có cho feature cần tìm?

Chạy:
```
@reviewer [path/to/file hoặc feature name]
```

---

## Ghi chú

- Docs được tạo tự động bởi `@reviewer` sau mỗi story
- Nếu có gì chưa rõ, cứ hỏi Claude!
- Đây là "living documentation" - sẽ được update theo code
