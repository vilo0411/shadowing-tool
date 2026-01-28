# Product Requirements Document (PRD)

**Dự án:** Shadowing Tool
**Version:** 1.0
**Cập nhật:** 2026-01-28
**Trạng thái:** Draft

---

## 1. Tổng quan

### Vấn đề

Luyện tập shadowing tiếng Anh với video/audio hiện tại khá bất tiện:
- Phải manually pause, rewind từng đoạn
- Không có cách split content thành chunks nhỏ dễ luyện
- Khó điều chỉnh tốc độ playback cho từng đoạn
- Không có flow học tập có hệ thống

### Giải pháp

Tool cho phép user load file audio/video local kèm subtitle (.srt), tự động split thành từng chunk theo subtitle lines. User luyện từng chunk với loop, điều chỉnh tốc độ, và có thể chỉnh sửa chunk khi cần. Progress được lưu local để tiếp tục học.

### Mục tiêu thành công

| Metric | Hiện tại | Mục tiêu | Cách đo |
|--------|----------|----------|---------|
| Thời gian setup 1 file | ~5 phút (manual VLC) | < 30 giây | Từ lúc chọn file đến bắt đầu luyện |
| Chunks có thể luyện | Phải manual set A-B | 100% subtitle lines | Số chunks parsed / tổng lines |
| Resume progress | Không có | Có | Tiếp tục đúng chunk đã dừng |

---

## 2. User Stories

### P0 - Must Have (MVP)

#### US-001: Load Media File
**Là** người học tiếng Anh
**Tôi muốn** load file video/audio từ máy tính
**Để** bắt đầu luyện shadowing với content mình chọn

**Acceptance Criteria:**
- [ ] AC1: Có thể chọn file từ file picker
- [ ] AC2: Hỗ trợ formats: mp4, mp3, webm, wav, m4a
- [ ] AC3: File được load và có thể play được
- [ ] AC4: Hiển thị tên file và duration sau khi load

**Edge Cases:**
- File corrupt/không đọc được → hiển thị error message rõ ràng
- File quá lớn → không giới hạn (browser tự handle)

---

#### US-002: Load Subtitle File
**Là** người học tiếng Anh
**Tôi muốn** load file .srt đi kèm video/audio
**Để** có text hiển thị và tự động split thành chunks

**Acceptance Criteria:**
- [ ] AC1: Có thể chọn file .srt từ file picker
- [ ] AC2: Parse được .srt format chuẩn (index, timestamp, text)
- [ ] AC3: Hiển thị tổng số chunks sau khi parse
- [ ] AC4: Mỗi subtitle line = 1 chunk (default)

**Edge Cases:**
- File .srt encoding khác UTF-8 → cố gắng detect, nếu fail thì hiển thị warning
- .srt format sai → hiển thị error với line number bị lỗi
- .srt không khớp duration với media → warning nhưng vẫn cho dùng

---

#### US-003: Practice Chunk
**Là** người học tiếng Anh
**Tôi muốn** luyện từng chunk một
**Để** tập trung vào từng đoạn ngắn

**Acceptance Criteria:**
- [ ] AC1: Play chunk từ start time đến end time
- [ ] AC2: Hiển thị subtitle text của chunk hiện tại
- [ ] AC3: Có thể pause/resume
- [ ] AC4: Tự động dừng khi hết chunk (không tự next)

**Edge Cases:**
- Chunk rất ngắn (< 1s) → vẫn play bình thường
- Chunk rất dài (> 30s) → vẫn play bình thường (user có thể split sau)

---

#### US-004: Loop Chunk
**Là** người học tiếng Anh
**Tôi muốn** lặp lại chunk hiện tại nhiều lần
**Để** luyện đến khi thuộc

**Acceptance Criteria:**
- [ ] AC1: Toggle loop on/off
- [ ] AC2: Khi loop on: tự động replay chunk khi hết
- [ ] AC3: Hiển thị trạng thái loop (on/off) rõ ràng
- [ ] AC4: Keyboard shortcut cho toggle loop

---

#### US-005: Speed Control
**Là** người học tiếng Anh
**Tôi muốn** điều chỉnh tốc độ playback
**Để** nghe chậm hơn khi đoạn khó

**Acceptance Criteria:**
- [ ] AC1: Tốc độ từ 0.5x đến 1.5x
- [ ] AC2: Step: 0.25x (0.5, 0.75, 1.0, 1.25, 1.5)
- [ ] AC3: Hiển thị tốc độ hiện tại
- [ ] AC4: Tốc độ được giữ khi chuyển chunk
- [ ] AC5: Keyboard shortcut cho tăng/giảm speed

