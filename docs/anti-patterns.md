# CLAUDE.md Anti-Patterns

Common mistakes that reduce the effectiveness of your CLAUDE.md.

## 1. Too Vague

**Bad:**
```markdown
## Tech stack
JavaScript, some framework, database
```

**Good:**
```markdown
## Tech stack
- TypeScript 5.3 (strict mode)
- Next.js 14 (App Router, not Pages Router)
- PostgreSQL 16 + Prisma 5
```

The AI can't help effectively if it doesn't know what you're working with.

## 2. Too Long

CLAUDE.md files over 200 lines risk being truncated. If you have more to say, split into multiple files:

```
CLAUDE.md            # Core context (keep under 200 lines)
docs/ARCHITECTURE.md # Detailed architecture docs
docs/API.md          # API conventions
```

Reference them from CLAUDE.md: "See `docs/ARCHITECTURE.md` for detailed layer descriptions."

## 3. Copy-Pasted Documentation

Your CLAUDE.md is NOT your README. It's not for humans browsing GitHub — it's operational context for an AI agent. Focus on *how to work with the code*, not what the project does for end users.

## 4. No Project Structure

This is the #1 missed opportunity. Without a directory layout, the AI wastes time searching for files. Always include a `## Project structure` section.

## 5. Contradictory Instructions

```markdown
## Conventions
- Use named exports
- Export components as default  ← contradicts the line above
```

Review your CLAUDE.md for internal consistency.

## 6. Outdated Information

A CLAUDE.md that says "we use Webpack" when you migrated to Vite six months ago will actively mislead the AI. Treat it like code — update it when things change.

## 7. Including Secrets

```markdown
## Environment
DATABASE_URL=postgresql://user:password@...  ← NEVER do this
```

CLAUDE.md is checked into version control. Never include credentials, API keys, or internal URLs.

## 8. No Commands Section

If the AI doesn't know how to run your project, it can't verify its own changes. Always include dev, build, test, and lint commands.

## 9. Framework Defaults as Instructions

Don't tell the AI things that are already standard for your framework:

```markdown
- Use JSX for React components  ← obvious
- Import modules with `import`  ← obvious
```

Focus on YOUR conventions that differ from defaults.

## 10. Ignoring the "Don't" List

Telling the AI what TO do is important. Telling it what NOT to do is equally valuable:

```markdown
## Important
- Do NOT modify the auth middleware without discussing first
- Do NOT add new dependencies to the shared package
- Do NOT use `console.log` — use the Logger service
```
