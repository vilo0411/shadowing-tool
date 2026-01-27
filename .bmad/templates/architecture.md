# Architecture Document

**Dự án:** [Tên dự án]  
**Version:** 1.0  
**Cập nhật:** YYYY-MM-DD  
**Trạng thái:** 🟨 Draft | 🟩 Approved

---

## 1. Tech Stack

```yaml
Frontend:
  - Framework: [Next.js/React/Vue/...]
  - Language: [TypeScript/JavaScript]
  - Styling: [Tailwind/CSS Modules/...]
  - State Management: [Zustand/Redux/...]
  - Form Handling: [React Hook Form/...]

Backend:
  - Runtime: [Node.js/Python/...]
  - Framework: [Express/FastAPI/Next.js API/...]
  - Database: [PostgreSQL/MongoDB/...]
  - ORM: [Prisma/Drizzle/SQLAlchemy/...]
  - Cache: [Redis/...] (nếu cần)

Authentication:
  - Provider: [Supabase Auth/NextAuth/Clerk/...]
  - Method: [JWT/Session/OAuth]

Infrastructure:
  - Hosting: [Vercel/Railway/AWS/...]
  - Database Hosting: [Supabase/PlanetScale/...]
  - File Storage: [S3/Cloudflare R2/...] (nếu cần)
  - CI/CD: [GitHub Actions/...]

Development:
  - Package Manager: [npm/pnpm/yarn]
  - Linting: [ESLint]
  - Formatting: [Prettier]
  - Testing: [Jest/Vitest/...]
```

---

## 2. System Overview

```
┌──────────────────────────────────────────────────────────────────┐
│                           CLIENT                                  │
│  ┌─────────────────────────────────────────────────────────────┐ │
│  │                      Browser/App                             │ │
│  │  ┌───────────┐  ┌───────────┐  ┌───────────┐               │ │
│  │  │   Pages   │  │Components │  │  Stores   │               │ │
│  │  └───────────┘  └───────────┘  └───────────┘               │ │
│  └─────────────────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────┘
                              │
                              │ HTTP/WebSocket
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│                           SERVER                                  │
│  ┌─────────────────────────────────────────────────────────────┐ │
│  │                      API Layer                               │ │
│  │  ┌───────────┐  ┌───────────┐  ┌───────────┐               │ │
│  │  │  Routes   │  │Middleware │  │ Services  │               │ │
│  │  └───────────┘  └───────────┘  └───────────┘               │ │
│  └─────────────────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│                         DATA LAYER                                │
│  ┌───────────┐  ┌───────────┐  ┌───────────┐                    │
│  │ Database  │  │   Cache   │  │  Storage  │                    │
│  └───────────┘  └───────────┘  └───────────┘                    │
└──────────────────────────────────────────────────────────────────┘
```

---

## 3. Cấu trúc thư mục

```
src/
├── app/                        # Next.js App Router
│   ├── (auth)/                # Route group: Auth pages
│   │   ├── login/
│   │   └── register/
│   ├── (main)/                # Route group: Main app (protected)
│   │   ├── dashboard/
│   │   └── settings/
│   ├── api/                   # API Routes
│   │   └── [resource]/
│   ├── layout.tsx
│   └── page.tsx
│
├── components/
│   ├── ui/                    # Base UI components (Button, Input, etc.)
│   ├── features/              # Feature-specific components
│   │   ├── auth/
│   │   └── dashboard/
│   └── layouts/               # Layout components
│
├── lib/
│   ├── db.ts                  # Database client
│   ├── auth.ts                # Auth utilities
│   ├── api.ts                 # API client
│   └── utils.ts               # General utilities
│
├── hooks/                      # Custom React hooks
│   ├── use-auth.ts
│   └── use-[feature].ts
│
├── stores/                     # State management
│   └── use-[store].ts
│
├── types/                      # TypeScript types
│   ├── index.ts
│   └── [domain].ts
│
├── styles/                     # Global styles
│   └── globals.css
│
└── config/                     # App configuration
    └── site.ts
```

---

## 4. Data Model

### Entity Relationship Diagram

```
┌──────────────┐       ┌──────────────┐
│     User     │       │    [Entity]  │
├──────────────┤       ├──────────────┤
│ id           │───┐   │ id           │
│ email        │   │   │ userId       │──┐
│ name         │   │   │ [field]      │  │
│ createdAt    │   │   │ createdAt    │  │
└──────────────┘   │   └──────────────┘  │
                   │                      │
                   └──────────────────────┘
                         1:N relationship
```

### Schema Definition

