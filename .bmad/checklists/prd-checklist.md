# ✅ PRD Quality Checklist

> Checklist để đảm bảo PRD đủ chất lượng trước khi chuyển sang Architecture

## Completeness

### Problem & Solution
- [ ] Vấn đề được mô tả rõ ràng
- [ ] Giải pháp align với vấn đề
- [ ] Target user được xác định cụ thể

### User Stories
- [ ] Mỗi P0 feature có user story
- [ ] Format đúng: "Là X, tôi muốn Y, để Z"
- [ ] Acceptance criteria cụ thể, có thể verify
- [ ] Edge cases được xem xét

### Requirements
- [ ] Functional requirements đầy đủ cho MVP
- [ ] Non-functional requirements realistic
- [ ] UI/UX requirements đủ để design

## Quality

### Clarity
- [ ] Không có yêu cầu mơ hồ
- [ ] Mỗi requirement chỉ có một cách hiểu
- [ ] Technical jargon được giải thích (nếu có)

### Prioritization
- [ ] P0 = thực sự cần cho MVP
- [ ] P1, P2 phân biệt rõ ràng
- [ ] Không có scope creep so với brief

### Consistency
- [ ] Không có requirements mâu thuẫn
- [ ] Naming consistent
- [ ] Tham chiếu đúng (US-001, FR-001, etc.)

## Feasibility

### Technical
- [ ] Không có requirements không thể implement
- [ ] Độ phức tạp phù hợp solo developer

### Timeline
- [ ] Scope phù hợp với timeline (nếu có)
- [ ] Có thể deliver MVP trong reasonable time

## Traceability

### Links
- [ ] Link đến Brief
- [ ] Mỗi requirement có ID unique
- [ ] Dependencies được note

## Final Check

- [ ] Đọc lại toàn bộ PRD
- [ ] Không có câu hỏi mở blocking
- [ ] Ready cho @architect review
