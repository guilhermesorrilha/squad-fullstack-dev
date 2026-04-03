---
task: "Write Changelog"
order: 2
input: |
  - project_plan: Plano com features implementadas
  - all_outputs: Outputs de todos os agentes
output: |
  - changelog: Changelog seguindo Keep a Changelog format
---

# Write Changelog

Gera changelog da entrega seguindo o padrão Keep a Changelog. Categoriza mudanças em Added, Changed, Fixed, Security.

## Process

1. Ler plano do projeto para identificar features implementadas
2. Ler outputs de todos os agentes para compilar mudanças
3. Categorizar mudanças: Added (novas features), Changed (alterações), Fixed (correções), Security (fixes de segurança)
4. Escrever em formato Keep a Changelog com data e versão
5. Incluir breaking changes em destaque se houver

## Output Format

```markdown
# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

## [{version}] - {YYYY-MM-DD}

### Added
- {nova feature com descrição concisa}

### Changed
- {alteração com contexto}

### Fixed
- {correção com referência ao bug}

### Security
- {fix de segurança com referência ao finding}
```

## Output Example

> Use as quality reference, not as rigid template.

```markdown
# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

## [1.0.0] - 2026-04-02

### Added
- OAuth2 authentication with Google and GitHub providers
- User dashboard with project metrics (total projects, last activity, storage used)
- Session management with JWT access tokens and refresh tokens (7-day expiry)
- Error handling for OAuth failures (timeout, denied, revoked)
- Empty state for new users with onboarding tooltip
- Responsive layout for mobile (375px), tablet (768px), and desktop (1280px)
- Skeleton loading states for all data-dependent components
- API documentation (OpenAPI 3.1) with executable curl examples

### Security
- SQL injection fix in /api/search endpoint (parameterized queries)
- Added security headers: CSP, HSTS, X-Frame-Options, X-Content-Type-Options
- Failed login attempts now logged with IP, timestamp, and user agent
- All secrets moved to environment variables (zero hardcoded credentials)

### Fixed
- CLS issue from unsized avatar images in dashboard (added explicit dimensions)
- Keyboard navigation on project dropdown (now uses native select with ARIA fallback)
- Focus visibility on footer links (replaced outline:none with custom focus style)
- Placeholder contrast ratio improved from 2.85:1 to 4.54:1
```

## Quality Criteria

- [ ] Segue formato Keep a Changelog
- [ ] Todas as features implementadas listadas em Added
- [ ] Fixes de segurança listados em Security
- [ ] Cada entry é concisa e descritiva

## Veto Conditions

Reject and redo if ANY are true:
1. Features implementadas ausentes do changelog
2. Fixes de segurança não categorizados em Security
