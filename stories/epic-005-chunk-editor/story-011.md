---
id: story-011
title: Merge Chunks
epic: epic-005-chunk-editor
status: todo
priority: 11
effort: M
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-010]
---

# Story 011: Merge Chunks

## Mô tả

Implement khả năng gộp nhiều chunks liên tiếp thành một chunk dài.

## Tasks

- [ ] Add multi-select capability to ChunkList:
  - Shift+click để select range
  - Show selection count
- [ ] Tạo `MergeButton` component:
  - Chỉ hiển thị khi có 2+ chunks selected
  - Show count: "Merge 3 chunks"
- [ ] Thêm `mergeChunks` action vào store:
  - Input: startIndex, endIndex
  - Create new chunk với:
    - startTime = first chunk start
    - endTime = last chunk end
    - text = joined texts (với separator)
  - Remove original chunks
  - Update indexes
- [ ] Preview merged chunk trước khi confirm
- [ ] Add merge option trong ChunkEditor modal

## Acceptance Criteria

- [ ] Có thể select multiple chunks
- [ ] Merge button appears khi 2+ selected
- [ ] Merged chunk có đúng timing
- [ ] Texts được gộp lại
- [ ] Preview trước khi confirm

## Technical Notes

### Merge Logic

```typescript
mergeChunks: (startIndex: number, endIndex: number) => {
  const chunks = [...get().session.editedChunks];
  const toMerge = chunks.slice(startIndex, endIndex + 1);

  const mergedChunk: Chunk = {
    id: generateId(),
    index: startIndex,
    startTime: toMerge[0].startTime,
    endTime: toMerge[toMerge.length - 1].endTime,
    text: toMerge.map(c => c.text).join(' '),
    originalIndex: toMerge[0].originalIndex,
  };

  // Replace range with merged chunk
  const newChunks = [
    ...chunks.slice(0, startIndex),
    mergedChunk,
    ...chunks.slice(endIndex + 1),
  ];

  // Reindex
  newChunks.forEach((c, i) => c.index = i);

  set(state => ({ session: { ...state.session, editedChunks: newChunks } }));
}
```

### Selection State

```typescript
// In store or local state
selectedChunks: number[]; // array of indexes

// Shift+click logic
const handleChunkClick = (index: number, shiftKey: boolean) => {
  if (shiftKey && selectedChunks.length > 0) {
    const start = Math.min(selectedChunks[0], index);
    const end = Math.max(selectedChunks[0], index);
    setSelectedChunks(range(start, end + 1));
  } else {
    setSelectedChunks([index]);
  }
};
```

### Tham khảo

- [docs/prd.md - US-008](../../docs/prd.md)

## Definition of Done

- [ ] Multi-select works
- [ ] Merge creates correct chunk
- [ ] Texts joined properly
- [ ] Indexes updated
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
