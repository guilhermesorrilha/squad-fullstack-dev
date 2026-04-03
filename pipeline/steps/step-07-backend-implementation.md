---
execution: subagent
agent: backend-dev
model_tier: powerful
inputFile: squads/fullstack-dev/output/project-plan.md
outputFile: squads/fullstack-dev/output/backend-output.md
---

# Step 07: Backend Implementation

## Context Loading

Load these files before executing:
- `squads/fullstack-dev/output/project-plan.md` — plano com contratos de API, user stories e requisitos
- `squads/fullstack-dev/pipeline/data/research-brief.md` — Backend best practices (REST, RFC 7807)
- `squads/fullstack-dev/pipeline/data/quality-criteria.md` — critérios de qualidade para Backend
- `_opensquad/_memory/company.md` — contexto da empresa

## Instructions

### Process
1. Analisar contratos de API do plano e definir schema de dados completo
2. Implementar modelos de dados e migrations do banco
3. Implementar endpoints REST com validação de input e erros RFC 7807
4. Implementar regras de negócio, autenticação e autorização
5. Escrever testes de integração (happy path + error paths)
6. Documentar contratos finais de API para o Tech Writer

## Output Format

O output MUST follow this exact structure:
```markdown
# Backend Implementation: {projeto}

## Schema de Dados
{definição de entidades, tabelas e relações}

## Endpoints Implementados
### {METHOD} {path}
- Request: {schema}
- Response 2xx: {schema}
- Response 4xx/5xx: {RFC 7807}
- Auth: {required/public}
- Validação: {regras}

## Código Completo
{código organizado por camada: models, repositories, services, controllers}

## Testes
{testes de integração}
```

## Output Example

```markdown
# Backend: Auth System

## Schema
CREATE TABLE users (
  id UUID PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  name VARCHAR(255) NOT NULL,
  provider VARCHAR(50) NOT NULL
);

## Endpoints
### POST /api/auth/google
- Request: { code, redirect_uri }
- Response 200: { access_token, refresh_token, user }
- Response 401: { type, title, status: 401, detail }
```

## Veto Conditions

Reject and redo if ANY of these are true:
1. Endpoints retornando HTTP 200 para erros (silent failures)
2. Input não validado no servidor

## Quality Criteria

- [ ] Todos os endpoints com status codes corretos
- [ ] Erros seguem RFC 7807
- [ ] Input validado no servidor
- [ ] Testes de integração cobrindo happy path e error paths
