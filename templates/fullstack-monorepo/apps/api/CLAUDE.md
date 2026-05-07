# CLAUDE.md — API Backend (Monorepo)

## Context
This is the **backend app** inside a Turborepo monorepo. Read the root `CLAUDE.md` for monorepo-wide conventions.

## Tech stack
- **Framework:** NestJS 10+
- **ORM:** Prisma / TypeORM
- **Database:** PostgreSQL
- **Validation:** `@repo/validators` (Zod schemas) + class-validator
- **Types:** `@repo/shared-types`

## Project structure
```
apps/api/
├── src/
│   ├── modules/      # Feature modules (Clean Architecture layers)
│   ├── common/       # Guards, filters, interceptors, pipes
│   ├── config/       # Environment config validation
│   ├── database/     # Migrations, seeds
│   ├── app.module.ts
│   └── main.ts
└── test/             # E2e tests
```

## Commands
```bash
pnpm dev --filter=api       # Dev server with hot reload
pnpm build --filter=api     # Build
pnpm test --filter=api      # Unit tests
pnpm test:e2e --filter=api  # E2e tests
```

## Key conventions
- Use shared Zod schemas from `@repo/validators` to validate request bodies
- Import types from `@repo/shared-types` for API contracts
- Repository pattern: domain layer depends on interfaces, not ORM directly
- Swagger docs auto-generated — decorators required on every endpoint
