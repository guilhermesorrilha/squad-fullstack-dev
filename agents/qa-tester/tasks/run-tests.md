---
task: "Run Tests"
order: 1
input: |
  - frontend_output: Implementação do Frontend
  - backend_output: Implementação do Backend
  - project_plan: Plano com critérios de aceite
output: |
  - qa_report: Relatório de QA com bugs e veredicto PASS/FAIL
---

# Run Tests

Executa testes funcionais contra critérios de aceite, valida integração end-to-end, identifica bugs e compila relatório estruturado com veredicto.

## Process

1. Ler critérios de aceite de cada user story no plano
2. Para cada critério, criar cenário de teste (happy path + edge cases)
3. Analisar código do Frontend e Backend para verificar implementação
4. Testar integração entre Frontend e Backend (contratos de API)
5. Testar error handling e edge cases (inputs inválidos, timeouts, empty states)
6. Documentar cada bug encontrado com steps to reproduce
7. Classificar bugs por severidade: critical, major, minor
8. Emitir veredicto PASS (nenhum critical/major) ou FAIL (com lista de bloqueios)

## Output Format

```markdown
# QA Report

## Resumo
- **Features testadas:** {N}/{N}
- **Critérios de aceite verificados:** {N}/{N}
- **Bugs encontrados:** {N} ({N} critical, {N} major, {N} minor)
- **Veredicto:** {PASS | FAIL}

## Testes Executados
### {Feature}
| Cenário | Resultado | Notas |
|---------|-----------|-------|
| ...     | PASS/FAIL | ...   |

## Bugs
### BUG-{N} [{SEVERITY}]
**Feature:** ...
**Steps to reproduce:**
1. ...
**Expected:** ...
**Actual:** ...
**Environment:** ...

## Veredicto
{PASS | FAIL} — {justificativa}
```

## Output Example

> Use as quality reference, not as rigid template.

```markdown
# QA Report: Sistema de Autenticação

## Resumo
- **Features testadas:** 3/3
- **Critérios de aceite verificados:** 12/15
- **Bugs encontrados:** 4 (1 critical, 1 major, 2 minor)
- **Veredicto:** FAIL — 1 bug critical bloqueia aprovação

## Testes Executados

### Login com Google
| Cenário                        | Resultado | Notas                          |
|--------------------------------|-----------|--------------------------------|
| Login happy path               | FAIL      | BUG-001: redirect falha        |
| Login com OAuth negado         | PASS      | Error banner exibido           |
| Login com timeout              | PASS      | Timeout tratado após 10s       |
| Loading state no botão         | PASS      | Spinner + texto "Entrando..."  |

### Dashboard
| Cenário                        | Resultado | Notas                          |
|--------------------------------|-----------|--------------------------------|
| Dashboard com dados            | PASS      | Métricas exibidas corretamente |
| Dashboard empty state          | FAIL      | BUG-003: mostra zeros          |
| Dashboard loading              | PASS      | Skeleton loader funcional      |

## Bugs

### BUG-001 [CRITICAL]
**Feature:** Login com Google
**Steps to reproduce:**
1. Clicar em "Entrar com Google"
2. Autorizar no Google OAuth consent screen
3. Observar redirect
**Expected:** Redirect para /dashboard com sessão ativa
**Actual:** Redirect para /login com erro 500 no console
**Environment:** Chrome 120, staging

### BUG-002 [MAJOR]
**Feature:** Recuperação de Sessão
**Steps to reproduce:**
1. Fazer login com Google
2. Fechar o browser
3. Abrir novamente após 1 hora
**Expected:** Sessão restaurada automaticamente via refresh token
**Actual:** Redirect para login — sessão perdida
**Environment:** Chrome, Firefox

## Veredicto
FAIL — BUG-001 (critical) impede o login funcionar. BUG-002 (major) afeta retenção de sessão. Recomendação: corrigir ambos e resubmeter para QA round 2.
```

## Quality Criteria

- [ ] 100% dos critérios de aceite verificados
- [ ] Cada bug com steps to reproduce completos
- [ ] Bugs classificados por severidade (critical/major/minor)
- [ ] Integração Frontend-Backend testada end-to-end
- [ ] Edge cases testados (inputs inválidos, empty states, timeouts)

## Veto Conditions

Reject and redo if ANY are true:
1. Critérios de aceite não foram todos verificados (alguns ignorados)
2. Bugs sem steps to reproduce documentados
