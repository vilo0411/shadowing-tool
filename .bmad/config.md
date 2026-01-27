# ⚙️ BMAD Configuration

> Cấu hình cho BMAD workflow trong dự án này

## Project Info

```yaml
project_name: "[Tên dự án]"
version: "0.1.0"
language: "vi"  # Ngôn ngữ output
```

## Agents

```yaml
agents:
  analyst:
    enabled: true
    output: "docs/brief.md"
    
  pm:
    enabled: true
    output: "docs/prd.md"
    
  architect:
    enabled: true
    output: "docs/architecture.md"
    
  sm:
    enabled: true
    output: "stories/"
    
  dev:
    enabled: true
    output: "src/"
    
  reviewer:
    enabled: true
    output: "explain/"
```

## Workflow Settings

```yaml
workflow:
  # Tự động suggest next step sau mỗi agent
  auto_suggest: true
  
  # Show progress bar
  show_progress: true
  
  # Require approval trước khi chuyển phase
  require_approval: false
```

## Code Conventions

```yaml
code:
  # Ngôn ngữ cho code comments
  comment_language: "en"
  
  # Style
  indent: 2
  quotes: "single"
  semicolons: false
  
  # Naming conventions
  components: "PascalCase"
  functions: "camelCase"
  constants: "SCREAMING_SNAKE_CASE"
  files:
    components: "PascalCase"
    utils: "camelCase"
```

## Documentation

```yaml
docs:
  # Ngôn ngữ documentation
  language: "vi"
  
  # Tự động tạo explain docs sau review
  auto_explain: true
  
  # Include code snippets trong explain
  include_code: true
```

## Story Settings

```yaml
stories:
  # Sizing scale
  sizes: ["XS", "S", "M", "L", "XL"]
  
  # Max size trước khi suggest chia nhỏ
  max_size: "L"
  
  # Status options
  statuses:
    - todo
    - in-progress
    - review
    - done
    - blocked
```

## Customization

### Thêm agent mới

1. Tạo file trong `.bmad/agents/new-agent.md`
2. Follow format của agents hiện có
3. Update `CLAUDE.md` để list agent mới

### Sửa template

1. Edit files trong `.bmad/templates/`
2. Agents sẽ dùng templates mới

### Sửa checklist

1. Edit files trong `.bmad/checklists/`
2. Agents sẽ validate theo checklists mới
