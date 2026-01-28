---
id: story-014
title: Resume Session & Mark Done
epic: epic-006-progress
status: todo
priority: 14
effort: M
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-013]
---

# Story 014: Resume Session & Mark Chunk as Done

## Mô tả

Implement khả năng resume session từ progress đã lưu và đánh dấu chunk là "done".

## Tasks

- [ ] Implement resume flow:
  - Khi load file → check nếu có saved progress
  - Show dialog: "Resume from chunk 54?" với options
  - If yes: restore currentChunkIndex, completedChunks
  - If no: start fresh, clear old progress
- [ ] Implement "Mark as Done":
  - Checkbox trong ChunkItem
  - Button trong PlayerControls
  - Keyboard shortcut: Enter
  - Auto-next sau khi mark done
- [ ] Update ChunkItem UI:
  - Checkmark icon cho done chunks
  - Different styling (faded, strikethrough, hoặc green)
- [ ] Add completedChunks to store:
  - `markChunkDone(index)` action
  - `markChunkUndone(index)` action
- [ ] Filter trong ChunkList (optional):
  - All / Done / Not done
  - Count hiển thị

## Acceptance Criteria

- [ ] Resume dialog xuất hiện khi có saved progress
- [ ] Can resume hoặc start fresh
- [ ] Mark done works (button, keyboard)
- [ ] Done chunks có visual indicator
- [ ] Auto-next sau khi mark done

## Technical Notes

### Resume Dialog

```typescript
const ResumeDialog = ({ progress, onResume, onStartFresh }) => (
  <Modal open>
    <h2>Resume Previous Session?</h2>
    <p>You were at chunk {progress.lastChunkIndex + 1}</p>
    <p>{progress.completedChunks.length} chunks completed</p>
    <div>
      <button onClick={onResume}>Resume</button>
      <button onClick={onStartFresh}>Start Fresh</button>
    </div>
  </Modal>
);
```

### Mark Done Actions

```typescript
markChunkDone: (index: number) => {
  set(state => ({
    session: {
      ...state.session,
      completedChunks: [...state.session.completedChunks, index]
    }
  }));
  // Auto next
  get().nextChunk();
},

markChunkUndone: (index: number) => {
  set(state => ({
    session: {
      ...state.session,
      completedChunks: state.session.completedChunks.filter(i => i !== index)
    }
  }));
},
```

### ChunkItem với Done State

```typescript
const ChunkItem = ({ chunk, isDone, isCurrent, onToggleDone, onClick }) => (
  <div
    className={cn(
      "flex items-center gap-2 p-2 cursor-pointer",
      isCurrent && "bg-blue-100",
      isDone && "opacity-50"
    )}
    onClick={onClick}
  >
    <button
      onClick={(e) => { e.stopPropagation(); onToggleDone(); }}
      className={cn(isDone && "text-green-500")}
    >
      {isDone ? <CheckCircle /> : <Circle />}
    </button>
    <span className={cn(isDone && "line-through")}>
      {chunk.index + 1}. {chunk.text.slice(0, 30)}...
    </span>
  </div>
);
```

### Tham khảo

- [docs/prd.md - US-011, US-013](../../docs/prd.md)

## Definition of Done

- [ ] Resume flow works
- [ ] Mark done works
- [ ] Visual indicators clear
- [ ] Auto-next after mark done
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
