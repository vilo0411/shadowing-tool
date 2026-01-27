# CLAUDE.md

> 🎯 File này là "single source of truth" cho Claude Code. Cập nhật thường xuyên.

## Thông tin dự án

**Tên dự án:** [Tên dự án]  
**Mô tả:** [Mô tả ngắn gọn dự án làm gì]  
**Trạng thái:** 🟥 Planning | 🟨 Development | 🟩 Production

## Tech Stack

> ⚠️ Để trống nếu chưa quyết định. Agent `@architect` sẽ gợi ý stack phù hợp.

```yaml
Frontend:
  - Framework: [Chưa quyết định]
  - Styling: [Chưa quyết định]
  - State Management: [Chưa quyết định]

Backend:
  - Runtime: [Chưa quyết định]
  - Framework: [Chưa quyết định]
  - Database: [Chưa quyết định]

Infrastructure:
  - Hosting: [Chưa quyết định]
  - CI/CD: [Chưa quyết định]
```

## Mục tiêu hiện tại

### 🎯 Sprint này (Tuần của YYYY-MM-DD)

1. [ ] Mục tiêu 1
2. [ ] Mục tiêu 2
3. [ ] Mục tiêu 3

### 📋 Tasks đang làm

| Task | Trạng thái | Ưu tiên | Link |
|------|------------|---------|------|
| [Tên task] | 🟥 Todo | Cao | [[stories/epic-xxx/story-xxx]] |

## Cấu trúc dự án

```
src/
├── [Sẽ được điền sau khi có architecture]
```

## BMAD Workflow

### Agents có sẵn

| Agent | Lệnh | Mô tả |
|-------|------|-------|
| Analyst | `@analyst` | Phân tích ý tưởng, brainstorm |
| PM | `@pm` | Tạo PRD từ brief |
| Architect | `@architect` | Thiết kế hệ thống, gợi ý tech stack |
| Scrum Master | `@sm` | Tạo stories từ architecture |
| Developer | `@dev` | Implement code |
| Reviewer | `@reviewer` | Review code + giải thích |

### Commands phụ

| Command | Mô tả |
|---------|-------|
| `@agent revise` | Sửa output dựa trên feedback |
| `@agent redo` | Làm lại hoàn toàn |
| `@agent explain` | Giải thích output |

### Trạng thái Planning

- [ ] Brief (`docs/brief.md`)
- [ ] PRD (`docs/prd.md`)
- [ ] Architecture (`docs/architecture.md`)
- [ ] Stories (`stories/`)

## Context quan trọng

### Quyết định đã đưa ra

| Ngày | Quyết định | Lý do |
|------|------------|-------|
| YYYY-MM-DD | [Quyết định gì] | [Tại sao] |

### Vấn đề đã biết / Tech Debt

- [ ] Vấn đề 1: [Mô tả]

## Links

- **Docs:** [[docs/]]
- **Stories:** [[stories/_backlog]]
- **Giải thích code:** [[explain/_index]]
- **GitHub:** [repo-url]

---

> 📌 **Lưu ý cho Claude Code:** 
> - Luôn đọc file này trước khi làm việc
> - Đọc agent prompt trong `.bmad/agents/` khi được gọi
> - Output bằng tiếng Việt, code comments bằng English
