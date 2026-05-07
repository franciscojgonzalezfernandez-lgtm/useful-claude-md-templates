# Advanced CLAUDE.md Patterns

## Multiple CLAUDE.md Files

Claude Code reads the CLAUDE.md closest to your working directory, walking up the tree. Use this for monorepos or large projects:

```
project/
├── CLAUDE.md               # Shared conventions
├── apps/
│   ├── web/CLAUDE.md        # Frontend-specific
│   └── api/CLAUDE.md        # Backend-specific
└── packages/
    └── ui/CLAUDE.md         # Component library-specific
```

Each sub-CLAUDE.md can reference the root: "See root CLAUDE.md for shared conventions."

## Context-Aware Sections

Structure your CLAUDE.md so the AI can quickly find relevant sections based on what it's working on:

```markdown
## When working on API endpoints
- Always add Swagger decorators
- Validate with class-validator
- Return consistent error format

## When working on React components
- Use the design system from `components/ui/`
- Test with React Testing Library
- Follow the compound component pattern for complex UI

## When writing tests
- Use factories for test data, not inline objects
- Mock at the boundary (HTTP, database), not internal functions
```

## Dynamic Context with .claude/ Directory

For complex projects, use the `.claude/` directory for additional context:

```
.claude/
├── settings.json          # Claude Code settings
└── commands/              # Custom slash commands
    ├── review.md          # /review command
    └── test-plan.md       # /test-plan command
```

## Linking to External Docs

Keep CLAUDE.md concise by linking to detailed docs:

```markdown
## Architecture
We follow Clean Architecture. See [architecture docs](./docs/ARCHITECTURE.md) for layer rules and dependency constraints.

## API Design
All endpoints follow our [API style guide](./docs/API_STYLE_GUIDE.md).
```

## Team-Specific Overrides

For teams where different developers have different preferences, use a personal override:

```
project/
├── CLAUDE.md              # Team conventions (committed)
└── .claude.local.md       # Personal preferences (gitignored)
```

Add `.claude.local.md` to `.gitignore`. Claude Code will read both files.

## Conditional Environment Instructions

```markdown
## Environment setup
- **Local dev:** `docker compose up -d` then `npm run dev`
- **CI:** Tests run in GitHub Actions, see `.github/workflows/test.yml`
- **Staging:** Auto-deployed from `develop` branch
- **Production:** Deployed from `main` via release tags
```

## Project-Specific Terminology

If your project has domain-specific terms, define them:

```markdown
## Glossary
- **Workspace:** a tenant in our multi-tenant system (not a code workspace)
- **Flow:** a user-defined automation pipeline (not a git flow)
- **Agent:** an AI worker process (not a browser user-agent)
```

This prevents the AI from misinterpreting domain terms.