```typescript
// User
interface User {
  id: string
  email: string
  name: string | null
  avatarUrl: string | null
  createdAt: Date
  updatedAt: Date
}

// [Other entities]
interface Entity {
  id: string
  userId: string
  // ... fields
  createdAt: Date
  updatedAt: Date
}
```

### Database Tables

```sql
-- Users table
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  name VARCHAR(255),
  avatar_url TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- [Other tables]
```

---

## 5. API Design

### REST Endpoints

| Method | Endpoint | Mô tả | Auth | Request | Response |
|--------|----------|-------|------|---------|----------|
| GET | `/api/users/me` | Get current user | ✅ | - | User |
| PATCH | `/api/users/me` | Update profile | ✅ | Partial<User> | User |
| GET | `/api/[resources]` | List resources | ✅ | Query params | Resource[] |
| POST | `/api/[resources]` | Create resource | ✅ | Resource | Resource |
| GET | `/api/[resources]/[id]` | Get single | ✅ | - | Resource |
| PATCH | `/api/[resources]/[id]` | Update | ✅ | Partial | Resource |
| DELETE | `/api/[resources]/[id]` | Delete | ✅ | - | - |

### Response Format

```typescript
// Success
{
  data: T,
  meta?: {
    page: number,
    limit: number,
    total: number
  }
}

// Error
{
  error: {
    code: string,
    message: string,
    details?: any
  }
}
```

---

## 6. Authentication Flow

```
┌─────────┐                  ┌─────────┐                  ┌─────────┐
│  User   │                  │ Client  │                  │ Server  │
└────┬────┘                  └────┬────┘                  └────┬────┘
     │                            │                            │
     │  1. Enter credentials      │                            │
     │ ──────────────────────────>│                            │
     │                            │                            │
     │                            │  2. POST /api/auth/login   │
     │                            │ ──────────────────────────>│
     │                            │                            │
     │                            │  3. Validate & create JWT  │
     │                            │ <──────────────────────────│
     │                            │                            │
     │                            │  4. Set cookie             │
     │                            │ ──────────────────────────>│
     │                            │                            │
     │  5. Redirect to dashboard  │                            │
     │ <──────────────────────────│                            │
     │                            │                            │
```

### Auth Implementation

```typescript
// Middleware: Protect routes
export async function middleware(request: NextRequest) {
  const session = await getSession()
  
  if (!session && isProtectedRoute(request.pathname)) {
    return NextResponse.redirect('/login')
  }
  
  return NextResponse.next()
}
```

---

## 7. Security Considerations

### Authentication
- [ ] JWT với expiration time hợp lý
- [ ] Refresh token rotation
- [ ] Secure cookie flags (httpOnly, secure, sameSite)

### Authorization
- [ ] Role-based access control (RBAC)
- [ ] Resource-level permissions

### Data Protection
- [ ] Input validation (zod/yup)
- [ ] SQL injection prevention (ORM)
- [ ] XSS prevention (React auto-escape)
- [ ] CSRF protection

### API Security
- [ ] Rate limiting
- [ ] Request size limits
- [ ] CORS configuration

---

## 8. Deployment Architecture

### Development

```
Local Machine
├── Next.js dev server (localhost:3000)
├── Database (Supabase dev project / local Postgres)
└── Hot reload enabled
```

### Production

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Vercel    │────▶│  Supabase   │────▶│   S3/R2     │
│  (Frontend  │     │  (Database  │     │  (Storage)  │
│   + API)    │     │   + Auth)   │     │             │
└─────────────┘     └─────────────┘     └─────────────┘
```

### Environment Variables

```bash
# .env.local (example)
DATABASE_URL=
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
NEXTAUTH_SECRET=
NEXTAUTH_URL=
```

---

## 9. Monitoring & Logging

### Error Tracking
- [ ] [Sentry/LogRocket/...]

### Analytics
- [ ] [Vercel Analytics/PostHog/...]

### Logging Strategy
- Development: Console logs
- Production: Structured JSON logs

---

## 10. Architecture Decision Records (ADRs)

### ADR-001: [Tên quyết định]

- **Date:** YYYY-MM-DD
- **Status:** Accepted
- **Context:** [Tình huống đặt ra quyết định]
- **Decision:** [Quyết định được đưa ra]
- **Rationale:** [Lý do chọn option này]
- **Consequences:** [Hệ quả tích cực và tiêu cực]
- **Alternatives Considered:**
  - Option A: [Pros/Cons]
  - Option B: [Pros/Cons]

---

## Appendix

### Useful Commands

```bash
# Development
npm run dev

# Build
npm run build

# Database
npx prisma migrate dev
npx prisma studio

# Deployment
vercel --prod
```

### References

- [[docs/prd]] - Product Requirements
- [[docs/brief]] - Project Brief
