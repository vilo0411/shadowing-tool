---
id: story-008
title: ChunkList & Navigation
epic: epic-004-navigation
status: todo
priority: 8
effort: M
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-005]
---

# Story 008: ChunkList & Navigation

## Mô tả

Tạo ChunkList sidebar hiển thị tất cả chunks và implement navigation (next/prev/jump to chunk).

## Tasks

- [ ] Thêm navigation actions vào store:
  - `nextChunk()` - go to next chunk
  - `prevChunk()` - go to previous chunk
  - `goToChunk(index)` - jump to specific chunk
- [ ] Tạo `ChunkItem` component:
  - Index number
  - Text preview (truncated)
  - Current indicator (highlight)
  - Done checkbox (placeholder for later)
- [ ] Tạo `ChunkList` component:
  - Scrollable list of ChunkItems
  - Auto-scroll to current chunk
  - Click to jump
- [ ] Tạo `Sidebar` component:
  - Container cho ChunkList
  - Header với "Chunks" title
  - Filter placeholder (all/done/not done)
- [ ] Update PlayerControls:
  - Add Next/Prev buttons
  - Connect with store actions
- [ ] Handle edge cases:
  - First chunk → prev does nothing
  - Last chunk → next does nothing

## Acceptance Criteria

- [ ] ChunkList hiển thị tất cả chunks
- [ ] Click chunk → jump tới chunk đó
- [ ] Next/Prev buttons work
- [ ] Current chunk được highlight
- [ ] Auto-scroll to current chunk
- [ ] Hiển thị "15/120" chính xác

## Technical Notes

### Navigation Actions

```typescript
nextChunk: () => {
  const { currentChunkIndex, chunks } = get().session;
  if (currentChunkIndex < chunks.length - 1) {
    set(state => ({
      session: { ...state.session, currentChunkIndex: currentChunkIndex + 1 }
    }));
  }
},
```

### ChunkItem

```typescript
interface ChunkItemProps {
  chunk: Chunk;
  index: number;
  isCurrent: boolean;
  onClick: () => void;
}
```

### Auto-scroll

```typescript
useEffect(() => {
  const currentElement = listRef.current?.querySelector(`[data-index="${currentIndex}"]`);
  currentElement?.scrollIntoView({ behavior: 'smooth', block: 'center' });
}, [currentIndex]);
```

### Layout

```
+------------------+
| Chunks      [?]  |
+------------------+
| [ ] 1. Hello...  |
| [x] 2. How ar... | <- current (highlighted)
| [ ] 3. I'm fi... |
| [ ] 4. Thank...  |
|    ...           |
+------------------+
```

### Tham khảo

- [docs/architecture.md - Section 6](../../docs/architecture.md)
- [docs/prd.md - US-006](../../docs/prd.md)

## Definition of Done

- [ ] ChunkList renders correctly
- [ ] Navigation works
- [ ] Auto-scroll works
- [ ] Edge cases handled
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
