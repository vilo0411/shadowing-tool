# 🚀 BMAD + Obsidian Workflow Template

Template cho workflow phát triển phần mềm với **Obsidian** (Planning/PM) và **Claude Code** (Execution).

---

## 📋 Giới thiệu

Template này giúp bạn:

1. **Quản lý dự án** - Sử dụng Obsidian như PM tool
2. **Planning có cấu trúc** - Từ idea → brief → PRD → architecture → stories
3. **Vibe coding hiệu quả** - Claude Code thực thi theo plan rõ ràng
4. **Hiểu code của mình** - Tự động tạo documentation giải thích code

---

## 🏁 Quick Start

### Bước 1: Tạo project mới

```bash
# Option A: Từ GitHub template
gh repo create my-project --template your-username/bmad-obsidian-template

# Option B: Clone và copy
git clone https://github.com/your-username/bmad-obsidian-template
cp -r bmad-obsidian-template my-project
cd my-project
rm -rf .git && git init
```

### Bước 2: Mở trong Obsidian

1. Mở Obsidian
2. "Open folder as vault" → chọn folder project
3. Cài plugins (xem bên dưới)

### Bước 3: Customize CLAUDE.md

Mở `CLAUDE.md` và điền thông tin project của bạn.

### Bước 4: Bắt đầu planning

Trong Claude Code:
```
@analyst Tôi muốn build một app [mô tả ý tưởng]...
```

---

## 📁 Cấu trúc folder

```
📂 project/
├── 📄 CLAUDE.md              # ⭐ Context chính cho Claude Code
├── 📄 README.md
│
├── 📂 .bmad/                 # Cấu hình BMAD
│   ├── 📂 agents/           # 6 AI agents
│   ├── 📂 templates/        # Document templates
│   └── 📂 checklists/       # Quality checklists
│
├── 📂 docs/                  # Planning documents
│   ├── brief.md             # @analyst output
│   ├── prd.md               # @pm output
│   ├── architecture.md      # @architect output
│   └── decisions.md         # ADRs
│
├── 📂 stories/               # Task management
│   ├── _backlog.md          # Dashboard (Dataview)
│   └── epic-xxx/            # Stories theo epic
│
├── 📂 explain/               # Code explanations
│   └── _index.md            # Mục lục docs
│
├── 📂 journal/               # Notes & ideas
│   └── ideas.md
│
└── 📂 src/                   # Source code
```

---

## 🤖 Agents

| Agent | Command | Mục đích |
|-------|---------|----------|
| **Analyst** | `@analyst` | Phân tích idea, tạo Brief |
| **PM** | `@pm` | Tạo PRD từ Brief |
| **Architect** | `@architect` | Thiết kế hệ thống, gợi ý tech stack |
| **Scrum Master** | `@sm` | Tạo Stories từ Architecture |
| **Developer** | `@dev [story-id]` | Implement code |
| **Reviewer** | `@reviewer` | Review code, tạo explanations |

### Commands phụ

| Command | Mục đích |
|---------|----------|
| `@agent revise` | Sửa output theo feedback |
| `@agent redo` | Làm lại từ đầu |
| `@agent explain` | Giải thích output |

---

## 🔄 Workflow

```
                    ┌─────────────────────────────────────┐
                    │           PLANNING PHASE            │
                    │                                     │
  Ý tưởng ──────▶   │  @analyst ─▶ @pm ─▶ @architect     │
                    │      ↓        ↓         ↓          │
                    │   brief    prd    architecture     │
                    └─────────────────────────────────────┘
                                    │
                                    ▼
                    ┌─────────────────────────────────────┐
                    │          DEVELOPMENT CYCLE          │
                    │                                     │
                    │  @sm ─────▶ @dev ─────▶ @reviewer  │
                    │    ↓          ↓           ↓        │
                    │ stories    code      explain/      │
                    │                                     │
                    │         ◀── iterate ──▶            │
                    └─────────────────────────────────────┘
```

### Chi tiết từng bước

1. **@analyst** - Brainstorm, hỏi clarifying questions, tạo brief
2. **@pm** - Chuyển brief thành PRD với user stories
3. **@architect** - Phân tích, **gợi ý tech stack**, thiết kế hệ thống
4. **@sm** - Chia thành epics và stories
5. **@dev** - Implement từng story
6. **@reviewer** - Review code + **tạo documentation giải thích**

### Revision Flow

Không hài lòng với output? Có 2 cách:

```
# Cách 1: Nói tiếp trong conversation
Bạn: [Feedback của bạn]

# Cách 2: Dùng revise command
Bạn: @agent revise
     - Điểm 1 cần sửa
     - Điểm 2 cần sửa
```

---

## 🔌 Obsidian Plugins

### Bắt buộc

| Plugin | Mục đích |
|--------|----------|
| **Dataview** | Queries trong backlog dashboard |
| **Templater** | Tạo files từ templates nhanh |

### Khuyến khích

| Plugin | Mục đích |
|--------|----------|
| **Git** | Auto-sync với GitHub |
| **Kanban** | Visual board cho stories |

### Cài đặt

1. Settings → Community plugins → Browse
2. Search và install từng plugin
3. Enable plugins

---

## 📊 Dataview Queries

Backlog dashboard (`stories/_backlog.md`) sử dụng Dataview để:
- List stories đang làm
- List stories theo priority
- Track progress

Để queries hoạt động, stories cần có frontmatter đúng format:

```yaml
---
id: story-001
status: todo
priority: 1
effort: M
epic: epic-001
---
```

---

## 💡 Tips

### Daily routine

1. Mở `CLAUDE.md` - update current goals
2. Check `stories/_backlog.md` - xem task cần làm
3. Chạy `@dev [story-id]` - bắt đầu code
4. Chạy `@reviewer` - review và tạo docs

### Khi gặp vấn đề

- **Không hiểu code?** → `@reviewer explain [topic]`
- **Cần sửa plan?** → `@agent revise [feedback]`
- **Muốn thay đổi approach?** → `@agent redo [new direction]`

### Best practices

- Update `CLAUDE.md` thường xuyên
- Commit nhỏ, thường xuyên
- Đọc `explain/` docs khi quên code làm gì
- Log decisions vào `docs/decisions.md`

---

## 🔗 Links

- [BMAD Method](https://github.com/bmad-code-org/BMAD-METHOD) - Original framework
- [Dataview Plugin](https://github.com/blacksmithgu/obsidian-dataview)
- [Templater Plugin](https://github.com/SilentVoid13/Templater)

---

## 📝 License

MIT - Sử dụng tự do, customize theo nhu cầu!
