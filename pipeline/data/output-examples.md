# Output Examples — Fullstack Dev Squad

## Exemplo 1: Plano de Projeto (Orchestrator)

```markdown
# Plano de Projeto: Sistema de Autenticação OAuth2

## Escopo
Implementar autenticação OAuth2 com Google e GitHub, incluindo login, registro, recuperação de senha e gerenciamento de sessão.

## User Stories

### US-01: Login com Google (P0)
**Como** usuário, **quero** fazer login com minha conta Google **para** acessar o sistema sem criar nova conta.
**Critérios de aceite:**
- Botão "Login com Google" visível na tela de login
- Redirect para Google OAuth consent screen
- Após autorização, redireciona para dashboard
- Sessão persiste por 7 dias
- Error handling para OAuth falhas
**Responsável:** Frontend (UI) + Backend (OAuth flow)
**Dependências:** Backend precisa configurar Google OAuth credentials antes

### US-02: Login com GitHub (P0)
...

### US-03: Recuperação de Senha (P1)
...

## Dependências
- Backend configura OAuth credentials → Frontend implementa botões
- Backend implementa endpoints de sessão → Frontend integra

## Riscos
1. Rate limiting do Google OAuth em ambiente de dev → mitigação: usar mock em testes
2. Tokens de refresh com expiração inconsistente → mitigação: implementar refresh preemptivo

## Definition of Done
- [ ] Testes unitários passando
- [ ] Integração Frontend-Backend funcional
- [ ] Documentação de API atualizada
- [ ] Code review aprovado
```

## Exemplo 2: Relatório de QA (QA Tester)

```markdown
# Relatório de QA: Sistema de Autenticação

## Resumo
- **Features testadas:** 3/3
- **Critérios de aceite verificados:** 12/15
- **Bugs encontrados:** 4 (1 critical, 1 major, 2 minor)
- **Veredicto:** FAIL — 1 bug critical bloqueia aprovação

## Bugs

### BUG-001 [CRITICAL]
**Feature:** Login com Google
**Steps to reproduce:**
1. Clicar em "Login com Google"
2. Autorizar no Google OAuth
3. Observar redirect
**Expected:** Redirect para /dashboard com sessão ativa
**Actual:** Redirect para /login com erro 500
**Environment:** Chrome 120, staging
**Root cause provável:** Token exchange endpoint retornando erro

### BUG-002 [MAJOR]
**Feature:** Recuperação de Senha
**Steps to reproduce:**
1. Clicar em "Esqueci minha senha"
2. Inserir email válido
3. Aguardar email
**Expected:** Email recebido em até 2 minutos
**Actual:** Email nunca chega (verificado em spam)
**Environment:** Gmail, staging

### BUG-003 [MINOR]
**Feature:** Login com GitHub
**Steps to reproduce:**
1. Fazer login com GitHub
2. Observar avatar no header
**Expected:** Avatar do GitHub exibido
**Actual:** Avatar placeholder genérico
**Environment:** Todos os browsers

### BUG-004 [MINOR]
**Feature:** Sessão
**Descrição:** Tooltip de "Logout" não aparece em mobile
**Environment:** Safari iOS 17

## Veredicto: FAIL
**Bloqueios:** BUG-001 (critical) deve ser resolvido antes de prosseguir.
**Recomendação:** Corrigir BUG-001 e BUG-002, resubmeter para QA round 2.
```

## Exemplo 3: Security Audit Report (Security Reviewer)

```markdown
# Security Audit Report

## Resumo
- **OWASP Top 10 verificados:** 10/10
- **Vulnerabilidades encontradas:** 3 (0 critical, 1 high, 1 medium, 1 low)
- **Veredicto:** CONDITIONAL PASS — 1 high deve ser corrigida antes do deploy

## Findings

### SEC-001 [HIGH] — A03 Injection
**Descrição:** Endpoint POST /api/search aceita input sem sanitização. Query parameter `q` é interpolado diretamente na query SQL.
**Impacto:** SQL injection permite leitura de dados arbitrários do banco.
**Evidência:** Payload `' OR 1=1 --` retorna todos os registros.
**Remediação:** Usar prepared statements / parameterized queries.
**Referência:** OWASP A03:2021

### SEC-002 [MEDIUM] — A05 Security Misconfiguration
**Descrição:** Headers de segurança ausentes na resposta HTTP.
**Missing:** Content-Security-Policy, X-Content-Type-Options, Strict-Transport-Security
**Remediação:** Configurar headers no reverse proxy/middleware.

### SEC-003 [LOW] — A09 Logging Failures
**Descrição:** Tentativas de login falhas não são logadas.
**Impacto:** Impossível detectar brute force attacks.
**Remediação:** Logar IP, timestamp e username de tentativas falhas.
```
