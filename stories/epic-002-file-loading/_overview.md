# Epic 002: File Loading

**ID:** epic-002-file-loading
**Priority:** P0
**Stories:** 2
**Progress:** 0%

## Mô tả

Implement khả năng load file media (video/audio) và subtitle (.srt) từ local filesystem.

Covers PRD User Stories:
- US-001: Load Media File
- US-002: Load Subtitle File

## User Stories thuộc Epic

| Story | Tên | Status | Effort |
|-------|-----|--------|--------|
| [story-003](story-003.md) | FileLoader component | Todo | M |
| [story-004](story-004.md) | Media & subtitle loading | Todo | M |

## Dependencies

- Depends on: Epic 001 (Project Setup)
- Required by: Epic 003, 004, 005, 006

## Technical Notes

- Sử dụng HTML5 File API
- Media files: tạo Object URL với `URL.createObjectURL()`
- Subtitle: read as text, parse với SRT parser
- Reference: [docs/prd.md - US-001, US-002](../../docs/prd.md)
