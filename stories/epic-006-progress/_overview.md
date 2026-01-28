# Epic 006: Progress Tracking

**ID:** epic-006-progress
**Priority:** P0
**Stories:** 2
**Progress:** 0%

## Mô tả

Implement lưu và khôi phục progress học tập: save chunks đã done, resume session.

Covers PRD User Stories:
- US-010: Save Progress
- US-011: Resume Session
- US-013: Mark Chunk as Done

## User Stories thuộc Epic

| Story | Tên | Status | Effort |
|-------|-----|--------|--------|
| [story-013](story-013.md) | Save progress | Todo | M |
| [story-014](story-014.md) | Resume & mark done | Todo | M |

## Dependencies

- Depends on: Epic 004 (Navigation)
- Final epic, completes MVP

## Technical Notes

- Progress saved to localStorage
- Key by file identifier (name + size hash)
- Auto-save on changes
- Reference: [docs/architecture.md - FR-003](../../docs/architecture.md)
