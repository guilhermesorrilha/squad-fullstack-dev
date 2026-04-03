---
execution: inline
agent: qa-tester
inputFile: squads/fullstack-dev/output/frontend-output.md
outputFile: squads/fullstack-dev/output/qa-report.md
---

# Step 10: QA Testing

## Context Loading

Load these files before executing:
- `squads/fullstack-dev/output/frontend-output.md` — implementação do Frontend
- `squads/fullstack-dev/output/backend-output.md` — implementação do Backend
- `squads/fullstack-dev/output/project-plan.md` — plano com critérios de aceite
- `squads/fullstack-dev/pipeline/data/quality-criteria.md` — critérios de qualidade para QA

## Instructions

### Process
1. Ler critérios de aceite de cada user story no plano
2. Para cada critério, criar cenário de teste (happy path + edge cases)
3. Analisar código do Frontend e Backend para verificar implementação
4. Testar integração entre Frontend e Backend (contratos de API)
5. Testar error handling e edge cases (inputs inválidos, timeouts, empty states)
6. Executar task `run-tests` do Quico Qualidade
7. Emitir veredicto PASS ou FAIL

## Output Format

```markdown
# QA Report: {projeto}

## Resumo
- Features testadas: {N}/{N}
- Critérios verificados: {N}/{N}
- Bugs: {N} ({N} critical, {N} major, {N} minor)
- Veredicto: {PASS | FAIL}

## Testes Executados
### {Feature}
| Cenário | Resultado | Notas |
|---------|-----------|-------|

## Bugs
### BUG-{N} [{SEVERITY}]
Steps to reproduce / Expected / Actual / Environment

## Veredicto
{PASS | FAIL} — {justificativa}
```

## Output Example

```markdown
# QA Report: Auth System
## Resumo
- Features testadas: 3/3
- Critérios verificados: 12/15
- Bugs: 2 (1 critical, 1 minor)
- Veredicto: FAIL — 1 critical bug

## Bugs
### BUG-001 [CRITICAL]
Feature: Login com Google
Steps: Clicar login → Autorizar → Observar redirect
Expected: Redirect para /dashboard
Actual: Erro 500 no redirect
```

## Veto Conditions

Reject and redo if ANY of these are true:
1. Critérios de aceite não foram todos verificados
2. Bugs sem steps to reproduce

## Quality Criteria

- [ ] 100% dos critérios de aceite verificados
- [ ] Bugs com steps to reproduce completos
- [ ] Edge cases testados
- [ ] Integração Frontend-Backend validada
