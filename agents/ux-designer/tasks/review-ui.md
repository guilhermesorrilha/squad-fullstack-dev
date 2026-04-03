---
task: "Review UI"
order: 2
input: |
  - frontend_output: Código/output do Frontend Developer
  - wireframes: Wireframes aprovados (para comparação)
output: |
  - ux_review: Relatório de revisão com findings e veredicto
---

# Review UI

Revisa a implementação do Frontend contra os wireframes aprovados. Verifica se fluxos, estados de interação, responsividade e acessibilidade visual foram implementados corretamente.

## Process

1. Comparar cada tela implementada contra o wireframe aprovado
2. Verificar se todos os estados de interação foram implementados (hover, focus, error, loading, empty)
3. Verificar responsividade nos 3 breakpoints documentados
4. Verificar consistência visual (espaçamentos, alinhamentos, tipografia)
5. Emitir veredicto: APPROVED, NEEDS CHANGES, ou REJECTED

## Output Format

```markdown
# UX Review

## Resumo
- Telas revisadas: {N}/{N}
- Estados verificados: {N}/{N}
- Veredicto: {APPROVED | NEEDS CHANGES | REJECTED}

## Findings
### {Tela/Componente}
- **Status:** {OK | Issue}
- **Descrição:** ...
- **Wireframe reference:** ...
- **Fix sugerido:** ...

## Veredicto
{APPROVED | NEEDS CHANGES | REJECTED} — {justificativa}
```

## Output Example

> Use as quality reference, not as rigid template.

```markdown
# UX Review: Sistema de Autenticação

## Resumo
- Telas revisadas: 3/3
- Estados verificados: 12/14
- Veredicto: NEEDS CHANGES

## Findings

### Landing Page — Botões OAuth
- **Status:** Issue
- **Descrição:** Botão "Entrar com GitHub" não tem estado de loading. Ao clicar, nada visual acontece até o redirect do OAuth.
- **Wireframe reference:** Estados de interação — Botão GitHub — Loading: "Spinner + Entrando"
- **Fix sugerido:** Adicionar spinner e texto "Entrando..." ao clicar, desabilitar botão durante loading

### Dashboard — Empty State
- **Status:** Issue
- **Descrição:** Empty state para usuários novos não foi implementado. A dashboard mostra zeros ao invés do empty state projetado com onboarding.
- **Wireframe reference:** Fluxo "Primeiro Acesso" → Dashboard (empty state)
- **Fix sugerido:** Implementar empty state conforme wireframe: ilustração + texto "Crie seu primeiro projeto" + CTA

### Login — Error Banner
- **Status:** OK
- **Descrição:** Error banner implementado corretamente com role="alert", ícone + mensagem, e dismissível.

## Veredicto
NEEDS CHANGES — 2 issues de implementação que divergem dos wireframes aprovados. Nenhum é bloqueante de segurança, mas ambos afetam a experiência do usuário. Corrigir antes de prosseguir.
```

## Quality Criteria

- [ ] Todas as telas comparadas contra wireframes
- [ ] Todos os estados de interação verificados
- [ ] Responsividade verificada nos 3 breakpoints
- [ ] Findings com referência ao wireframe original
- [ ] Veredicto claro com justificativa

## Veto Conditions

Reject and redo if ANY are true:
1. Review não verificou todos os estados de interação documentados nos wireframes
2. Findings sem referência ao wireframe original