---

#### US-006: Navigate Chunks
**Là** người học tiếng Anh
**Tôi muốn** di chuyển giữa các chunks
**Để** học theo thứ tự hoặc skip đến đoạn cần luyện

**Acceptance Criteria:**
- [ ] AC1: Next/Previous chunk buttons
- [ ] AC2: Hiển thị chunk list (có thể scroll)
- [ ] AC3: Click vào chunk trong list để jump đến
- [ ] AC4: Hiển thị current chunk index / total (e.g., "15/120")
- [ ] AC5: Keyboard shortcuts: Arrow keys hoặc J/K

**Edge Cases:**
- Đang ở chunk đầu tiên, bấm Previous → không làm gì (hoặc wrap to last)
- Đang ở chunk cuối cùng, bấm Next → không làm gì (hoặc wrap to first)

---

#### US-007: Edit Chunk Timing
**Là** người học tiếng Anh
**Tôi muốn** chỉnh sửa start/end time của chunk
**Để** fix khi timing trong .srt không chính xác

**Acceptance Criteria:**
- [ ] AC1: Có thể edit start time (input hoặc drag)
- [ ] AC2: Có thể edit end time (input hoặc drag)
- [ ] AC3: Preview chunk mới ngay sau khi edit
- [ ] AC4: Save changes (lưu vào session, không modify file gốc)

**Edge Cases:**
- Start time > End time → không cho phép, hiển thị error
- Edit làm chunk overlap với chunk khác → warning nhưng vẫn cho phép

---

#### US-008: Merge Chunks
**Là** người học tiếng Anh
**Tôi muốn** gộp nhiều chunks ngắn thành 1 chunk dài
**Để** luyện cả câu dài liền mạch

**Acceptance Criteria:**
- [ ] AC1: Chọn 2+ chunks liên tiếp để merge
- [ ] AC2: Merged chunk có: start = first chunk start, end = last chunk end
- [ ] AC3: Text được gộp lại (có separator như newline)
- [ ] AC4: Preview trước khi confirm merge

---

#### US-009: Split Chunk
**Là** người học tiếng Anh
**Tôi muốn** tách chunk dài thành nhiều chunks nhỏ
**Để** luyện từng phần của câu dài

**Acceptance Criteria:**
- [ ] AC1: Chọn điểm split (timestamp) trong chunk
- [ ] AC2: Tạo 2 chunks mới từ 1 chunk
- [ ] AC3: Text chia theo tỷ lệ thời gian (hoặc manual edit)
- [ ] AC4: Preview trước khi confirm split

---

#### US-010: Save Progress
**Là** người học tiếng Anh
**Tôi muốn** progress được lưu lại
**Để** tiếp tục từ nơi dừng lại

**Acceptance Criteria:**
- [ ] AC1: Tự động save khi đánh dấu chunk "done"
- [ ] AC2: Lưu: file path, current chunk index, chunks đã done
- [ ] AC3: Lưu vào localStorage (browser) hoặc local file
- [ ] AC4: Hiển thị % progress (chunks done / total)

**Edge Cases:**
- File bị rename/move → không tìm thấy, hiển thị warning
- localStorage bị clear → mất progress, bắt đầu lại

---

#### US-011: Resume Session
**Là** người học tiếng Anh
**Tôi muốn** tiếp tục session cũ
**Để** không phải setup lại từ đầu

**Acceptance Criteria:**
- [ ] AC1: Khi load file đã học → hỏi có muốn resume không
- [ ] AC2: Nếu resume: jump đến chunk đã dừng, restore progress
- [ ] AC3: Nếu không: bắt đầu fresh, clear progress cũ

---

### P1 - Should Have

#### US-012: Keyboard Shortcuts Overview
**Là** người học tiếng Anh
**Tôi muốn** xem danh sách keyboard shortcuts
**Để** thao tác nhanh hơn

**Acceptance Criteria:**
- [ ] AC1: Hiển thị shortcut list (modal hoặc panel)
- [ ] AC2: Có thể mở bằng `?` hoặc button

---

#### US-013: Mark Chunk as Done
**Là** người học tiếng Anh
**Tôi muốn** đánh dấu chunk đã học xong
**Để** track progress và skip khi review

**Acceptance Criteria:**
- [ ] AC1: Toggle done/not done cho chunk hiện tại
- [ ] AC2: Hiển thị visual indicator (checkmark, highlight)
- [ ] AC3: Keyboard shortcut để mark done + auto next

