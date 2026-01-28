---
id: story-006
title: Loop Functionality
epic: epic-003-playback
status: todo
priority: 6
effort: S
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-005]
---

# Story 006: Loop Functionality

## Mô tả

Implement khả năng loop (lặp lại) chunk hiện tại. Khi loop bật, chunk sẽ tự động replay khi kết thúc.

## Tasks

- [ ] Thêm `isLooping` state vào store
- [ ] Thêm `toggleLoop` action
- [ ] Update useMediaPlayer hook:
  - Khi chunk kết thúc + loop on → replay từ đầu
  - Khi chunk kết thúc + loop off → pause
- [ ] Tạo `LoopToggle` component:
  - Button với icon (Repeat)
  - Visual feedback khi loop on (highlighted)
  - Tooltip hiển thị trạng thái
- [ ] Add vào PlayerControls

## Acceptance Criteria

- [ ] Toggle loop on/off bằng button
- [ ] Khi loop on: chunk tự replay khi hết
- [ ] Khi loop off: pause khi hết chunk
- [ ] Visual indicator rõ ràng (loop on/off)

## Technical Notes

### Loop Logic in useMediaPlayer

```typescript
const handleTimeUpdate = () => {
  if (media.currentTime >= chunk.endTime / 1000) {
    if (isLooping) {
      // Replay from start
      media.currentTime = chunk.startTime / 1000;
      media.play();
    } else {
      // Stop
      media.pause();
      media.currentTime = chunk.startTime / 1000;
    }
  }
};
```

### LoopToggle Component

```typescript
<button
  onClick={toggleLoop}
  className={cn(
    "p-2 rounded",
    isLooping ? "bg-blue-500 text-white" : "bg-gray-200"
  )}
>
  <Repeat size={20} />
</button>
```

### Tham khảo

- [docs/prd.md - US-004](../../docs/prd.md)

## Definition of Done

- [ ] Loop toggle works
- [ ] Auto-replay when loop on
- [ ] Clear visual feedback
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
