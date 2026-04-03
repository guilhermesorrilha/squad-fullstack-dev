---
task: "Create Plan"
order: 2
input: |
  - requirements: Lista de requisitos analisados na task anterior
  - dependencies: Mapa de dependências
  - risks: Riscos identificados
output: |
  - project_plan: Plano de tarefas com responsáveis, prioridades e DoD
---

# Create Plan

Cria o plano de execução detalhado com user stories, tarefas atribuídas a cada agente, prioridades, critérios de aceite e definition of done.

## Process

1. Converter cada requisito funcional em user stories no formato "Como X, quero Y, para Z"
2. Decompor user stories em tarefas atribuídas a agentes específicos (Frontend, Backend, etc.)
3. Definir prioridades (P0 = crítico, P1 = importante, P2 = nice-to-have)
4. Definir definition of done global e por fase
5. Estabelecer WIP limits por agente
6. Documentar contratos de API entre Frontend e Backend

## Output Format

```markdown
# Plano de Projeto: {nome}

## User Stories
### US-{N}: {título} ({prioridade})
**Como** {persona}, **quero** {ação}, **para** {benefício}.
**Critérios de aceite:**
- ...
**Responsável:** {agente}
**Dependências:** {lista}

## Contratos de API
### {endpoint}
- Method: {GET/POST/PUT/DELETE}
- Request: {schema}
- Response: {schema}
- Errors: {lista}

## Definition of Done
- [ ] ...

## WIP Limits
| Agente | WIP Max |
|--------|---------|
| ...    | ...     |
```

## Output Example

> Use as quality reference, not as rigid template.

```markdown
# Plano de Projeto: Sistema de Autenticação OAuth2

## User Stories

### US-01: Login com Google (P0)
**Como** usuário, **quero** fazer login com minha conta Google, **para** acessar o sistema sem criar nova conta.
**Critérios de aceite:**
- Botão "Login com Google" visível na tela de login
- Redirect para Google OAuth consent screen
- Após autorização, redireciona para dashboard
- Sessão persiste por 7 dias com refresh token
- Error handling para OAuth falhas (timeout, denied, revoked)
**Responsável:** Frontend (UI) + Backend (OAuth flow)
**Dependências:** Backend configura Google OAuth credentials antes

### US-02: Dashboard de Métricas (P1)
**Como** usuário logado, **quero** ver minhas métricas na dashboard, **para** acompanhar meu uso.
**Critérios de aceite:**
- Exibe total de projetos, última atividade, uso de storage
- Loading skeleton enquanto dados carregam
- Empty state para usuários novos
- Responsivo em mobile, tablet, desktop
**Responsável:** Frontend (UI) + Backend (API)
**Dependências:** API de métricas definida no contrato

## Contratos de API

### POST /api/auth/google
- Request: `{ code: string, redirect_uri: string }`
- Response 200: `{ access_token: string, refresh_token: string, user: { id, name, email, avatar } }`
- Response 401: `{ type: "auth_error", title: "OAuth Failed", status: 401, detail: "..." }`

### GET /api/dashboard/metrics
- Request: Headers `Authorization: Bearer {token}`
- Response 200: `{ projects_count: number, last_activity: ISO8601, storage_used_mb: number }`
- Response 401: `{ type: "auth_error", title: "Unauthorized", status: 401, detail: "..." }`

## Definition of Done
- [ ] Testes unitários passando
- [ ] Integração Frontend-Backend funcional
- [ ] Documentação de API atualizada
- [ ] Code review aprovado
- [ ] Responsivo em 3 breakpoints
- [ ] Acessível via teclado

## WIP Limits
| Agente | WIP Max |
|--------|---------|
| Fábio Front | 2 user stories |
| Bernardo Backend | 2 user stories |
| Quico Qualidade | 1 feature em teste |
```

## Quality Criteria

- [ ] Cada user story no formato "Como X, quero Y, para Z"
- [ ] Todas as user stories têm critérios de aceite específicos
- [ ] Contratos de API entre Frontend e Backend documentados
- [ ] Definition of done clara e verificável
- [ ] WIP limits definidos por agente

## Veto Conditions

Reject and redo if ANY are true:
1. User stories sem critérios de aceite
2. Contratos de API entre Frontend e Backend não documentados
