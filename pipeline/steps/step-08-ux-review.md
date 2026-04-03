---
execution: inline
agent: ux-designer
inputFile: squads/fullstack-dev/output/frontend-output.md
outputFile: squads/fullstack-dev/output/ux-review.md
---

# Step 08: UX Review

## Context Loading

Load these files before executing:
- `squads/fullstack-dev/output/frontend-output.md` — implementação do Frontend
- `squads/fullstack-dev/output/wireframes.md` — wireframes aprovados (para comparação)
- `squads/fullstack-dev/pipeline/data/quality-criteria.md` — critérios de qualidade UX

## Instructions

### Process
1. Comparar cada tela implementada contra o wireframe aprovado
2. Verificar se todos os estados de interação foram implementados (hover, focus, error, loading, empty)
3. Verificar responsividade nos 3 breakpoints documentados
4. Verificar consistência visual (espaçamentos, alinhamentos, tipografia)
5. Executar task `review-ui` da Uma Usabilidade
6. Emitir veredicto: APPROVED, NEEDS CHANGES, ou REJECTED

## Output Format

```markdown
# UX Review: {projeto}

## Resumo
- Telas revisadas: {N}/{N}
- Estados verificados: {N}/{N}
- Veredicto: {APPROVED | NEEDS CHANGES | REJECTED}

## Findings
### {Tela/Componente}
- Status: {OK | Issue}
- Descrição: ...
- Wireframe reference: ...
- Fix sugerido: ...

## Veredicto
{veredicto} — {justificativa}
```

## Output Example

```markdown
# UX Review: Auth System

## Resumo
- Telas revisadas: 3/3
- Estados verificados: 12/14
- Veredicto: NEEDS CHANGES

## Findings
### Dashboard — Empty State
- Status: Issue
- Descrição: Empty state não implementado. Dashboard mostra zeros.
- Wireframe reference: Fluxo "Primeiro Acesso" → empty state
- Fix sugerido: Implementar empty state com ilustração + CTA

## Veredicto
NEEDS CHANGES — 2 issues que divergem dos wireframes aprovados.
```

## Veto Conditions

Reject and redo if ANY of these are true:
1. Review não comparou todas as telas contra wireframes
2. Estados de interação não verificados

## Quality Criteria

- [ ] Todas as telas comparadas contra wireframes
- [ ] Todos os estados de interação verificados
- [ ] Responsividade verificada nos 3 breakpoints
- [ ] Findings com referência ao wireframe original
