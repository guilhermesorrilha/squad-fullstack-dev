---
task: "Security Audit"
order: 1
input: |
  - frontend_output: Código frontend implementado
  - backend_output: Código backend implementado
output: |
  - security_report: Relatório de segurança com findings e veredicto
---

# Security Audit

Executa auditoria de segurança baseada no OWASP Top 10. Verifica cada item contra o código implementado e produz relatório com findings categorizados por severidade.

## Process

1. Mapear attack surface do projeto (endpoints públicos, autenticação, dados sensíveis)
2. Verificar A01 — Broken Access Control (roles, permissões, IDOR)
3. Verificar A02 — Cryptographic Failures (dados sensíveis, hashing, TLS)
4. Verificar A03 — Injection (SQL, NoSQL, command, XSS)
5. Verificar A04 — Insecure Design (threat model, business logic flaws)
6. Verificar A05 — Security Misconfiguration (headers, CORS, error messages)
7. Verificar A06 — Vulnerable Components (dependências desatualizadas)
8. Verificar A07 — Auth Failures (senhas, sessões, MFA)
9. Verificar A08 — Data Integrity (supply chain, deserialization)
10. Verificar A09 — Logging Failures (eventos de segurança não logados)
11. Verificar A10 — SSRF (server-side request forgery)
12. Verificar headers de segurança (CSP, HSTS, X-Frame-Options, X-Content-Type-Options)
13. Scan por secrets hardcoded no código
14. Compilar relatório com findings, severidade e remediação

## Output Format

```markdown
# Security Audit Report

## Resumo
- **OWASP Top 10 verificados:** {N}/10
- **Findings:** {N} ({N} critical, {N} high, {N} medium, {N} low)
- **Veredicto:** {PASS | CONDITIONAL PASS | FAIL}

## Attack Surface
- {endpoints, auth, dados sensíveis}

## OWASP Checklist
| # | Categoria | Status | Findings |
|---|-----------|--------|----------|
| A01 | Broken Access Control | PASS/FAIL | ... |
...

## Findings
### SEC-{N} [{SEVERITY}] — {OWASP Category}
**Descrição:** ...
**Impacto:** ...
**Evidência:** ...
**Remediação:** ...

## Headers de Segurança
| Header | Status | Valor |
|--------|--------|-------|
| CSP | PASS/MISSING | ... |
...

## Veredicto
{PASS | CONDITIONAL PASS | FAIL} — {justificativa}
```

## Output Example

> Use as quality reference, not as rigid template.

```markdown
# Security Audit Report: Auth System

## Resumo
- **OWASP Top 10 verificados:** 10/10
- **Findings:** 3 (0 critical, 1 high, 1 medium, 1 low)
- **Veredicto:** CONDITIONAL PASS — 1 finding high deve ser corrigida

## OWASP Checklist
| # | Categoria | Status | Findings |
|---|-----------|--------|----------|
| A01 | Broken Access Control | PASS | Roles implementados corretamente |
| A02 | Cryptographic Failures | PASS | Passwords com bcrypt, TLS ativo |
| A03 | Injection | FAIL | SEC-001: SQL injection no search |
| A04 | Insecure Design | PASS | Threat model adequado |
| A05 | Security Misconfiguration | FAIL | SEC-002: headers ausentes |
| A06 | Vulnerable Components | PASS | Deps atualizadas |
| A07 | Auth Failures | PASS | OAuth2 implementado corretamente |
| A08 | Data Integrity | PASS | JWT com RS256, deps verificadas |
| A09 | Logging Failures | FAIL | SEC-003: login failures não logados |
| A10 | SSRF | PASS | Sem fetch externo user-controlled |

## Findings

### SEC-001 [HIGH] — A03 Injection
**Descrição:** POST /api/search interpola input do usuário diretamente na query SQL.
**Impacto:** SQL injection permite leitura arbitrária de dados do banco.
**Evidência:** Payload `' OR 1=1 --` retorna todos os registros.
**Remediação:** Usar prepared statements / parameterized queries. Substituir string concatenation por query builder com placeholders.

### SEC-002 [MEDIUM] — A05 Security Misconfiguration
**Descrição:** Headers de segurança ausentes nas respostas HTTP.
**Impacto:** XSS e clickjacking facilitados sem CSP e X-Frame-Options.
**Evidência:** Response headers não incluem CSP, HSTS, X-Content-Type-Options.
**Remediação:** Adicionar middleware de headers: CSP com nonces, HSTS max-age=31536000, X-Frame-Options: DENY, X-Content-Type-Options: nosniff.

### SEC-003 [LOW] — A09 Logging Failures
**Descrição:** Tentativas de login falhas não são registradas.
**Impacto:** Brute force attacks não são detectáveis.
**Evidência:** Nenhum log gerado ao submeter credenciais inválidas 10x.
**Remediação:** Logar IP, timestamp, user agent e username de tentativas falhas.

## Veredicto
CONDITIONAL PASS — SEC-001 (high) deve ser corrigida antes do deploy. SEC-002 e SEC-003 recomendados mas não bloqueantes.
```

## Quality Criteria

- [ ] Todos os 10 itens do OWASP Top 10 verificados
- [ ] Cada finding com severidade (critical/high/medium/low)
- [ ] Remediação documentada para cada finding
- [ ] Headers de segurança verificados
- [ ] Secrets scan realizado (nenhuma credencial hardcoded)

## Veto Conditions

Reject and redo if ANY are true:
1. Menos de 10 itens do OWASP verificados (algum item ignorado)
2. Findings sem remediação documentada
