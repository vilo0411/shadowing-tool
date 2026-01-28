---
id: story-005
title: MediaPlayer Component
epic: epic-003-playback
status: todo
priority: 5
effort: L
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-004]
---

# Story 005: MediaPlayer Component

## Mô tả

Tạo MediaPlayer component có thể play video/audio và SubtitleDisplay để hiển thị text của chunk hiện tại. Player phải có khả năng play từ start time đến end time của chunk.

## Tasks

- [ ] Tạo `useMediaPlayer` hook (`src/hooks/useMediaPlayer.ts`):
  - Ref đến video/audio element
  - play(), pause(), seek(time)
  - currentTime, duration tracking
  - Auto-stop at chunk end time
- [ ] Tạo `MediaPlayer` component:
  - Render `<video>` hoặc `<audio>` based on file type
  - Connect với store để lấy mediaUrl
  - Hidden native controls (custom controls riêng)
- [ ] Tạo `SubtitleDisplay` component:
  - Hiển thị text của current chunk
  - Large, readable font
- [ ] Tạo `PlayerControls` component:
  - Play/Pause button
  - Current time display
  - Chunk info (current/total)
- [ ] Tạo `PracticeView` layout:
  - Header (file name, progress)
  - MediaPlayer
  - SubtitleDisplay
  - PlayerControls
  - Sidebar placeholder

## Acceptance Criteria

- [ ] Video/Audio plays correctly
- [ ] Playback stops at chunk end time
- [ ] Subtitle text hiển thị đúng
- [ ] Play/Pause button works
- [ ] Hiển thị "15/120" (chunk index/total)

## Technical Notes

### useMediaPlayer Hook

```typescript
const useMediaPlayer = (chunk: Chunk | null) => {
  const mediaRef = useRef<HTMLVideoElement | HTMLAudioElement>(null);

  useEffect(() => {
    const media = mediaRef.current;
    if (!media || !chunk) return;

    const handleTimeUpdate = () => {
      // Stop at chunk end
      if (media.currentTime >= chunk.endTime / 1000) {
        media.pause();
        media.currentTime = chunk.startTime / 1000;
      }
    };

    media.addEventListener('timeupdate', handleTimeUpdate);
    return () => media.removeEventListener('timeupdate', handleTimeUpdate);
  }, [chunk]);

  return { mediaRef, play, pause, seek, currentTime, duration };
};
```

### Detect File Type

```typescript
const isVideo = (file: File) => file.type.startsWith('video/');
```

### Layout

```
+------------------------------------------+
|  [FileName.mp4]           [Progress: 45%] |
+------------------------------------------+
|                                          |
|           [ Video Player ]               |
|                                          |
+------------------------------------------+
|  "This is the subtitle text displayed"   |
+------------------------------------------+
|  [Pause]            Chunk 15/120         |
+------------------------------------------+
```

### Tham khảo

- [docs/architecture.md - Section 7](../../docs/architecture.md)
- [docs/prd.md - US-003](../../docs/prd.md)

## Definition of Done

- [ ] Playback works for video and audio
- [ ] Stops at chunk end
- [ ] Subtitle displays correctly
- [ ] Controls work
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
