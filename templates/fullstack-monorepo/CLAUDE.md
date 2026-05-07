# CLAUDE.md — Fullstack Monorepo (Root)

## Project overview
[Project name] is a [brief description]. Monorepo managed with Turborepo, containing a Next.js frontend and NestJS backend with shared packages.

## Tech stack
- **Monorepo:** Turborepo + pnpm workspaces
- **Frontend:** Next.js (App Router), React, Tailwind CSS
- **Backend:** NestJS, TypeORM/Prisma, PostgreSQL
- **Shared:** TypeScript, Zod schemas, shared types
- **Testing:** Vitest (frontend), Jest (backend), Playwright (e2e)
- **CI/CD:** GitHub Actions
- **Containerization:** Docker Compose (dev), multi-stage Dockerfiles (prod)

## Monorepo structure
```
/
├── apps/
│   ├── web/              # Next.js frontend (see apps/web/CLAUDE.md)
│   └── api/              # NestJS backend (see apps/api/CLAUDE.md)
├── packages/
│   ├── shared-types/     # TypeScript interfaces shared between apps
│   ├── validators/       # Zod schemas used by both frontend and backend
│   ├── ui/               # Shared React component library
│   ├── config-eslint/    # Shared ESLint config
│   └── config-ts/        # Shared tsconfig
├── docker-compose.yml    # Local dev environment
├── turbo.json            # Turborepo pipeline config
├── pnpm-workspace.yaml   # Workspace definition
└── package.json          # Root scripts and devDependencies
```

## Development commands
```bash
pnpm install             # Install all dependencies
pnpm dev                 # Start all apps in parallel
pnpm dev --filter=web    # Start only frontend
pnpm dev --filter=api    # Start only backend
pnpm build               # Build all apps (respects dependency graph)
pnpm lint                # Lint all packages
pnpm test                # Run all tests
pnpm test --filter=api   # Run backend tests only
docker compose up -d     # Start database and services
```

## Workspace conventions
- Shared packages are imported via workspace protocol: `"@repo/shared-types": "workspace:*"`
- Changes to `packages/` auto-trigger rebuilds in dependent apps via Turborepo
- Each app has its own `CLAUDE.md` for app-specific context (see `apps/web/CLAUDE.md`, `apps/api/CLAUDE.md`)
- Environment variables: `.env` at root for shared, `.env` in each app for app-specific
- Never import directly between `apps/` — always go through `packages/`

## Code style
- TypeScript strict mode in all packages
- Shared types: define once in `packages/shared-types`, import everywhere
- Validation: define Zod schemas in `packages/validators`, use in both frontend forms and backend DTOs
- Prefer composition over inheritance
- Keep packages focused — one purpose per package

## Testing strategy
- **Unit tests:** each package and app has co-located tests
- **Integration tests:** API tests with test database in `apps/api/`
- **E2e tests:** Playwright in `apps/web/` against running backend
- **CI pipeline:** lint → type-check → unit tests → build → e2e tests

## Dependency management
- `pnpm` only — no npm or yarn
- Shared devDependencies at root (TypeScript, ESLint, Prettier)
- App-specific dependencies in each app's `package.json`
- Update shared packages atomically (single PR, single version bump)
