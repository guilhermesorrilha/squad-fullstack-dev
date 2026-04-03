---
task: "Setup Deploy"
order: 1
input: |
  - project_plan: Plano com requisitos de infraestrutura
  - all_outputs: Outputs dos agentes anteriores
output: |
  - deploy_config: Configuração de CI/CD e deploy
  - deploy_report: Relatório de deploy com status
---

# Setup Deploy

Configura pipeline de CI/CD, ambientes e executa o deploy. Implementa health checks e rollback automático.

## Process

1. Analisar stack e requisitos de infraestrutura do projeto
2. Definir pipeline de CI/CD: build → lint → test → deploy
3. Configurar ambientes staging e production
4. Implementar estratégia de deploy (blue-green ou canary)
5. Configurar health checks com endpoints dedicados
6. Configurar rollback automático baseado em error rate
7. Executar deploy e verificar status
8. Compilar relatório com configuração e status

## Output Format

```markdown
# Deploy Report

## Pipeline CI/CD
{diagrama do pipeline}

## Ambientes
| Ambiente | URL | Status |
|----------|-----|--------|
| Staging  | ... | ...    |
| Production | ... | ...  |

## Estratégia de Deploy
{blue-green | canary — detalhes}

## Health Checks
| Endpoint | Intervalo | Threshold |
|----------|-----------|-----------|
| ...      | ...       | ...       |

## Rollback
- **Trigger:** {condição}
- **Processo:** {automático/manual}

## Configuração
{arquivos de configuração gerados}

## Status
{resultado do deploy}
```

## Output Example

> Use as quality reference, not as rigid template.

```markdown
# Deploy Report: Auth System

## Pipeline CI/CD
```
push to main
  → install dependencies
  → lint (ESLint + Prettier)
  → type check (TypeScript)
  → unit tests
  → integration tests
  → build (frontend + backend)
  → deploy staging
  → health check staging
  → [manual approval for production]
  → deploy production
  → health check production
  → [rollback if health check fails]
```

## Ambientes
| Ambiente   | URL                          | Status  |
|------------|------------------------------|---------|
| Staging    | https://staging.example.com  | HEALTHY |
| Production | https://app.example.com      | HEALTHY |

## Estratégia de Deploy
**Blue-Green** — duas instâncias idênticas. O deploy sobe a nova versão no ambiente inativo (green), roda health checks, e faz o swap de tráfego. O ambiente anterior (blue) permanece ativo por 30 minutos para rollback rápido.

## Health Checks
| Endpoint       | Intervalo | Threshold | Timeout |
|----------------|-----------|-----------|---------|
| /health        | 10s       | 3 falhas  | 5s      |
| /health/db     | 30s       | 2 falhas  | 10s     |
| /health/redis  | 30s       | 2 falhas  | 5s      |

## Rollback
- **Trigger:** 3 health check failures consecutivos OU error rate > 5% em 2 minutos
- **Processo:** Automático — swap de tráfego de volta para o ambiente anterior (blue)
- **Notificação:** Alert via webhook para canal de deploy

## Status
Deploy executado com sucesso. Todas as health checks passando. Aplicação disponível em production.
```

## Quality Criteria

- [ ] Pipeline CI/CD completo (build, lint, test, deploy)
- [ ] Ambientes staging e production configurados
- [ ] Health checks ativos com thresholds definidos
- [ ] Rollback automático configurado
- [ ] Zero configuração manual em produção

## Veto Conditions

Reject and redo if ANY are true:
1. Deploy sem health checks configurados
2. Sem estratégia de rollback definida
