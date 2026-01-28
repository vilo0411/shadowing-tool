# CLAUDE.md

> 🎯 File này là "single source of truth" cho Claude Code. Cập nhật thường xuyên.

## Thông tin dự án

**Tên dự án:** Shadowing Tool
**Mô tả:** Tool luyện tập tiếng Anh theo phương pháp shadowing - load video/audio + subtitle, split thành chunks để luyện từng đoạn
**Trạng thái:** 🟨 Ready for Development

## Tech Stack

```yaml
Frontend:
  - Framework: React 18
  - Build Tool: Vite 5
  - Language: TypeScript
  - Styling: Tailwind CSS
  - State Management: Zustand
  - Icons: Lucide React

Backend:
  - None (client-side only)

Storage:
  - localStorage (progress, settings)

Infrastructure:
  - Hosting: Vercel / GitHub Pages / Local
  - CI/CD: GitHub Actions (optional)
```

## Mục tiêu hiện tại

### 🎯 Sprint này (Tuần của 2026-01-28)

1. [x] Hoàn thành planning docs (Brief, PRD, Architecture)
2. [x] Tạo stories từ architecture (6 epics, 14 stories)
3. [ ] Setup project (Vite + React + TypeScript)

### 📋 Tasks đang làm

| Task | Trạng thái | Ưu tiên | Link |
|------|------------|---------|------|
| story-001: Project init | 🟥 Todo | 1 | [stories/epic-001-setup/story-001.md](stories/epic-001-setup/story-001.md) |

## Cấu trúc dự án

```
src/
├── main.tsx                 # Entry point
├── App.tsx                  # Root component
├── index.css                # Global styles + Tailwind
│
├── components/
│   ├── ui/                  # Base UI (Button, Modal, etc.)
│   ├── layout/              # Header, Sidebar
│   └── features/            # FileLoader, Player, ChunkList, ChunkEditor
│
├── hooks/                   # useMediaPlayer, useKeyboardShortcuts, etc.
├── stores/                  # Zustand stores (app state, progress)
├── lib/                     # srtParser, timeUtils, storage
├── types/                   # TypeScript interfaces
└── constants/               # App constants
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

- [x] Brief (`docs/brief.md`)
- [x] PRD (`docs/prd.md`)
- [x] Architecture (`docs/architecture.md`)
- [x] Stories (`stories/`) - 6 epics, 14 stories

## Context quan trọng

### Quyết định đã đưa ra

| Ngày | Quyết định | Lý do |
|------|------------|-------|
| 2026-01-28 | React + Vite stack | Nhanh, đơn giản, phù hợp personal tool |
| 2026-01-28 | Client-side only | Không cần backend, mọi thứ xử lý trong browser |
| 2026-01-28 | localStorage cho progress | Đủ cho personal use, không cần cloud sync |
| 2026-01-28 | Zustand cho state | Lightweight, no boilerplate |

### Vấn đề đã biết / Tech Debt

- [ ] Phải chọn file mỗi lần mở app (browser security limitation)

## Links

- **Docs:** `docs/`
- **Brief:** `docs/brief.md`
- **PRD:** `docs/prd.md`
- **Architecture:** `docs/architecture.md`
- **Backlog:** `stories/_backlog.md`
- **Stories:** `stories/`

---

> 📌 **Lưu ý cho Claude Code:**
> - Luôn đọc file này trước khi làm việc
> - Đọc agent prompt trong `.bmad/agents/` khi được gọi
> - Output bằng tiếng Việt, code comments bằng English
