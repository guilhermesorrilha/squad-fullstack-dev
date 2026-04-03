---
execution: subagent
agent: tech-writer
model_tier: powerful
inputFile: squads/fullstack-dev/output/backend-output.md
outputFile: squads/fullstack-dev/output/documentation.md
---

# Step 16: Documentation

## Context Loading

Load these files before executing:
- `squads/fullstack-dev/output/backend-output.md` — implementação backend com endpoints
- `squads/fullstack-dev/output/frontend-output.md` — implementação frontend
- `squads/fullstack-dev/output/project-plan.md` — plano do projeto
- `squads/fullstack-dev/output/security-report.md` — findings de segurança corrigidos
- `squads/fullstack-dev/pipeline/data/research-brief.md` — Technical Writing best practices

## Instructions

### Process
1. Ler output do Backend e extrair todos os endpoints
2. Executar task `write-api-docs` do Tomás Texto: documentar cada endpoint com exemplos curl
3. Documentar todos os status codes (2xx, 4xx, 5xx)
4. Gerar README com quickstart, setup, architecture
5. Executar task `write-changelog` do Tomás Texto: compilar changelog com Added, Changed, Fixed, Security

## Output Format

```markdown
# Documentation: {projeto}

## API Documentation
{documentação completa de cada endpoint}

## README
{quickstart, setup, architecture}

## Changelog
{Keep a Changelog format}
```

## Output Example

```markdown
# Documentation: Auth System

## API
### POST /api/auth/google
{request, response, errors, curl example}

## README
## Quickstart
git clone... npm install... npm run dev

## Changelog
## [1.0.0] - 2026-04-02
### Added
- OAuth2 authentication with Google and GitHub
```

## Veto Conditions

Reject and redo if ANY of these are true:
1. Endpoints sem exemplos executáveis
2. Error codes não documentados

## Quality Criteria

- [ ] 100% endpoints documentados com exemplos
- [ ] Todos os status codes listados
- [ ] README com quickstart funcional
- [ ] Changelog em Keep a Changelog format
