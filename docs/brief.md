# Project Brief: Shadowing Tool

## Vấn đề

Luyện tập shadowing tiếng Anh với video/audio hiện tại khá bất tiện:
- Phải manually pause, rewind từng đoạn
- Không có cách split content thành chunks nhỏ dễ luyện
- Khó điều chỉnh tốc độ playback cho từng đoạn
- Không có flow học tập có hệ thống

## Người dùng mục tiêu

- **Primary:** Bản thân developer (personal tool)
- **Profile:** Người học tiếng Anh muốn cải thiện phát âm, ngữ điệu qua phương pháp shadowing
- **Use case:** Luyện tập với video/audio yêu thích (phim, podcast, YouTube...)

## Giải pháp đề xuất

Tool cho phép:
1. Load file audio/video local + subtitle (.srt)
2. Tự động split thành từng chunk theo subtitle
3. Luyện từng chunk với loop, điều chỉnh tốc độ
4. Next sang chunk tiếp khi đã ổn
5. Lưu và theo dõi progress học tập

## Core Features (MVP)

1. **Load Media + Subtitle**
   - Import file audio/video local
   - Parse file .srt để tách thành chunks
   - Hiển thị list các chunks

2. **Practice Mode**
   - Play chunk hiện tại
   - Loop (lặp lại chunk)
   - Speed control (0.5x - 1.5x)
   - Hiển thị subtitle text của chunk

3. **Navigation**
   - Next/Previous chunk
   - Jump to specific chunk
   - Keyboard shortcuts cho các actions

4. **Chunk Editor** *(NEW)*
   - Chỉnh sửa start/end time của chunk
   - Merge chunks (gộp 2+ chunks ngắn thành 1)
   - Split chunk (tách chunk dài thành nhiều phần)
   - Preview sau khi chỉnh sửa

5. **Progress Tracking** *(NEW)*
   - Lưu progress cho mỗi file (chunk nào đã học)
   - Hiển thị % hoàn thành
   - Tiếp tục từ chunk dừng lại lần trước

## Ngoài phạm vi (v1)

- ❌ Ghi âm giọng mình để so sánh
- ❌ Chấm điểm/feedback phát âm (AI)
- ❌ Auto-generate subtitle
- ❌ Import từ YouTube/Netflix trực tiếp
- ❌ Sync progress lên cloud (chỉ lưu local)
- ❌ Mobile app
- ❌ UI đẹp/fancy animations
- ❌ Đánh dấu chunk "khó" để review

## Đối thủ / Giải pháp hiện có

| Tên | Ưu điểm | Nhược điểm |
|-----|---------|------------|
| VLC Player | Có A-B repeat, speed control | Không có subtitle chunking, manual setup |
| Language Reactor | Tích hợp Netflix/YouTube tốt | Cần browser extension, không dùng local files |
| Youglish | Database lớn | Chỉ YouTube, không custom content |
| Audacity | Control tốt | Không có subtitle integration |

## Rủi ro & Giả định

- **Giả định:** User có sẵn file video/audio + .srt subtitle
- **Giả định:** .srt format đủ accurate để split chunks có nghĩa
- **Mitigated:** ~~Timing không chính xác~~ → Chunk Editor cho phép manual adjustment

## Câu hỏi mở

- [x] ~~Có cần lưu progress (chunk đã học) không?~~ → Có, lưu local
- [x] ~~Chunk quá dài/ngắn thì xử lý thế nào?~~ → Chunk Editor để manual adjust
- [ ] Có cần đánh dấu chunk "khó" để review lại không? → Tạm để ngoài scope v1
