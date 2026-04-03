---
execution: subagent
agent: accessibility-auditor
model_tier: powerful
inputFile: squads/fullstack-dev/output/frontend-output.md
outputFile: squads/fullstack-dev/output/accessibility-report.md
---

# Step 13: Accessibility Audit

## Context Loading

Load these files before executing:
- `squads/fullstack-dev/output/frontend-output.md` — código frontend
- `squads/fullstack-dev/pipeline/data/research-brief.md` — WCAG 2.1 reference
- `squads/fullstack-dev/pipeline/data/quality-criteria.md` — critérios de acessibilidade

## Instructions

### Process
1. Verificar HTML semântico e ARIA landmarks
2. Testar navegação por teclado em todos os elementos interativos
3. Verificar contraste de cores (>= 4.5:1 texto normal, >= 3:1 texto grande)
4. Validar alt text em todas as imagens
5. Verificar focus management em modais e componentes dinâmicos
6. Executar task `accessibility-audit` da Ada Acessibilidade
7. Compilar relatório com issues referenciando WCAG SC

## Output Format

```markdown
# Accessibility Audit Report

## Resumo
- POUR: {status por princípio}
- Issues: {N} ({levels})
- Veredicto: {PASS | FAIL}

## POUR Checklist
{checklist por princípio}

## Issues
### A11Y-{N} [{LEVEL}] — SC {number}
Componente / Descrição / Impacto / Remediação

## Veredicto
```

## Output Example

```markdown
# Accessibility Audit: Auth System
## Resumo
- Issues: 2 (1 Level A, 1 Level AA)
- Veredicto: FAIL — 1 Level A bloqueante

### A11Y-001 [Level A] — SC 2.1.1
Dropdown inacessível via teclado. Implementar com role="listbox".
```

## Veto Conditions

Reject and redo if ANY of these are true:
1. Algum princípio POUR não verificado
2. Issues sem WCAG success criterion

## Quality Criteria

- [ ] POUR completo verificado
- [ ] Contraste verificado
- [ ] Navegação por teclado testada
- [ ] Issues com WCAG SC específico
