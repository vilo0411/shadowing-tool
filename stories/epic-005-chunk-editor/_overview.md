# Epic 005: Chunk Editor

**ID:** epic-005-chunk-editor
**Priority:** P0
**Stories:** 3
**Progress:** 0%

## Mô tả

Implement khả năng chỉnh sửa chunks: edit timing, merge nhiều chunks, split chunk dài.

Covers PRD User Stories:
- US-007: Edit Chunk Timing
- US-008: Merge Chunks
- US-009: Split Chunk

## User Stories thuộc Epic

| Story | Tên | Status | Effort |
|-------|-----|--------|--------|
| [story-010](story-010.md) | ChunkEditor & timing edit | Todo | M |
| [story-011](story-011.md) | Merge chunks | Todo | M |
| [story-012](story-012.md) | Split chunk | Todo | M |

## Dependencies

- Depends on: Epic 004 (Navigation)
- Nice to have, có thể skip cho MVP minimal

## Technical Notes

- Edits stored separately from original chunks
- Can reset to original
- Preview before save
- Reference: [docs/architecture.md - ADR-004](../../docs/architecture.md)
