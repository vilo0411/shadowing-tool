---
id: story-007
title: Speed Control
epic: epic-003-playback
status: todo
priority: 7
effort: S
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-005]
---

# Story 007: Speed Control

## Mô tả

Implement điều chỉnh tốc độ playback từ 0.5x đến 1.5x.

## Tasks

- [ ] Thêm `playbackSpeed` state vào store (default: 1.0)
- [ ] Thêm `setSpeed` action
- [ ] Update useMediaPlayer hook:
  - Set `media.playbackRate` khi speed thay đổi
- [ ] Tạo `SpeedControl` component:
  - Dropdown hoặc buttons cho các mức speed
  - Hiển thị speed hiện tại
- [ ] Add vào PlayerControls
- [ ] Tốc độ phải được giữ khi chuyển chunk

## Acceptance Criteria

- [ ] Có thể chọn speed: 0.5x, 0.75x, 1.0x, 1.25x, 1.5x
- [ ] Hiển thị speed hiện tại
- [ ] Playback đúng tốc độ đã chọn
- [ ] Speed được giữ khi chuyển chunk

## Technical Notes

### Speed Steps

```typescript
const SPEED_STEPS = [0.5, 0.75, 1.0, 1.25, 1.5];
```

### Set Playback Rate

```typescript
useEffect(() => {
  if (mediaRef.current) {
    mediaRef.current.playbackRate = playbackSpeed;
  }
}, [playbackSpeed]);
```

### SpeedControl Component

```typescript
// Option 1: Dropdown
<select value={speed} onChange={e => setSpeed(Number(e.target.value))}>
  {SPEED_STEPS.map(s => (
    <option key={s} value={s}>{s}x</option>
  ))}
</select>

// Option 2: Buttons
<div className="flex gap-1">
  <button onClick={() => setSpeed(Math.max(0.5, speed - 0.25))}>-</button>
  <span>{speed}x</span>
  <button onClick={() => setSpeed(Math.min(1.5, speed + 0.25))}>+</button>
</div>
```

### Tham khảo

- [docs/prd.md - US-005](../../docs/prd.md)

## Definition of Done

- [ ] Speed control UI works
- [ ] Playback rate changes correctly
- [ ] Speed persists across chunks
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
