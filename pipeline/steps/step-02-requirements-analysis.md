---
execution: inline
agent: orchestrator
inputFile: squads/fullstack-dev/output/project-briefing.md
outputFile: squads/fullstack-dev/output/project-plan.md
---

# Step 02: Requirements Analysis & Planning

## Context Loading

Load these files before executing:
- `squads/fullstack-dev/output/project-briefing.md` — briefing do projeto descrito pelo usuário
- `squads/fullstack-dev/pipeline/data/research-brief.md` — frameworks e metodologias de referência
- `squads/fullstack-dev/pipeline/data/domain-framework.md` — metodologia operacional do squad
- `squads/fullstack-dev/pipeline/data/quality-criteria.md` — critérios de qualidade por fase
- `_opensquad/_memory/company.md` — contexto da empresa

## Instructions

### Process
1. Ler o briefing do projeto e identificar todos os requisitos explícitos e implícitos
2. Executar a task `analyze-requirements` do Oscar Orquestra: classificar requisitos, mapear dependências, identificar riscos
3. Executar a task `create-plan` do Oscar Orquestra: criar user stories com critérios de aceite, definir contratos de API, estabelecer definition of done
4. Compilar o plano completo em um único documento estruturado
5. Apresentar o plano para aprovação no próximo checkpoint

## Output Format

O output MUST follow this exact structure:
```markdown
# Plano de Projeto: {nome}

## Requisitos
### Funcionais
- REQ-{N}: {descrição} (P0/P1/P2)
### Não-Funcionais
- NFR-{N}: {descrição}

## User Stories
### US-{N}: {título} ({prioridade})
**Como** {persona}, **quero** {ação}, **para** {benefício}.
**Critérios de aceite:** ...
**Responsável:** {agente}

## Contratos de API
### {METHOD} {path}
- Request: ...
- Response: ...
- Errors: ...

## Dependências
{mapa de dependências entre agentes}

## Riscos
{riscos com mitigação}

## Definition of Done
{checklist global}
```

## Output Example

```markdown
# Plano de Projeto: Sistema de Autenticação OAuth2

## Requisitos
### Funcionais
- REQ-001: Login com Google OAuth2 (P0)
- REQ-002: Login com GitHub OAuth2 (P0)
- REQ-003: Dashboard com métricas do usuário (P1)
- REQ-004: Gerenciamento de sessão com refresh token (P0)

### Não-Funcionais
- NFR-001: LCP < 2.5s em todas as páginas
- NFR-002: WCAG 2.1 AA em todos os componentes interativos
- NFR-003: OWASP Top 10 compliance
- NFR-004: Responsivo em mobile, tablet e desktop

## User Stories

### US-01: Login com Google (P0)
**Como** usuário, **quero** fazer login com minha conta Google, **para** acessar o sistema sem criar nova conta.
**Critérios de aceite:**
- Botão "Login com Google" visível na tela de login
- Redirect correto após autorização
- Sessão persiste por 7 dias
- Error handling para falhas de OAuth
**Responsável:** Frontend (UI) + Backend (OAuth flow)
**Dependências:** Backend configura Google OAuth credentials primeiro

## Contratos de API

### POST /api/auth/google
- Request: `{ code: string, redirect_uri: string }`
- Response 200: `{ access_token, refresh_token, user: { id, name, email, avatar } }`
- Response 401: RFC 7807 `{ type, title, status: 401, detail }`

## Definition of Done
- [ ] Testes passando
- [ ] Integração Frontend-Backend funcional
- [ ] Responsivo em 3 breakpoints
- [ ] Acessível via teclado
- [ ] Documentação de API atualizada
```

## Veto Conditions

Reject and redo if ANY of these are true:
1. Requisitos do briefing foram ignorados ou interpretados incorretamente
2. User stories sem critérios de aceite específicos

## Quality Criteria

- [ ] Plano cobre 100% dos requisitos do briefing
- [ ] Cada user story tem critérios de aceite
- [ ] Contratos de API entre Frontend e Backend documentados
- [ ] Dependências mapeadas
- [ ] Definition of done clara
