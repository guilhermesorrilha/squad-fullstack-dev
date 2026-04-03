---
execution: inline
agent: devops
inputFile: squads/fullstack-dev/output/project-plan.md
outputFile: squads/fullstack-dev/output/deploy-report.md
---

# Step 17: Deploy

## Context Loading

Load these files before executing:
- `squads/fullstack-dev/output/project-plan.md` — plano com requisitos de infra
- `squads/fullstack-dev/output/frontend-output.md` — código frontend
- `squads/fullstack-dev/output/backend-output.md` — código backend
- `squads/fullstack-dev/output/documentation.md` — documentação (para incluir no deploy)
- `squads/fullstack-dev/pipeline/data/research-brief.md` — DevOps best practices

## Instructions

### Process
1. Analisar stack do projeto e definir requisitos de infraestrutura
2. Configurar pipeline CI/CD (build → lint → test → deploy)
3. Configurar ambientes staging e production
4. Implementar estratégia de deploy (blue-green ou canary)
5. Executar task `setup-deploy` da Diana Deploy
6. Configurar health checks e rollback automático
7. Executar deploy e verificar status

## Output Format

```markdown
# Deploy Report: {projeto}

## Pipeline CI/CD
{configuração do pipeline}

## Ambientes
{staging, production — URLs e status}

## Estratégia de Deploy
{blue-green ou canary — detalhes}

## Health Checks
{endpoints, intervalos, thresholds}

## Rollback
{trigger e processo}

## Status
{resultado do deploy}
```

## Output Example

```markdown
# Deploy: Auth System
## Pipeline
push → install → lint → test → build → deploy staging → health check → [approval] → deploy prod
## Status
Deploy executado com sucesso. Health checks passando.
```

## Veto Conditions

Reject and redo if ANY of these are true:
1. Deploy sem health checks configurados
2. Sem estratégia de rollback

## Quality Criteria

- [ ] Pipeline CI/CD configurado
- [ ] Health checks ativos
- [ ] Rollback automático configurado
- [ ] Zero config manual em produção
