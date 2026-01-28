# Epic 004: Chunk Navigation

**ID:** epic-004-navigation
**Priority:** P0
**Stories:** 2
**Progress:** 0%

## Mô tả

Implement navigation giữa các chunks: next/prev, jump to chunk, chunk list sidebar, và keyboard shortcuts.

Covers PRD User Stories:
- US-006: Navigate Chunks
- US-012: Keyboard Shortcuts Overview

## User Stories thuộc Epic

| Story | Tên | Status | Effort |
|-------|-----|--------|--------|
| [story-008](story-008.md) | ChunkList & Navigation | Todo | M |
| [story-009](story-009.md) | Keyboard shortcuts | Todo | M |

## Dependencies

- Depends on: Epic 003 (Playback)
- Required by: Epic 005, 006

## Technical Notes

- ChunkList nằm trong sidebar
- Keyboard shortcuts cần global event listener
- Reference: [docs/prd.md - Section 7](../../docs/prd.md)
