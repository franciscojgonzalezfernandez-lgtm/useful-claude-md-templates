# Contributing

Thanks for your interest in contributing to claude-md-templates!

## How to Contribute

### Improving existing templates
1. Fork the repo
2. Edit the template you want to improve
3. Submit a PR with a clear description of what you changed and why

### Adding a new template
1. Create a new directory under `templates/` (e.g., `templates/django-backend/`)
2. Add a `CLAUDE.md` with production-ready content
3. Add a `README.md` explaining when to use this template
4. Update the root `README.md` comparison table
5. Submit a PR

### Template quality checklist
- [ ] Covers all essential sections (overview, stack, structure, commands, conventions)
- [ ] Uses specific technologies, not generic placeholders (except `[Project name]`)
- [ ] Includes architecture and testing guidelines
- [ ] Under 200 lines (CLAUDE.md best practice)
- [ ] Tested with Claude Code on a real or sample project

## Guidelines
- Keep templates practical — based on real project experience
- Avoid framework defaults that the AI already knows
- Include "what NOT to do" alongside "what to do"
- No sensitive data, even as examples
