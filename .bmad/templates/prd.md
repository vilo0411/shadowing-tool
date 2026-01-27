# Product Requirements Document (PRD)

**Dự án:** [Tên dự án]  
**Version:** 1.0  
**Cập nhật:** YYYY-MM-DD  
**Trạng thái:** 🟨 Draft | 🟩 Approved

---

## 1. Tổng quan

### Vấn đề
[Tóm tắt từ brief]

### Giải pháp
[Mô tả solution rõ hơn]

### Mục tiêu thành công

| Metric | Baseline | Target | Cách đo |
|--------|----------|--------|---------|
| [Metric 1] | [Hiện tại] | [Mục tiêu] | [Method] |
| [Metric 2] | | | |

---

## 2. User Stories

### P0 - Must Have (MVP)

#### US-001: [Tên ngắn gọn]

**Là** [user type]  
**Tôi muốn** [action cụ thể]  
**Để** [benefit/value]

**Acceptance Criteria:**
- [ ] AC1: [Điều kiện cụ thể, có thể verify]
- [ ] AC2: [Điều kiện cụ thể]
- [ ] AC3: [Điều kiện cụ thể]

**Edge Cases:**
- Khi [điều kiện đặc biệt] → [expected behavior]
- Khi [error case] → [error handling]

---

#### US-002: [Tên]

**Là** [user type]  
**Tôi muốn** [action]  
**Để** [benefit]

**Acceptance Criteria:**
- [ ] AC1: 
- [ ] AC2: 

---

### P1 - Should Have

#### US-00X: [Tên]
...

---

### P2 - Nice to Have

#### US-00X: [Tên]
...

---

## 3. Functional Requirements

### FR-001: [Tên feature/module]

- **Mô tả:** [Chi tiết feature]
- **Input:** [User cung cấp gì]
- **Output:** [System trả về gì]
- **Business Rules:**
  - [Rule 1]
  - [Rule 2]
- **Validation:**
  - [Validation rule 1]

---

### FR-002: [Tên]
...

---

## 4. Non-Functional Requirements

### Performance
- [ ] Initial page load: < [X] seconds
- [ ] API response time: < [X] ms
- [ ] Support [X] concurrent users

### Security
- [ ] Authentication: [method - JWT/Session/OAuth]
- [ ] Authorization: [role-based/permission-based]
- [ ] Data encryption: [at rest/in transit]
- [ ] Input validation: [requirements]

### Reliability
- [ ] Uptime: [X]%
- [ ] Backup: [frequency]
- [ ] Error handling: [graceful degradation]

### Compatibility
- [ ] Browsers: [Chrome, Firefox, Safari, Edge]
- [ ] Devices: [Desktop, Tablet, Mobile]
- [ ] Screen sizes: [min width]

### Accessibility
- [ ] WCAG level: [A/AA/AAA]
- [ ] Keyboard navigation
- [ ] Screen reader support

---

## 5. UI/UX Requirements

### Screens

| # | Screen | Mục đích | Priority |
|---|--------|----------|----------|
| 1 | [Screen name] | [Purpose] | P0 |
| 2 | [Screen name] | [Purpose] | P0 |

### UI States (cho mỗi screen)

- **Loading:** [Skeleton/Spinner/Progress]
- **Empty:** [Message + CTA]
- **Error:** [Error message + retry option]
- **Success:** [Feedback]

### Navigation Flow

```
Landing Page
    ↓
Login/Register
    ↓
Dashboard
    ├── Feature A
    ├── Feature B
    └── Settings
```

---

## 6. Data Requirements

### Data to Collect
| Data | Source | Required | Notes |
|------|--------|----------|-------|
| [Field] | [User input/System] | Y/N | |

### Data Retention
- [Policy về data retention]

### Privacy
- [GDPR/Privacy requirements]

---

## 7. Integration Requirements

| System | Purpose | Type | Priority |
|--------|---------|------|----------|
| [Service] | [What for] | API/OAuth/Webhook | P0/P1 |

---

## 8. Ngoài phạm vi (v1)

- [Feature X] - sẽ xem xét cho v2
- [Feature Y] - cần thêm research

---

## 9. Assumptions & Dependencies

### Assumptions
- [Assumption 1]
- [Assumption 2]

### Dependencies
- [Dependency 1]
- [Dependency 2]

---

## 10. Câu hỏi mở

- [ ] [Question 1]
- [ ] [Question 2]

---

## Appendix

### Glossary
| Term | Definition |
|------|------------|
| [Term] | [Definition] |

### References
- [[docs/brief]] - Project Brief
