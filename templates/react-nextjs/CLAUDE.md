# CLAUDE.md — React / Next.js

## Project overview
[Project name] is a [brief description]. Built with Next.js (App Router), React, and TypeScript.

## Tech stack
- **Framework:** Next.js 14+ (App Router)
- **Language:** TypeScript (strict mode)
- **Styling:** Tailwind CSS
- **State:** React Server Components + `use` hook for server state, Zustand for client state
- **Data fetching:** Server Components (default), React Query for client-side mutations
- **Auth:** NextAuth.js / Clerk
- **Database:** Prisma ORM + PostgreSQL
- **Testing:** Vitest + React Testing Library + Playwright (e2e)

## Project structure
```
src/
├── app/              # Next.js App Router pages and layouts
│   ├── (auth)/       # Auth-related routes (grouped)
│   ├── (dashboard)/  # Dashboard routes (grouped)
│   ├── api/          # API route handlers
│   ├── layout.tsx    # Root layout
│   └── page.tsx      # Home page
├── components/
│   ├── ui/           # Reusable UI primitives (Button, Input, Modal)
│   └── features/     # Feature-specific components (UserCard, ProjectList)
├── lib/              # Shared utilities, helpers, constants
├── hooks/            # Custom React hooks
├── types/            # TypeScript type definitions
├── styles/           # Global styles
└── __tests__/        # Test files mirroring src/ structure
```

## Development commands
```bash
npm run dev          # Start dev server (http://localhost:3000)
npm run build        # Production build
npm run lint         # ESLint
npm run test         # Vitest unit tests
npm run test:e2e     # Playwright e2e tests
npm run db:migrate   # Run Prisma migrations
npm run db:seed      # Seed database
```

## Code style and conventions
- Use functional components only — no class components
- Prefer Server Components by default; add `"use client"` only when needed (event handlers, hooks, browser APIs)
- File naming: `kebab-case.tsx` for components, `camelCase.ts` for utilities
- Component naming: PascalCase, matching file name
- One component per file — co-locate styles and tests
- Use `import type` for type-only imports
- Barrel exports (`index.ts`) only in `components/ui/`
- Avoid `any` — use `unknown` and narrow types

## Component patterns
- Props: define with `interface`, suffix with `Props` (e.g., `ButtonProps`)
- Default exports for page components, named exports for everything else
- Use `cn()` utility (clsx + tailwind-merge) for conditional classes
- Error boundaries: use `error.tsx` at route level
- Loading states: use `loading.tsx` and `<Suspense>` for streaming

## Data and state management
- Server Components fetch data directly (no useEffect for initial data)
- Use Server Actions for mutations (`"use server"`)
- Client state: Zustand stores in `lib/stores/`
- URL state: use `useSearchParams` for filters, pagination, sorting
- No prop drilling beyond 2 levels — use composition or context

## Testing guidelines
- Unit tests for utilities and hooks
- Component tests with React Testing Library — test behavior, not implementation
- E2e tests for critical user flows (auth, checkout, form submissions)
- Mock external APIs at the network level (MSW)
- Aim for 80% coverage on business logic, don't test styles

## Performance
- Images: always use `next/image` with width/height or fill
- Fonts: use `next/font` — no external font CDNs
- Dynamic imports for heavy components: `dynamic(() => import(...))`
- Avoid layout shifts — set explicit dimensions on media
- Use `React.memo` only when profiling shows re-render issues

## Security
- Validate all inputs with Zod (shared schemas for client + server)
- Sanitize user-generated content before rendering
- Use `headers()` and `cookies()` only in Server Components
- Environment variables: `NEXT_PUBLIC_` prefix only for client-safe values
- CSRF protection is built into Server Actions — use them for mutations
