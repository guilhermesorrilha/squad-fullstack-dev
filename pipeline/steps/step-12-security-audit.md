---
execution: subagent
agent: security-reviewer
model_tier: powerful
inputFile: squads/fullstack-dev/output/frontend-output.md
outputFile: squads/fullstack-dev/output/security-report.md
---

# Step 12: Security Audit

## Context Loading

Load these files before executing:
- `squads/fullstack-dev/output/frontend-output.md` — código frontend
- `squads/fullstack-dev/output/backend-output.md` — código backend
- `squads/fullstack-dev/pipeline/data/research-brief.md` — OWASP Top 10 reference
- `squads/fullstack-dev/pipeline/data/quality-criteria.md` — critérios de segurança

## Instructions

### Process
1. Mapear attack surface do projeto (endpoints, auth, dados sensíveis)
2. Verificar cada item do OWASP Top 10 contra o código implementado
3. Verificar headers de segurança (CSP, HSTS, X-Frame-Options)
4. Scan por secrets hardcoded no código
5. Executar task `security-audit` do Sérgio Segurança
6. Compilar relatório com findings categorizados por severidade

## Output Format

```markdown
# Security Audit Report

## Resumo
- OWASP verificados: {N}/10
- Findings: {N} ({severidades})
- Veredicto: {PASS | CONDITIONAL PASS | FAIL}

## OWASP Checklist
{tabela com status de cada item}

## Findings
### SEC-{N} [{SEVERITY}] — {OWASP}
Descrição / Impacto / Evidência / Remediação

## Headers de Segurança
{tabela com status}

## Veredicto
```

## Output Example

```markdown
# Security Audit: Auth System
## Resumo
- OWASP: 10/10 verificados
- Findings: 2 (1 high, 1 medium)
- Veredicto: CONDITIONAL PASS

## Findings
### SEC-001 [HIGH] — A03 Injection
SQL injection no /api/search. Usar prepared statements.
```

## Veto Conditions

Reject and redo if ANY of these are true:
1. Menos de 10 itens OWASP verificados
2. Findings sem remediação documentada

## Quality Criteria

- [ ] Todos os 10 itens OWASP verificados
- [ ] Findings com severidade e remediação
- [ ] Headers de segurança verificados
- [ ] Secrets scan realizado
