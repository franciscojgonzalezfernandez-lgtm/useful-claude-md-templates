# CLAUDE.md — Web Frontend (Monorepo)

## Context
This is the **frontend app** inside a Turborepo monorepo. Read the root `CLAUDE.md` for monorepo-wide conventions.

## Tech stack
- **Framework:** Next.js 14+ (App Router)
- **Styling:** Tailwind CSS
- **Shared UI:** `@repo/ui` package
- **Validation:** `@repo/validators` (Zod schemas)
- **Types:** `@repo/shared-types`

## Project structure
```
apps/web/
├── src/
│   ├── app/          # Pages and layouts (App Router)
│   ├── components/   # App-specific components
│   ├── hooks/        # Custom hooks
│   └── lib/          # Utilities, API client
├── public/           # Static assets
└── next.config.js    # Next.js config (transpilePackages for workspace deps)
```

## Commands
```bash
pnpm dev --filter=web    # Dev server
pnpm build --filter=web  # Build
pnpm test --filter=web   # Tests
```

## Key conventions
- Import shared components from `@repo/ui`, not local copies
- Use Zod schemas from `@repo/validators` for form validation
- API calls go through `lib/api-client.ts` — never call fetch directly in components
- Environment variables: `NEXT_PUBLIC_API_URL` points to the backend
