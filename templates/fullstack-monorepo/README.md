# Fullstack Monorepo Template

CLAUDE.md template for **Turborepo monorepos** with Next.js frontend + NestJS backend.

## What's included
- Root CLAUDE.md with monorepo-wide conventions
- `apps/web/CLAUDE.md` — frontend-specific context
- `apps/api/CLAUDE.md` — backend-specific context
- Workspace management patterns (pnpm workspaces)
- Shared packages strategy (types, validators, UI)

## Usage
```bash
cp templates/fullstack-monorepo/CLAUDE.md your-project/CLAUDE.md
cp templates/fullstack-monorepo/apps/web/CLAUDE.md your-project/apps/web/CLAUDE.md
cp templates/fullstack-monorepo/apps/api/CLAUDE.md your-project/apps/api/CLAUDE.md
```

## Why multiple CLAUDE.md files?
Claude Code reads the `CLAUDE.md` closest to your working directory. In a monorepo, the AI needs different context depending on which app you're working in. The root file covers shared conventions; app-level files cover specifics.

## Best for
- Full-stack TypeScript monorepos
- Projects with shared code between frontend and backend
- Teams using Turborepo or Nx
