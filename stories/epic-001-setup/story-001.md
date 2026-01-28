---
id: story-001
title: Project Initialization
epic: epic-001-setup
status: todo
priority: 1
effort: M
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: []
---

# Story 001: Project Initialization

## Mô tả

Khởi tạo project Vite với React và TypeScript, cài đặt dependencies, setup Tailwind CSS, và tạo cấu trúc thư mục theo architecture.

## Tasks

- [ ] Khởi tạo Vite project với React + TypeScript template
- [ ] Cài đặt dependencies:
  - `zustand` - state management
  - `lucide-react` - icons
  - `tailwindcss`, `postcss`, `autoprefixer` - styling
- [ ] Setup Tailwind CSS config
- [ ] Tạo folder structure:
  ```
  src/
  ├── components/
  │   ├── ui/
  │   ├── layout/
  │   └── features/
  ├── hooks/
  ├── stores/
  ├── lib/
  ├── types/
  └── constants/
  ```
- [ ] Setup TypeScript strict mode
- [ ] Tạo base styles trong `index.css`
- [ ] Clean up default Vite files

## Acceptance Criteria

- [ ] `npm run dev` chạy không lỗi
- [ ] TypeScript không có errors
- [ ] Tailwind CSS hoạt động (test với một class)
- [ ] Folder structure đúng như architecture

## Technical Notes

### Commands

```bash
npm create vite@latest . -- --template react-ts
npm install zustand lucide-react
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

### Files cần tạo/sửa

- `package.json` - dependencies
- `tsconfig.json` - strict mode
- `tailwind.config.js` - content paths
- `src/index.css` - Tailwind directives
- `src/App.tsx` - clean up

### Tham khảo

- [docs/architecture.md - Section 1, 3](../../docs/architecture.md)

## Definition of Done

- [ ] Code hoạt động
- [ ] Không có TypeScript errors
- [ ] Đã test locally
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
