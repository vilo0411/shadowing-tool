---
id: story-010
title: ChunkEditor & Timing Edit
epic: epic-005-chunk-editor
status: todo
priority: 10
effort: M
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-008]
---

# Story 010: ChunkEditor & Timing Edit

## Mô tả

Tạo ChunkEditor modal cho phép chỉnh sửa start/end time của chunk.

## Tasks

- [ ] Tạo `TimingInput` component:
  - Input cho timestamp (format: MM:SS.mmm hoặc seconds)
  - Validation (không cho phép negative, start > end)
  - +/- buttons để adjust nhỏ (±100ms)
- [ ] Tạo `ChunkEditor` component (modal):
  - Start time input
  - End time input
  - Text display (read-only for now)
  - Preview button (play edited chunk)
  - Save/Cancel buttons
- [ ] Thêm `updateChunkTiming` action vào store:
  - Update chunk in editedChunks array
  - Keep original chunks unchanged
- [ ] Add edit button vào ChunkItem:
  - Pencil icon
  - Opens ChunkEditor modal
- [ ] Validation:
  - Start time < End time
  - Times within media duration

## Acceptance Criteria

- [ ] Có thể edit start/end time
- [ ] Preview chunk trước khi save
- [ ] Validation prevents invalid times
- [ ] Changes saved to session (not file)
- [ ] Modal đóng khi save/cancel

## Technical Notes

### TimingInput Component

```typescript
interface TimingInputProps {
  value: number; // milliseconds
  onChange: (ms: number) => void;
  label: string;
  max?: number;
}

// Display as MM:SS.mmm, edit as seconds
```

### Chunk Edit in Store

```typescript
updateChunkTiming: (chunkId: string, startTime: number, endTime: number) => {
  const chunks = [...get().session.editedChunks];
  const index = chunks.findIndex(c => c.id === chunkId);
  if (index !== -1) {
    chunks[index] = { ...chunks[index], startTime, endTime };
    set(state => ({ session: { ...state.session, editedChunks: chunks } }));
  }
}
```

### ChunkEditor Layout

```
+--------------------------------+
| Edit Chunk #15            [x]  |
+--------------------------------+
| Start: [00:15.500] [-] [+]     |
| End:   [00:18.200] [-] [+]     |
+--------------------------------+
| "This is the subtitle text"    |
+--------------------------------+
| [Preview]  [Cancel] [Save]     |
+--------------------------------+
```

### Tham khảo

- [docs/prd.md - US-007](../../docs/prd.md)
- [docs/architecture.md - ADR-004](../../docs/architecture.md)

## Definition of Done

- [ ] Modal opens/closes correctly
- [ ] Timing edit works
- [ ] Preview plays edited range
- [ ] Validation works
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
