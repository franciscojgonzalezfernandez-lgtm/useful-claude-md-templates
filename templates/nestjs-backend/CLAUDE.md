# CLAUDE.md — NestJS Backend

## Project overview
[Project name] is a [brief description]. Built with NestJS, TypeScript, and PostgreSQL.

## Tech stack
- **Framework:** NestJS 10+
- **Language:** TypeScript (strict mode)
- **Database:** PostgreSQL + TypeORM / Prisma
- **Auth:** Passport.js (JWT strategy)
- **Validation:** class-validator + class-transformer
- **Docs:** Swagger (auto-generated via decorators)
- **Queue:** BullMQ + Redis
- **Testing:** Jest + Supertest (e2e)
- **Containerization:** Docker + Docker Compose

## Architecture
Clean Architecture with 3 layers:

```
src/
├── modules/              # Feature modules
│   ├── users/
│   │   ├── domain/       # Entities, value objects, repository interfaces
│   │   ├── application/  # Use cases (services), DTOs, ports
│   │   ├── infrastructure/ # TypeORM repos, external API clients
│   │   └── presentation/ # Controllers, guards, decorators
│   ├── auth/
│   └── [feature]/
├── common/               # Shared code
│   ├── decorators/       # Custom decorators
│   ├── filters/          # Exception filters
│   ├── guards/           # Auth guards
│   ├── interceptors/     # Logging, transform interceptors
│   ├── pipes/            # Validation pipes
│   └── interfaces/       # Shared interfaces
├── config/               # Configuration module (env validation)
├── database/             # Migrations, seeds
├── app.module.ts
└── main.ts
```

## Dependency rule
Dependencies point inward: `presentation → application → domain`. Domain layer has zero imports from other layers.

## Development commands
```bash
npm run start:dev       # Start with hot reload
npm run build           # Compile TypeScript
npm run start:prod      # Run compiled code
npm run lint            # ESLint
npm run test            # Unit tests
npm run test:e2e        # End-to-end tests
npm run test:cov        # Coverage report
npm run migration:gen   # Generate migration
npm run migration:run   # Run migrations
npm run seed            # Seed database
```

## Code style and conventions
- One module per feature — never put unrelated logic in the same module
- Controllers: thin — delegate to services immediately, no business logic
- Services (use cases): one public method per use case, descriptive names (`createUser`, `findOrderById`)
- Entities: rich domain models with behavior, not anemic data bags
- DTOs: separate Create/Update/Response DTOs — never expose entities directly
- Use `readonly` properties on DTOs
- Naming: `*.controller.ts`, `*.service.ts`, `*.entity.ts`, `*.repository.ts`, `*.dto.ts`, `*.guard.ts`

## Error handling
- Use NestJS built-in exceptions (`NotFoundException`, `ForbiddenException`, etc.)
- Create custom domain exceptions extending `HttpException` for business errors
- Global exception filter catches and formats all errors consistently
- Never throw raw `Error` — always use typed exceptions

## Database patterns
- Repository pattern: inject repository interfaces, not TypeORM/Prisma directly
- Transactions: use `DataSource.transaction()` for multi-entity operations
- Pagination: return `{ data, total, page, limit }` format
- Soft deletes: use `deletedAt` column, filter in repository
- Indexes: add for all frequently queried columns

## Testing guidelines
- Unit tests: mock repositories and external services
- E2e tests: use test database, run migrations before suite
- Test file location: co-located with source (`*.spec.ts`)
- Name tests descriptively: `describe('UserService')` → `it('should throw NotFoundException when user does not exist')`
- Cover edge cases: invalid input, missing records, duplicate entries, unauthorized access

## API conventions
- RESTful routes: `GET /users`, `POST /users`, `GET /users/:id`, `PATCH /users/:id`, `DELETE /users/:id`
- Versioning: URI-based (`/api/v1/`)
- Response envelope: `{ data, meta }` for lists, raw object for single items
- Swagger decorators on every endpoint: `@ApiOperation`, `@ApiResponse`, `@ApiTags`
- Rate limiting on auth endpoints

## Security
- Validate all inputs with class-validator (whitelist: true, forbidNonWhitelisted: true)
- Hash passwords with bcrypt (10+ rounds)
- JWT tokens: short-lived access (15m) + long-lived refresh (7d)
- Helmet middleware enabled
- CORS: explicit origin whitelist, no wildcards in production
- Environment variables validated at startup with Joi/Zod
