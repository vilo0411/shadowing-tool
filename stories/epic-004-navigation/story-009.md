---
id: story-009
title: Keyboard Shortcuts
epic: epic-004-navigation
status: todo
priority: 9
effort: M
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-008]
---

# Story 009: Keyboard Shortcuts

## Mô tả

Implement global keyboard shortcuts cho tất cả các actions chính.

## Tasks

- [ ] Tạo `useKeyboardShortcuts` hook:
  - Global keydown event listener
  - Map keys to actions
  - Prevent conflicts with input fields
- [ ] Implement shortcuts:
  - `Space` → Play/Pause
  - `→` hoặc `J` → Next chunk
  - `←` hoặc `K` → Previous chunk
  - `L` → Toggle loop
  - `[` → Speed down
  - `]` → Speed up
  - `Enter` → Mark done + next (placeholder)
  - `?` → Show shortcuts modal
- [ ] Tạo `ShortcutsModal` component:
  - List all shortcuts
  - Open with `?` key
  - Close with `Esc` or click outside
- [ ] Tạo `Modal` base component (`src/components/ui/Modal.tsx`)
- [ ] Thêm button để mở shortcuts modal trong UI

## Acceptance Criteria

- [ ] Tất cả shortcuts work correctly
- [ ] Shortcuts không trigger khi đang type trong input
- [ ] `?` mở modal hiển thị shortcuts
- [ ] Modal có thể đóng bằng Esc

## Technical Notes

### useKeyboardShortcuts Hook

```typescript
const useKeyboardShortcuts = () => {
  const { play, pause, nextChunk, prevChunk, toggleLoop, setSpeed } = useAppStore();
  const [showShortcuts, setShowShortcuts] = useState(false);

  useEffect(() => {
    const handleKeyDown = (e: KeyboardEvent) => {
      // Don't trigger if typing in input
      if (e.target instanceof HTMLInputElement || e.target instanceof HTMLTextAreaElement) {
        return;
      }

      switch (e.key) {
        case ' ':
          e.preventDefault();
          isPlaying ? pause() : play();
          break;
        case 'ArrowRight':
        case 'j':
          nextChunk();
          break;
        case 'ArrowLeft':
        case 'k':
          prevChunk();
          break;
        case 'l':
          toggleLoop();
          break;
        case '[':
          decreaseSpeed();
          break;
        case ']':
          increaseSpeed();
          break;
        case '?':
          setShowShortcuts(true);
          break;
        case 'Escape':
          setShowShortcuts(false);
          break;
      }
    };

    document.addEventListener('keydown', handleKeyDown);
    return () => document.removeEventListener('keydown', handleKeyDown);
  }, [/* dependencies */]);

  return { showShortcuts, setShowShortcuts };
};
```

### Shortcuts Reference Table

| Action | Key |
|--------|-----|
| Play/Pause | Space |
| Next chunk | → / J |
| Prev chunk | ← / K |
| Toggle loop | L |
| Speed up | ] |
| Speed down | [ |
| Mark done | Enter |
| Show help | ? |

### Tham khảo

- [docs/prd.md - Section 7](../../docs/prd.md)
- [docs/prd.md - US-012](../../docs/prd.md)

## Definition of Done

- [ ] All shortcuts work
- [ ] No conflicts with inputs
- [ ] Modal displays correctly
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
