# 📋 Backlog

> Cập nhật: Tự động qua Dataview

## Tổng quan dự án

| Metric | Value |
|--------|-------|
| **Trạng thái** | 🟥 Planning |
| **Tổng stories** | - |
| **Hoàn thành** | - |
| **Progress** | 0% |

---

## 🔥 Đang thực hiện

```dataview
TABLE WITHOUT ID
  file.link as "Story",
  epic as "Epic",
  effort as "Effort",
  updated as "Updated"
FROM "stories"
WHERE status = "in-progress" AND file.name != "_backlog" AND file.name != "_overview"
SORT updated DESC
```

---

## 📋 Sắp tới (Todo)

```dataview
TABLE WITHOUT ID
  file.link as "Story",
  epic as "Epic",
  priority as "Priority",
  effort as "Effort"
FROM "stories"
WHERE status = "todo" AND file.name != "_backlog" AND file.name != "_overview"
SORT priority ASC
LIMIT 10
```

---

## ⏸️ Blocked

```dataview
TABLE WITHOUT ID
  file.link as "Story",
  epic as "Epic",
  depends_on as "Blocked by"
FROM "stories"
WHERE status = "blocked" AND file.name != "_backlog" AND file.name != "_overview"
```

---

## ✅ Hoàn thành gần đây

```dataview
TABLE WITHOUT ID
  file.link as "Story",
  epic as "Epic",
  completed as "Completed"
FROM "stories"
WHERE status = "done" AND file.name != "_backlog" AND file.name != "_overview"
SORT completed DESC
LIMIT 5
```

---

## 📊 Theo Epic

```dataview
TABLE WITHOUT ID
  file.link as "Epic",
  length(rows) as "Stories"
FROM "stories"
WHERE file.name = "_overview"
GROUP BY epic
```

---

## 🚀 Bắt đầu

Stories sẽ được tạo bởi `@sm` sau khi có Architecture.

```
@sm
```

---

## Hướng dẫn

### Status Legend
- 🟥 `todo` - Chưa bắt đầu
- 🟨 `in-progress` - Đang làm
- 🔍 `review` - Đang review
- ✅ `done` - Hoàn thành
- ⏸️ `blocked` - Bị block

### Effort Legend
- **XS** - < 30 phút
- **S** - 1-2 giờ
- **M** - 2-4 giờ
- **L** - 4-8 giờ
- **XL** - > 8 giờ (nên chia nhỏ)

### Priority
- **1** - Làm đầu tiên
- **2** - Làm sau priority 1
- **3+** - Làm sau
