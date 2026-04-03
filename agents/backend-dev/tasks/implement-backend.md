---
task: "Implement Backend"
order: 1
input: |
  - project_plan: Plano com contratos de API, user stories e requisitos
output: |
  - backend_code: Código backend implementado (APIs, models, services)
  - api_contracts: Contratos de API finais documentados
---

# Implement Backend

Implementa APIs, regras de negócio, modelos de dados e integrações conforme o plano do Orchestrator. Segue contratos de API definidos e padrões de erro RFC 7807.

## Process

1. Analisar contratos de API do plano e definir schema de dados
2. Modelar entidades e criar migrations do banco de dados
3. Implementar Repository layer para acesso a dados
4. Implementar Service layer com regras de negócio
5. Implementar Controllers/Handlers com endpoints REST
6. Adicionar validação de input em todos os endpoints
7. Implementar tratamento de erros seguindo RFC 7807
8. Implementar autenticação e autorização conforme requisitos
9. Escrever testes de integração para happy path e error paths

## Output Format

```markdown
# Backend Implementation

## Schema de Dados
{definição de entidades e relações}

## Endpoints Implementados
### {METHOD} {path}
- **Request:** {schema}
- **Response 2xx:** {schema}
- **Response 4xx/5xx:** {RFC 7807 schema}
- **Auth:** {required/public}
- **Validação:** {regras}

## Código Completo
{todo o código organizado por camada: models, repositories, services, controllers}

## Testes
{testes de integração}
```

## Output Example

> Use as quality reference, not as rigid template.

```markdown
# Backend Implementation: Auth Service

## Schema de Dados

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  name VARCHAR(255) NOT NULL,
  avatar_url TEXT,
  provider VARCHAR(50) NOT NULL,
  provider_id VARCHAR(255) NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(provider, provider_id)
);

CREATE TABLE sessions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  refresh_token VARCHAR(512) UNIQUE NOT NULL,
  expires_at TIMESTAMP NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);
```

## Endpoints Implementados

### POST /api/auth/google
- **Request:** `{ code: string, redirect_uri: string }`
- **Response 200:** `{ access_token: string, refresh_token: string, user: { id, name, email, avatar_url } }`
- **Response 401:** `{ type: "https://api.example.com/errors/oauth-failed", title: "OAuth Failed", status: 401, detail: "Google token exchange failed: invalid_grant" }`
- **Auth:** public
- **Validação:** code required, non-empty; redirect_uri required, valid URL

### GET /api/dashboard/metrics
- **Request:** Headers `Authorization: Bearer {access_token}`
- **Response 200:** `{ projects_count: number, last_activity: string, storage_used_mb: number }`
- **Response 401:** `{ type: "https://api.example.com/errors/unauthorized", title: "Unauthorized", status: 401, detail: "Access token expired or invalid" }`
- **Auth:** required (Bearer token)
- **Validação:** n/a (authenticated user only)
```

## Quality Criteria

- [ ] Todos os endpoints retornam status codes HTTP corretos
- [ ] Erros seguem RFC 7807 (type, title, status, detail)
- [ ] Input validado no servidor para todos os endpoints
- [ ] Autenticação e autorização implementadas
- [ ] Testes de integração cobrindo happy path e error paths
- [ ] Queries com índices adequados

## Veto Conditions

Reject and redo if ANY are true:
1. Endpoints retornando HTTP 200 para erros (silent failures)
2. Input não validado no servidor (confiando em validação client-side)
