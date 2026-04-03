---
task: "Accessibility Audit"
order: 1
input: |
  - frontend_output: Código frontend implementado
output: |
  - accessibility_report: Relatório WCAG 2.1 AA com issues e veredicto
---

# Accessibility Audit

Executa auditoria de acessibilidade WCAG 2.1 Level AA. Verifica os quatro princípios POUR, testa navegação por teclado, contraste de cores, semântica HTML e ARIA.

## Process

1. Verificar HTML semântico e ARIA landmarks (header, nav, main, footer)
2. Verificar skip navigation link funcional
3. Testar navegação por teclado em todos os elementos interativos (Tab, Enter, Escape, Arrow keys)
4. Verificar contraste de cores (ratio >= 4.5:1 texto normal, >= 3:1 texto grande)
5. Validar alt text em todas as imagens (descritivo, não decorativo)
6. Verificar focus management em modais e componentes dinâmicos
7. Verificar labels e instrucões em todos os inputs de formulário
8. Testar com screen reader (verificar name/role/value para todos os componentes)
9. Compilar relatório com issues referenciando WCAG SC específico

## Output Format

```markdown
# Accessibility Audit Report

## Resumo
- **Princípio POUR:** {status por princípio}
- **Issues encontrados:** {N} ({N} Level A, {N} Level AA)
- **Veredicto:** {PASS | FAIL}

## POUR Checklist
### Perceivable
- [ ] Alt text em todas as imagens (SC 1.1.1)
- [ ] Contraste >= 4.5:1 texto normal (SC 1.4.3)
- [ ] Contraste >= 3:1 texto grande (SC 1.4.3)
...

### Operable
- [ ] Navegação por teclado funcional (SC 2.1.1)
- [ ] Focus visible em todos os elementos (SC 2.4.7)
...

### Understandable
- [ ] Lang attribute no HTML (SC 3.1.1)
- [ ] Labels em todos os inputs (SC 3.3.2)
...

### Robust
- [ ] HTML válido (SC 4.1.1)
- [ ] Name/role/value para componentes custom (SC 4.1.2)
...

## Issues
### A11Y-{N} [{LEVEL}] — SC {number}
**Componente:** ...
**Descrição:** ...
**Impacto:** ...
**Remediação:** ...

## Veredicto
{PASS | FAIL} — {justificativa}
```

## Output Example

> Use as quality reference, not as rigid template.

```markdown
# Accessibility Audit Report: Auth System

## Resumo
- **Perceivable:** 5/6 checks pass
- **Operable:** 4/5 checks pass
- **Understandable:** 4/4 checks pass
- **Robust:** 3/3 checks pass
- **Issues encontrados:** 3 (1 Level A, 2 Level AA)
- **Veredicto:** FAIL — 1 issue Level A bloqueia aprovação

## Issues

### A11Y-001 [Level A] — SC 2.1.1 Keyboard
**Componente:** Dropdown de seleção de projeto na dashboard
**Descrição:** Dropdown custom abre apenas com clique do mouse. Tab pula o componente e Arrow keys não navegam as opções.
**Impacto:** Usuários que dependem de teclado não conseguem selecionar projeto.
**Remediação:** Implementar com `<select>` nativo ou custom dropdown com role="listbox", aria-activedescendant, e handlers para Arrow Up/Down, Enter, Escape.

### A11Y-002 [Level AA] — SC 1.4.3 Contrast
**Componente:** Texto de placeholder nos inputs de busca
**Descrição:** Placeholder tem cor #999 sobre fundo #fff, resultando em contrast ratio de 2.85:1.
**Impacto:** Texto difícil de ler para usuários com baixa visão.
**Remediação:** Alterar placeholder para #767676 (ratio 4.54:1) ou mais escuro.

### A11Y-003 [Level AA] — SC 2.4.7 Focus Visible
**Componente:** Links no footer
**Descrição:** Links do footer têm `outline: none` sem estilo alternativo de foco visível.
**Impacto:** Usuários navegando por teclado perdem referência visual de onde estão.
**Remediação:** Remover `outline: none` ou adicionar estilo de foco custom (ex: box-shadow ou underline).

## Veredicto
FAIL — A11Y-001 (Level A) é bloqueante: componente inacessível via teclado viola critério fundamental. A11Y-002 e A11Y-003 (Level AA) devem ser corrigidos para conformidade completa.
```

## Quality Criteria

- [ ] Todos os 4 princípios POUR verificados
- [ ] Contraste verificado em todos os textos
- [ ] Navegação por teclado testada em 100% dos elementos interativos
- [ ] Cada issue referencia o WCAG success criterion específico
- [ ] Focus management verificado em modais e componentes dinâmicos

## Veto Conditions

Reject and redo if ANY are true:
1. Algum princípio POUR não foi verificado
2. Issues sem referência ao WCAG success criterion
