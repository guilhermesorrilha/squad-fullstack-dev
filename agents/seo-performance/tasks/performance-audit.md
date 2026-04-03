---
task: "Performance Audit"
order: 1
input: |
  - frontend_output: Código frontend implementado
output: |
  - performance_report: Relatório de performance e SEO com métricas e recomendações
---

# Performance Audit

Audita Core Web Vitals, meta tags, structured data e otimização de assets. Produz relatório com métricas mensuráveis e recomendações priorizadas por impacto.

## Process

1. Analisar Core Web Vitals (LCP, INP, CLS) no código
2. Identificar render-blocking resources (JS/CSS síncronos no head)
3. Verificar otimização de imagens (dimensões explícitas, lazy loading, formatos modernos)
4. Verificar meta tags essenciais (title, description, OG tags, canonical)
5. Auditar structured data (JSON-LD / schema.org) se aplicável
6. Verificar configuração de cache e compressão
7. Compilar relatório com métricas, issues e recomendações priorizadas

## Output Format

```markdown
# Performance & SEO Audit Report

## Core Web Vitals
| Métrica | Valor Estimado | Threshold | Status |
|---------|---------------|-----------|--------|
| LCP     | ...           | < 2.5s    | ...    |
| INP     | ...           | < 200ms   | ...    |
| CLS     | ...           | < 0.1     | ...    |

## SEO Checklist
- [ ] Title tag presente e único por página
- [ ] Meta description presente e único
- [ ] Open Graph tags presentes
- [ ] Canonical URL configurada
- [ ] Structured data (JSON-LD) válido
...

## Issues
### PERF-{N} [{IMPACT}]
**Tipo:** performance | seo
**Descrição:** ...
**Impacto na métrica:** ...
**Remediação:** ...
**Prioridade:** {alta | média | baixa}

## Recomendações (priorizadas por impacto)
1. ...
2. ...

## Veredicto
{PASS | NEEDS OPTIMIZATION | FAIL} — {justificativa}
```

## Output Example

> Use as quality reference, not as rigid template.

```markdown
# Performance & SEO Audit: Auth System

## Core Web Vitals
| Métrica | Valor Estimado | Threshold | Status |
|---------|---------------|-----------|--------|
| LCP     | ~1.8s         | < 2.5s    | GOOD   |
| INP     | ~120ms        | < 200ms   | GOOD   |
| CLS     | ~0.15         | < 0.1     | POOR   |

## SEO Checklist
- [x] Title tag presente e único por página
- [x] Meta description presente e único
- [ ] Open Graph tags presentes — MISSING
- [x] Canonical URL configurada
- [ ] Structured data (JSON-LD) — NOT IMPLEMENTED

## Issues

### PERF-001 [HIGH]
**Tipo:** performance
**Descrição:** Imagens de avatar no dashboard não têm width/height explícitos, causando layout shift quando carregam.
**Impacto na métrica:** CLS de 0.15 (above 0.1 threshold)
**Remediação:** Adicionar `width` e `height` nos `<img>` de avatar. Usar `aspect-ratio` CSS como fallback.
**Prioridade:** Alta — CLS é Core Web Vital, impacta ranking.

### PERF-002 [MEDIUM]
**Tipo:** seo
**Descrição:** Open Graph tags ausentes. Links compartilhados em redes sociais não mostram preview.
**Impacto na métrica:** Sem impacto em Core Web Vitals, mas afeta CTR de compartilhamentos.
**Remediação:** Adicionar og:title, og:description, og:image, og:url no head de cada página.
**Prioridade:** Média — afeta distribuição social, não ranking direto.

### PERF-003 [LOW]
**Tipo:** seo
**Descrição:** Structured data (JSON-LD) não implementado.
**Impacto na métrica:** Sem rich snippets nos resultados de busca.
**Remediação:** Adicionar JSON-LD com schema.org/WebApplication para a landing page.
**Prioridade:** Baixa — benefício incremental para este tipo de aplicação.

## Recomendações (priorizadas por impacto)
1. **[Alta]** Corrigir CLS: dimensões explícitas em imagens de avatar
2. **[Média]** Adicionar Open Graph tags para previews em redes sociais
3. **[Baixa]** Implementar JSON-LD para rich snippets

## Veredicto
NEEDS OPTIMIZATION — Core Web Vitals LCP e INP estão bons, mas CLS excede o threshold. 1 correção obrigatória (PERF-001) e 2 recomendações de SEO.
```

## Quality Criteria

- [ ] Todos os 3 Core Web Vitals analisados com valores estimados
- [ ] Meta tags verificadas (title, description, OG, canonical)
- [ ] Render-blocking resources identificados
- [ ] Imagens verificadas (dimensões, lazy loading)
- [ ] Recomendações priorizadas por impacto

## Veto Conditions

Reject and redo if ANY are true:
1. Core Web Vitals não foram analisados
2. Issues sem remediação documentada
