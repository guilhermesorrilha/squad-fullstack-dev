---
task: "Write API Docs"
order: 1
input: |
  - backend_output: Código backend com endpoints implementados
output: |
  - api_documentation: Documentação completa de API com exemplos executáveis
  - readme: README atualizado com setup e usage
---

# Write API Docs

Documenta todos os endpoints de API no padrão OpenAPI com exemplos executáveis (curl e SDK). Atualiza o README com instruções de setup, usage e arquitetura.

## Process

1. Ler output do Backend e extrair todos os endpoints implementados
2. Para cada endpoint, documentar: method, path, request, response, errors, auth
3. Incluir exemplos executáveis (curl) para cada endpoint
4. Documentar todos os status codes (2xx, 4xx, 5xx) com exemplos de response body
5. Gerar estrutura README: quickstart, setup, usage, architecture, contributing
6. Verificar que todos os exemplos são copiáveis e funcionais

## Output Format

```markdown
# API Documentation

## Base URL
`{base_url}`

## Authentication
{método de autenticação}

## Endpoints

### {METHOD} {path}
{descrição}

**Request:**
```json
{request body}
```

**Response 200:**
```json
{response body}
```

**Errors:**
| Status | Type | Description |
|--------|------|-------------|
| ...    | ...  | ...         |

**Example (curl):**
```bash
curl -X {METHOD} {url} ...
```

---

# README

## Quickstart
...

## Setup
...

## Architecture
...
```

## Output Example

> Use as quality reference, not as rigid template.

```markdown
# API Documentation: Auth Service

## Base URL
`https://api.example.com/v1`

## Authentication
Bearer token no header `Authorization`. Obtido via endpoint de login OAuth.

## Endpoints

### POST /api/auth/google
Inicia autenticação via Google OAuth. Troca o authorization code por tokens de acesso.

**Request:**
```json
{
  "code": "4/0AX4XfWh...",
  "redirect_uri": "https://app.example.com/callback"
}
```

**Response 200:**
```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIs...",
  "refresh_token": "dGhpcyBpcyBhIHJl...",
  "expires_in": 3600,
  "user": {
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "name": "Guilherme Silva",
    "email": "gui@example.com",
    "avatar_url": "https://lh3.googleusercontent.com/..."
  }
}
```

**Errors:**
| Status | Type | Description |
|--------|------|-------------|
| 400 | validation_error | code ou redirect_uri ausente/inválido |
| 401 | oauth_failed | Token exchange falhou (code expirado ou inválido) |
| 500 | internal_error | Erro interno no servidor |

**Example (curl):**
```bash
curl -X POST https://api.example.com/v1/api/auth/google \
  -H "Content-Type: application/json" \
  -d '{"code": "4/0AX4XfWh...", "redirect_uri": "https://app.example.com/callback"}'
```

---

# README

## Quickstart

```bash
git clone https://github.com/user/project.git
cd project
cp .env.example .env  # configure suas variáveis
npm install
npm run dev
```

Acesse `http://localhost:3000` no browser.

## Architecture

```
src/
├── controllers/    # HTTP handlers
├── services/       # Business logic
├── repositories/   # Data access
├── models/         # Entity definitions
├── middleware/      # Auth, validation, error handling
└── config/         # Environment and app config
```
```

## Quality Criteria

- [ ] 100% dos endpoints documentados com request/response
- [ ] Todos os status codes de resposta listados (2xx, 4xx, 5xx)
- [ ] Exemplos curl copiáveis para cada endpoint
- [ ] README com quickstart funcional

## Veto Conditions

Reject and redo if ANY are true:
1. Endpoints sem exemplos executáveis (curl ou SDK)
2. Status codes de erro (4xx/5xx) não documentados
