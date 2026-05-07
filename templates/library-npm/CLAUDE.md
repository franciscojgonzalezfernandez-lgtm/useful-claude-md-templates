# CLAUDE.md — npm Library / Package

## Project overview
[Package name] is a [brief description]. Published to npm as `[package-name]`.

## Tech stack
- **Language:** TypeScript (strict mode)
- **Build:** tsup (ESM + CJS dual output)
- **Testing:** Vitest
- **Linting:** ESLint + Prettier
- **Docs:** TypeDoc (API reference) + README examples
- **CI/CD:** GitHub Actions (test → build → publish)
- **Package manager:** pnpm

## Project structure
```
├── src/
│   ├── index.ts          # Public API — all exports go through here
│   ├── core/             # Core logic
│   ├── utils/            # Internal utilities
│   └── types.ts          # Public type definitions
├── tests/
│   ├── unit/             # Unit tests
│   └── integration/      # Integration tests
├── examples/             # Usage examples
├── tsconfig.json
├── tsup.config.ts        # Build config
├── vitest.config.ts
├── package.json
├── CHANGELOG.md
└── README.md
```

## Development commands
```bash
pnpm dev              # Watch mode (rebuild on change)
pnpm build            # Production build (ESM + CJS)
pnpm test             # Run tests
pnpm test:watch       # Watch mode tests
pnpm test:cov         # Coverage report
pnpm lint             # Lint
pnpm typecheck        # Type check without emitting
pnpm docs             # Generate API docs
pnpm changeset        # Create changeset for versioning
pnpm release          # Build + publish to npm
```

## Code style and conventions
- Export only what users need — keep internals private
- `src/index.ts` is the single entry point — every public export goes through it
- Internal modules: prefix with underscore or keep unexported
- Pure functions preferred — no side effects in core logic
- No runtime dependencies unless absolutely necessary (keep install size small)
- Use generics for flexible APIs, but provide sensible defaults

## API design principles
- Minimal API surface — fewer exports = easier to maintain
- Options objects over long parameter lists: `createThing({ name, type })` not `createThing(name, type)`
- Return types: be explicit, don't rely on inference for public APIs
- Error handling: throw typed errors with descriptive messages
- Document every public function with JSDoc (feeds into TypeDoc)
- Deprecation: use `@deprecated` JSDoc tag before removing

## Package.json essentials
```json
{
  "type": "module",
  "main": "./dist/index.cjs",
  "module": "./dist/index.js",
  "types": "./dist/index.d.ts",
  "exports": {
    ".": {
      "import": "./dist/index.js",
      "require": "./dist/index.cjs",
      "types": "./dist/index.d.ts"
    }
  },
  "files": ["dist"],
  "sideEffects": false
}
```

## Testing
- Test public API only — refactoring internals should not break tests
- Edge cases: empty input, null/undefined, large datasets, concurrent usage
- Snapshot tests for serializable output (use sparingly)
- Benchmark critical paths with `vitest.bench`
- Minimum 90% coverage on public API

## Publishing checklist
- [ ] All tests pass
- [ ] Build succeeds (both ESM and CJS)
- [ ] Types are correct (`pnpm typecheck`)
- [ ] CHANGELOG.md updated
- [ ] Version bumped (semver: breaking = major, feature = minor, fix = patch)
- [ ] README examples are accurate
- [ ] `npm pack` and inspect contents — no junk files