---

### P2 - Nice to Have

#### US-014: Export Edited Chunks
**Là** người học tiếng Anh
**Tôi muốn** export chunks đã edit thành file .srt mới
**Để** dùng lại hoặc share

#### US-015: Dark Mode
**Là** người học tiếng Anh
**Tôi muốn** có dark mode
**Để** học ban đêm không mỏi mắt

---

## 3. Functional Requirements

### FR-001: SRT Parser
- **Mô tả:** Parse file .srt thành array of chunks
- **Input:** File .srt (text content)
- **Output:** Array of `{ index, startTime, endTime, text }`
- **Business Rules:**
  - startTime và endTime format: `HH:MM:SS,mmm`
  - Hỗ trợ multi-line text trong 1 subtitle entry
  - Bỏ qua blank lines và invalid entries

### FR-002: Media Player Control
- **Mô tả:** Control playback của audio/video
- **Input:** Commands (play, pause, seek, setSpeed)
- **Output:** Playback state changes
- **Business Rules:**
  - Seek precision: ±100ms là acceptable
  - Speed không ảnh hưởng pitch (nếu browser hỗ trợ)

### FR-003: Progress Storage
- **Mô tả:** Lưu và load progress
- **Input:** Progress data (file path, chunks status)
- **Output:** Saved/loaded data
- **Business Rules:**
  - Key storage by file path (normalized)
  - Auto-save khi có changes
  - Max storage: 100 files (xóa cũ nhất nếu quá)

---

## 4. Non-Functional Requirements

### Performance
- [ ] Initial load < 3s
- [ ] Parse .srt file (1000 lines) < 500ms
- [ ] Seek to chunk < 200ms
- [ ] UI responsive (no lag khi thao tác)

### Compatibility
- [ ] Browsers: Chrome, Firefox, Safari (latest 2 versions)
- [ ] OS: macOS, Windows (no mobile for v1)

### Usability
- [ ] Có thể dùng 100% bằng keyboard
- [ ] UI đơn giản, không cần hướng dẫn

---

## 5. UI/UX Requirements

### Screens/Views cần có

1. **Home/Load View** - Chọn media + subtitle files
2. **Practice View** - Main view để luyện tập
3. **Chunk List Panel** - Sidebar hiển thị all chunks
4. **Edit Chunk Modal** - Chỉnh sửa timing của chunk

### Layout Practice View

```
+------------------------------------------+
|  [File name]              [Progress: 45%] |
+------------------------------------------+
|                                          |
|           [ Video/Audio Player ]         |
|                                          |
+------------------------------------------+
|  "This is the subtitle text"             |
+------------------------------------------+
|  [<<] [Play/Pause] [>>]  [Loop] [0.75x]  |
|                          [Mark Done]     |
+------------------------------------------+
|  Chunk List (scrollable sidebar)         |
|  - [x] 1. Hello world                    |
|  - [ ] 2. How are you  <-- current       |
|  - [ ] 3. I'm fine                       |
+------------------------------------------+
```

### States

**Loading state:**
- Hiển thị spinner khi đang load file

**Empty state:**
- Khi chưa load file: hiển thị dropzone hoặc button "Load files"

**Error state:**
- Khi file lỗi: hiển thị error message + action (try again, pick different file)

---

## 6. Ngoài phạm vi (v1)

- Ghi âm giọng mình để so sánh
- AI chấm điểm phát âm
- Auto-generate subtitle (Whisper, etc.)
- Import từ YouTube/Netflix
- Sync progress lên cloud
- Mobile app
- Đánh dấu chunk "khó" để review riêng
- Export progress report
- Multiple subtitle tracks

---

## 7. Keyboard Shortcuts (Reference)

| Action | Shortcut |
|--------|----------|
| Play/Pause | `Space` |
| Next chunk | `→` hoặc `J` |
| Previous chunk | `←` hoặc `K` |
| Toggle loop | `L` |
| Speed up | `]` |
| Speed down | `[` |
| Mark done | `Enter` |
| Show shortcuts | `?` |

---

## 8. Câu hỏi mở

- [ ] Có cần undo cho chunk edits không?
- [ ] Chunk list sort order: by index hay by done status?
- [ ] Có cần filter chunks (all/done/not done)?

---

## Checklist Quality

- [x] Mỗi user story có acceptance criteria
- [x] P0 features đủ cho MVP hoạt động
- [x] Edge cases được xem xét
- [x] NFRs realistic cho solo dev
- [x] Không có scope creep so với brief
