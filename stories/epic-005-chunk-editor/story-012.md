---
id: story-012
title: Split Chunk
epic: epic-005-chunk-editor
status: todo
priority: 12
effort: M
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-010]
---

# Story 012: Split Chunk

## Mô tả

Implement khả năng tách một chunk dài thành hai chunks nhỏ hơn.

## Tasks

- [ ] Add Split button trong ChunkEditor modal
- [ ] Tạo split point selector:
  - Slider để chọn điểm split trong range của chunk
  - Hoặc input timestamp
  - Visual feedback showing where split will happen
- [ ] Thêm `splitChunk` action vào store:
  - Input: chunkId, splitTime
  - Create 2 new chunks từ 1 chunk
  - First: startTime → splitTime
  - Second: splitTime → endTime
  - Split text (proportional hoặc manual)
- [ ] Preview cả 2 chunks trước khi confirm
- [ ] Handle text splitting:
  - Option 1: Split proportional to time
  - Option 2: Manual edit text cho mỗi phần

## Acceptance Criteria

- [ ] Có thể chọn split point
- [ ] Split tạo đúng 2 chunks
- [ ] Timings chính xác
- [ ] Text được split hợp lý
- [ ] Preview trước khi confirm

## Technical Notes

### Split Logic

```typescript
splitChunk: (chunkId: string, splitTime: number) => {
  const chunks = [...get().session.editedChunks];
  const index = chunks.findIndex(c => c.id === chunkId);
  const original = chunks[index];

  // Calculate text split (proportional)
  const totalDuration = original.endTime - original.startTime;
  const splitRatio = (splitTime - original.startTime) / totalDuration;
  const words = original.text.split(' ');
  const splitWordIndex = Math.round(words.length * splitRatio);

  const chunk1: Chunk = {
    id: generateId(),
    index: index,
    startTime: original.startTime,
    endTime: splitTime,
    text: words.slice(0, splitWordIndex).join(' '),
    originalIndex: original.originalIndex,
  };

  const chunk2: Chunk = {
    id: generateId(),
    index: index + 1,
    startTime: splitTime,
    endTime: original.endTime,
    text: words.slice(splitWordIndex).join(' '),
    originalIndex: original.originalIndex,
  };

  // Replace original with 2 new chunks
  const newChunks = [
    ...chunks.slice(0, index),
    chunk1,
    chunk2,
    ...chunks.slice(index + 1),
  ];

  // Reindex
  newChunks.forEach((c, i) => c.index = i);

  set(state => ({ session: { ...state.session, editedChunks: newChunks } }));
}
```

### Split UI

```
+--------------------------------+
| Split Chunk #15           [x]  |
+--------------------------------+
| Start: 00:15.500               |
| End:   00:22.000               |
| Duration: 6.5s                 |
+--------------------------------+
| Split at: [00:18.000]          |
| [========|========] <- slider  |
+--------------------------------+
| Part 1: "First part of text"   |
| Part 2: "Second part of text"  |
+--------------------------------+
| [Preview 1] [Preview 2]        |
| [Cancel] [Split]               |
+--------------------------------+
```

### Tham khảo

- [docs/prd.md - US-009](../../docs/prd.md)

## Definition of Done

- [ ] Split point selector works
- [ ] Split creates 2 correct chunks
- [ ] Text split reasonably
- [ ] Previews work
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
