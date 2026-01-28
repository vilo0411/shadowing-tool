---
id: story-002
title: Core Infrastructure
epic: epic-001-setup
status: todo
priority: 2
effort: M
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-001]
---

# Story 002: Core Infrastructure

## Mô tả

Tạo các types, Zustand stores, SRT parser, và utility functions cần thiết cho app.

## Tasks

- [ ] Tạo TypeScript types (`src/types/index.ts`):
  - `Chunk` - subtitle chunk
  - `Session` - current session state
  - `FileProgress` - saved progress
  - `PlayerState` - playback state
- [ ] Tạo Zustand store (`src/stores/useAppStore.ts`):
  - Session state (files, chunks, playback)
  - Actions (load files, navigate chunks, control playback)
- [ ] Tạo Progress store (`src/stores/useProgressStore.ts`):
  - Progress persistence to localStorage
  - Load/save progress actions
- [ ] Tạo SRT parser (`src/lib/srtParser.ts`):
  - `parseSRT(content: string): Chunk[]`
  - `parseTimestamp(ts: string): number`
  - `formatTimestamp(ms: number): string`
- [ ] Tạo storage utilities (`src/lib/storage.ts`):
  - localStorage wrapper with error handling
- [ ] Tạo time utilities (`src/lib/timeUtils.ts`):
  - Format/parse time functions
- [ ] Tạo constants (`src/constants/index.ts`):
  - Keyboard shortcuts mapping
  - Speed steps
  - Storage keys

## Acceptance Criteria

- [ ] Types định nghĩa đầy đủ, không có `any`
- [ ] Zustand store hoạt động (test với React DevTools)
- [ ] SRT parser parse được sample .srt file
- [ ] localStorage save/load hoạt động

## Technical Notes

### SRT Format Example

```
1
00:00:01,000 --> 00:00:04,000
Hello world

2
00:00:05,000 --> 00:00:08,000
How are you?
```

### Zustand Store Structure

```typescript
interface AppState {
  // State
  session: Session;

  // Actions
  loadMediaFile: (file: File) => void;
  loadSubtitleFile: (file: File) => void;
  // ... more actions
}
```

### Tham khảo

- [docs/architecture.md - Section 4, 5](../../docs/architecture.md)

## Definition of Done

- [ ] Tất cả types được export
- [ ] Stores có tests (manual hoặc unit)
- [ ] SRT parser handles edge cases
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
