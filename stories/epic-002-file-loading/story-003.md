---
id: story-003
title: FileLoader Component
epic: epic-002-file-loading
status: todo
priority: 3
effort: M
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-002]
---

# Story 003: FileLoader Component

## Mô tả

Tạo component FileLoader với 2 dropzones: một cho media file và một cho subtitle file. Đây là màn hình đầu tiên user thấy khi mở app.

## Tasks

- [ ] Tạo `DropZone` component (`src/components/ui/DropZone.tsx`):
  - Accept file types as prop
  - Drag & drop support
  - Click to open file picker
  - Visual feedback khi drag over
- [ ] Tạo `FileLoader` component (`src/components/features/FileLoader/FileLoader.tsx`):
  - 2 DropZones: Media và Subtitle
  - Hiển thị accepted file types
  - Show selected file names
- [ ] Tạo `LoadView` component:
  - Container cho FileLoader
  - Instructions text
  - App title/branding nhỏ

## Acceptance Criteria

- [ ] Có thể drag & drop files vào dropzone
- [ ] Có thể click để mở file picker
- [ ] Media dropzone accepts: .mp4, .mp3, .webm, .wav, .m4a
- [ ] Subtitle dropzone accepts: .srt
- [ ] Hiển thị file name sau khi chọn
- [ ] Visual feedback khi dragging

## Technical Notes

### File Input Accept Attribute

```typescript
// Media
accept="video/*,audio/*,.mp4,.mp3,.webm,.wav,.m4a"

// Subtitle
accept=".srt"
```

### DropZone Props

```typescript
interface DropZoneProps {
  accept: string;
  label: string;
  onFileSelect: (file: File) => void;
  selectedFile?: File | null;
}
```

### Layout

```
+----------------------------------+
|        Shadowing Tool            |
|                                  |
|  +------------+  +------------+  |
|  |   Drop     |  |   Drop     |  |
|  |   Media    |  |  Subtitle  |  |
|  |   File     |  |   File     |  |
|  +------------+  +------------+  |
|                                  |
|        [Start Practice]          |
+----------------------------------+
```

### Tham khảo

- [docs/architecture.md - Section 6](../../docs/architecture.md)
- [docs/prd.md - US-001, US-002](../../docs/prd.md)

## Definition of Done

- [ ] Component renders correctly
- [ ] Drag & drop works
- [ ] File picker works
- [ ] Responsive design
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
