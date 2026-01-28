---
id: story-013
title: Save Progress
epic: epic-006-progress
status: todo
priority: 13
effort: M
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-008]
---

# Story 013: Save Progress

## Mô tả

Implement auto-save progress vào localStorage, bao gồm: current chunk, chunks đã done, và chunk edits.

## Tasks

- [ ] Update `useProgressStore`:
  - Save progress with file identifier
  - Load progress by file identifier
  - Generate file ID: hash(fileName + fileSize)
- [ ] Implement progress data structure:
  - fileId
  - fileName
  - lastChunkIndex
  - completedChunks (array of indexes)
  - chunkEdits (for restore edits)
  - lastAccessedAt (timestamp)
- [ ] Auto-save triggers:
  - When chunk changes
  - When marking chunk as done
  - When editing chunks
  - Debounce saves (không save mỗi frame)
- [ ] Implement storage management:
  - Max 100 file progresses
  - Delete oldest when exceeding limit
- [ ] Add progress indicator trong UI:
  - "45% complete" hoặc "54/120 chunks done"
  - Progress bar trong Header

## Acceptance Criteria

- [ ] Progress auto-saves khi có changes
- [ ] Progress persists sau khi refresh
- [ ] Progress bar hiển thị % đúng
- [ ] Old progresses được cleanup

## Technical Notes

### File ID Generation

```typescript
const generateFileId = (file: File): string => {
  return `${file.name}-${file.size}`;
  // Or use a proper hash if needed
};
```

### Progress Store with Persistence

```typescript
import { create } from 'zustand';
import { persist } from 'zustand/middleware';

interface ProgressState {
  progresses: Record<string, FileProgress>;
  saveProgress: (fileId: string, progress: FileProgress) => void;
  loadProgress: (fileId: string) => FileProgress | null;
}

const useProgressStore = create<ProgressState>()(
  persist(
    (set, get) => ({
      progresses: {},
      saveProgress: (fileId, progress) => {
        set(state => ({
          progresses: {
            ...state.progresses,
            [fileId]: { ...progress, lastAccessedAt: Date.now() }
          }
        }));
        // Cleanup if > 100
        cleanupOldProgresses(get, set);
      },
      loadProgress: (fileId) => get().progresses[fileId] || null,
    }),
    { name: 'shadowing-progress' }
  )
);
```

### Auto-save with Debounce

```typescript
import { useMemo } from 'react';
import { debounce } from './utils';

const useAutoSave = () => {
  const saveProgress = useProgressStore(s => s.saveProgress);
  const session = useAppStore(s => s.session);

  const debouncedSave = useMemo(
    () => debounce(() => {
      if (session.mediaFile) {
        const fileId = generateFileId(session.mediaFile);
        saveProgress(fileId, {
          fileId,
          fileName: session.mediaFile.name,
          lastChunkIndex: session.currentChunkIndex,
          completedChunks: session.completedChunks,
          lastAccessedAt: Date.now(),
        });
      }
    }, 1000),
    [session, saveProgress]
  );

  useEffect(() => {
    debouncedSave();
  }, [session.currentChunkIndex, session.completedChunks]);
};
```

### Tham khảo

- [docs/architecture.md - FR-003](../../docs/architecture.md)
- [docs/prd.md - US-010](../../docs/prd.md)

## Definition of Done

- [ ] Auto-save works
- [ ] Progress persists
- [ ] Progress bar displays
- [ ] Storage cleanup works
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
