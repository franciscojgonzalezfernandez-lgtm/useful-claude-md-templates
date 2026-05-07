# How to Write an Effective CLAUDE.md

## What is CLAUDE.md?

CLAUDE.md is a configuration file that gives Claude Code (and other AI coding assistants) context about your project. It lives in your project root and is automatically read when you start a session.

Think of it as onboarding documentation — but for AI instead of new developers.

## Essential Sections

### 1. Project Overview (required)
One or two sentences explaining what the project does and who it's for. This helps the AI understand the domain.

```markdown
## Project overview
TaskFlow is a project management SaaS for small teams. Built with Next.js and NestJS.
```

### 2. Tech Stack (required)
List your actual technologies. Be specific about versions when it matters.

```markdown
## Tech stack
- **Framework:** Next.js 14 (App Router)
- **Language:** TypeScript (strict mode)
- **Database:** PostgreSQL + Prisma
```

### 3. Project Structure (required)
Show your directory layout. This is the single most impactful section — it tells the AI where to find things.

```markdown
## Project structure
src/
├── app/          # Next.js pages
├── components/   # React components
├── lib/          # Utilities
└── types/        # TypeScript types
```

### 4. Commands (required)
How to run, build, test, and lint.

```markdown
## Commands
npm run dev      # Start dev server
npm run test     # Run tests
npm run lint     # Lint code
```

### 5. Code Conventions (recommended)
Your team's style preferences. The AI will follow these.

```markdown
## Code conventions
- Functional components only
- Use `interface` over `type` for object shapes
- Named exports, no default exports
```

### 6. Architecture Decisions (recommended)
Explain non-obvious choices so the AI doesn't "fix" your intentional patterns.

```markdown
## Architecture
We use the Repository pattern. Controllers never access the database directly.
```

## Writing Tips

**Be specific, not generic.** "Use TypeScript" is less useful than "TypeScript strict mode, no `any`, use `unknown` and narrow."

**Include what to avoid.** AI assistants are eager to help — tell them what NOT to do.

```markdown
- Do NOT add comments to obvious code
- Do NOT use class components
- Do NOT install new dependencies without asking
```

**Keep it under 200 lines.** Long files get truncated. Focus on what matters most.

**Update it regularly.** As your project evolves, your CLAUDE.md should too.

## What NOT to Include

- Sensitive information (API keys, passwords, internal URLs)
- Temporary debugging instructions
- Meeting notes or team processes
- Exhaustive API documentation (link to it instead)
