---
id: story-004
title: Media & Subtitle Loading Logic
epic: epic-002-file-loading
status: todo
priority: 4
effort: M
created: 2026-01-28
updated: 2026-01-28
completed:
depends_on: [story-003]
---

# Story 004: Media & Subtitle Loading Logic

## Mô tả

Implement logic để load media file (tạo Object URL) và parse subtitle file thành chunks. Connect FileLoader với Zustand store.

## Tasks

- [ ] Implement `loadMediaFile` action trong store:
  - Tạo Object URL từ File
  - Lưu file reference và URL vào state
  - Handle cleanup (revoke old URL)
- [ ] Implement `loadSubtitleFile` action trong store:
  - Read file as text
  - Parse với SRT parser
  - Store chunks vào state
  - Set currentChunkIndex = 0
- [ ] Connect FileLoader với store:
  - Gọi store actions khi file được chọn
  - Hiển thị loading state
  - Handle errors
- [ ] Implement transition to Practice View:
  - Khi cả 2 files loaded → show PracticeView
  - Tạo basic PracticeView placeholder
- [ ] Error handling:
  - Invalid file format
  - Parse errors
  - Empty subtitle file

## Acceptance Criteria

- [ ] Media file được load và có URL để play
- [ ] Subtitle file được parse thành chunks
- [ ] Hiển thị tổng số chunks sau khi load
- [ ] Hiển thị error message khi file invalid
- [ ] App chuyển sang Practice view sau khi load xong

## Technical Notes

### Object URL

```typescript
const loadMediaFile = (file: File) => {
  // Revoke old URL to prevent memory leak
  if (state.session.mediaUrl) {
    URL.revokeObjectURL(state.session.mediaUrl);
  }

  const url = URL.createObjectURL(file);
  set({ session: { ...state.session, mediaFile: file, mediaUrl: url } });
};
```

### Read Subtitle File

```typescript
const loadSubtitleFile = async (file: File) => {
  try {
    const text = await file.text();
    const chunks = parseSRT(text);
    set({ session: { ...state.session, subtitleFile: file, chunks } });
  } catch (error) {
    // Handle parse error
  }
};
```

### Edge Cases (from PRD)

- File .srt encoding khác UTF-8 → try TextDecoder with different encodings
- Empty file → show "No subtitles found" error
- Invalid format → show parse error with details

### Tham khảo

- [docs/architecture.md - Section 5](../../docs/architecture.md)
- [docs/prd.md - US-001 Edge Cases, US-002 Edge Cases](../../docs/prd.md)

## Definition of Done

- [ ] Media file loads successfully
- [ ] Subtitle parses correctly
- [ ] Error messages hiển thị đúng
- [ ] No memory leaks (Object URL revoked)
- [ ] Commit với message rõ ràng

---

## Notes

[Ghi chú trong quá trình implement]
