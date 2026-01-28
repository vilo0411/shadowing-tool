# Backlog

> Cập nhật: 2026-01-28

## Tổng quan dự án

| Metric | Value |
|--------|-------|
| **Trạng thái** | Planning Complete |
| **Tổng Epics** | 6 |
| **Tổng Stories** | 14 |
| **Hoàn thành** | 0 |
| **Progress** | 0% |

---

## Epics Overview

| Epic | Tên | Stories | Priority | Status |
|------|-----|---------|----------|--------|
| [epic-001](epic-001-setup/_overview.md) | Project Setup | 2 | P0 | Todo |
| [epic-002](epic-002-file-loading/_overview.md) | File Loading | 2 | P0 | Todo |
| [epic-003](epic-003-playback/_overview.md) | Media Playback | 3 | P0 | Todo |
| [epic-004](epic-004-navigation/_overview.md) | Chunk Navigation | 2 | P0 | Todo |
| [epic-005](epic-005-chunk-editor/_overview.md) | Chunk Editor | 3 | P0 | Todo |
| [epic-006](epic-006-progress/_overview.md) | Progress Tracking | 2 | P0 | Todo |

---

## Thứ tự Implement Khuyến Nghị

### Phase 1: Foundation (Stories 1-2)
Setup project và core infrastructure.

- [ ] [story-001](epic-001-setup/story-001.md): Project initialization
- [ ] [story-002](epic-001-setup/story-002.md): Core infrastructure (types, stores, utils)

### Phase 2: File Loading (Stories 3-4)
Load media và subtitle files.

- [ ] [story-003](epic-002-file-loading/story-003.md): FileLoader component
- [ ] [story-004](epic-002-file-loading/story-004.md): Media & subtitle loading logic

### Phase 3: Basic Playback (Stories 5-7)
Media player với loop và speed control.

- [ ] [story-005](epic-003-playback/story-005.md): MediaPlayer component
- [ ] [story-006](epic-003-playback/story-006.md): Loop functionality
- [ ] [story-007](epic-003-playback/story-007.md): Speed control

### Phase 4: Navigation (Stories 8-9)
ChunkList và keyboard shortcuts.

- [ ] [story-008](epic-004-navigation/story-008.md): ChunkList & navigation
- [ ] [story-009](epic-004-navigation/story-009.md): Keyboard shortcuts

### Phase 5: Chunk Editor (Stories 10-12)
Edit, merge, split chunks.

- [ ] [story-010](epic-005-chunk-editor/story-010.md): ChunkEditor & timing edit
- [ ] [story-011](epic-005-chunk-editor/story-011.md): Merge chunks
- [ ] [story-012](epic-005-chunk-editor/story-012.md): Split chunk

### Phase 6: Progress (Stories 13-14)
Save và resume progress.

- [ ] [story-013](epic-006-progress/story-013.md): Save progress
- [ ] [story-014](epic-006-progress/story-014.md): Resume session & mark done

---

## MVP Minimal Path

Nếu muốn ship nhanh nhất, có thể skip:
- Story 010-012 (Chunk Editor) → implement sau
- Hoặc chỉ implement Story 010 (timing edit only)

**Minimal MVP:** Stories 1-9, 13-14 = **11 stories**

---

## Dependencies Diagram

```
story-001 (Project init)
    │
    ▼
story-002 (Core infra)
    │
    ├────────────────────┐
    ▼                    ▼
story-003 (FileLoader)   │
    │                    │
    ▼                    │
story-004 (Load logic)   │
    │                    │
    ▼                    │
story-005 (MediaPlayer) ◄┘
    │
    ├───────────┬───────────┐
    ▼           ▼           ▼
story-006   story-007   story-008 (ChunkList)
(Loop)      (Speed)         │
                            ├───────────┐
                            ▼           ▼
                        story-009   story-010 (Edit)
                        (Shortcuts)     │
                            │           ├─────────┐
                            │           ▼         ▼
                            │       story-011 story-012
                            │       (Merge)   (Split)
                            ▼
                        story-013 (Save)
                            │
                            ▼
                        story-014 (Resume)
```

---

## Effort Summary

| Size | Count | Estimated Hours |
|------|-------|-----------------|
| S | 2 | 2-4h |
| M | 11 | 22-44h |
| L | 1 | 4-8h |
| **Total** | **14** | **28-56h** |

---

## Hướng dẫn

### Status Legend
- `todo` - Chưa bắt đầu
- `in-progress` - Đang làm
- `review` - Đang review
- `done` - Hoàn thành
- `blocked` - Bị block

### Effort Legend
- **XS** - < 30 phút
- **S** - 1-2 giờ
- **M** - 2-4 giờ
- **L** - 4-8 giờ
- **XL** - > 8 giờ (nên chia nhỏ)

### Priority
- **1** - Làm đầu tiên
- **2+** - Làm theo thứ tự

---

## Bắt đầu Development

Chạy command sau để bắt đầu story đầu tiên:

```
@dev story-001
```
