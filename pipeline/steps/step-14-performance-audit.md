---
execution: subagent
agent: seo-performance
model_tier: powerful
inputFile: squads/fullstack-dev/output/frontend-output.md
outputFile: squads/fullstack-dev/output/performance-report.md
---

# Step 14: Performance & SEO Audit

## Context Loading

Load these files before executing:
- `squads/fullstack-dev/output/frontend-output.md` — código frontend
- `squads/fullstack-dev/pipeline/data/research-brief.md` — Core Web Vitals reference
- `squads/fullstack-dev/pipeline/data/quality-criteria.md` — critérios de performance e SEO

## Instructions

### Process
1. Analisar Core Web Vitals (LCP, INP, CLS) no código
2. Identificar render-blocking resources
3. Verificar otimização de imagens (dimensões, lazy loading)
4. Verificar meta tags essenciais (title, description, OG, canonical)
5. Auditar structured data (JSON-LD)
6. Executar task `performance-audit` do Pedro Performance
7. Compilar relatório com métricas e recomendações priorizadas

## Output Format

```markdown
# Performance & SEO Audit Report

## Core Web Vitals
| Métrica | Valor | Threshold | Status |
|---------|-------|-----------|--------|

## SEO Checklist
{checklist de meta tags e structured data}

## Issues
### PERF-{N} [{IMPACT}]
Tipo / Descrição / Impacto / Remediação / Prioridade

## Recomendações
{priorizadas por impacto}

## Veredicto
```

## Output Example

```markdown
# Performance Audit: Auth System
## Core Web Vitals
| Métrica | Valor | Threshold | Status |
|---------|-------|-----------|--------|
| LCP     | ~1.8s | < 2.5s   | GOOD   |
| CLS     | ~0.15 | < 0.1    | POOR   |

### PERF-001 [HIGH]
Imagens sem width/height causando CLS de 0.15.
```

## Veto Conditions

Reject and redo if ANY of these are true:
1. Core Web Vitals não analisados
2. Issues sem remediação

## Quality Criteria

- [ ] 3 Core Web Vitals analisados
- [ ] Meta tags verificadas
- [ ] Render-blocking resources identificados
- [ ] Recomendações priorizadas por impacto
