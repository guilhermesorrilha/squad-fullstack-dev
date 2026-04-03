---
task: "Analyze Requirements"
order: 1
input: |
  - project_briefing: Briefing do projeto descrito pelo usuário
  - company_context: Contexto da empresa (company.md)
output: |
  - requirements: Lista de requisitos funcionais e não-funcionais
  - risks: Riscos identificados com mitigação
  - dependencies: Mapa de dependências entre componentes
---

# Analyze Requirements

Analisa o briefing do projeto para extrair requisitos funcionais e não-funcionais, identificar riscos e mapear dependências entre os componentes do sistema.

## Process

1. Ler o briefing do projeto e extrair todos os requisitos explícitos e implícitos
2. Classificar requisitos em funcionais (features) e não-funcionais (performance, segurança, acessibilidade)
3. Identificar ambiguidades e listar decisões que precisam ser tomadas
4. Mapear dependências entre frontend, backend e infraestrutura
5. Identificar riscos técnicos com plano de mitigação para cada um

## Output Format

```yaml
requirements:
  functional:
    - id: "REQ-001"
      description: "..."
      priority: "P0"
      acceptance_criteria:
        - "..."
  non_functional:
    - id: "NFR-001"
      description: "..."
      category: "performance | security | accessibility | seo"

dependencies:
  - from: "frontend"
    to: "backend"
    description: "..."

risks:
  - id: "RISK-001"
    description: "..."
    probability: "high | medium | low"
    impact: "high | medium | low"
    mitigation: "..."

open_questions:
  - "..."
```

## Output Example

> Use as quality reference, not as rigid template.

```yaml
requirements:
  functional:
    - id: "REQ-001"
      description: "Login com OAuth2 (Google e GitHub)"
      priority: "P0"
      acceptance_criteria:
        - "Botão de login visível na landing page"
        - "Redirect correto após autorização OAuth"
        - "Sessão persiste por 7 dias com refresh token"
        - "Error handling para falhas de OAuth (timeout, denied)"
    - id: "REQ-002"
      description: "Dashboard com métricas do usuário"
      priority: "P1"
      acceptance_criteria:
        - "Exibe total de projetos, última atividade, uso de storage"
        - "Dados atualizados em tempo real ou com polling de 30s"
        - "Loading state enquanto dados carregam"
        - "Empty state para usuários novos sem dados"
  non_functional:
    - id: "NFR-001"
      description: "LCP < 2.5s em todas as páginas"
      category: "performance"
    - id: "NFR-002"
      description: "WCAG 2.1 AA em todos os componentes interativos"
      category: "accessibility"

dependencies:
  - from: "frontend-login"
    to: "backend-oauth"
    description: "Frontend precisa de endpoints OAuth configurados antes de implementar fluxo de login"
  - from: "frontend-dashboard"
    to: "backend-metrics-api"
    description: "Dashboard consome API de métricas — contrato de API deve ser definido primeiro"

risks:
  - id: "RISK-001"
    description: "Rate limiting do Google OAuth em ambiente de desenvolvimento"
    probability: "medium"
    impact: "low"
    mitigation: "Usar mock OAuth em testes, reservar rate limit para staging"
  - id: "RISK-002"
    description: "Dados de métricas podem ser pesados para consulta real-time"
    probability: "medium"
    impact: "medium"
    mitigation: "Implementar cache com TTL de 30s e materialized views"
```

## Quality Criteria

- [ ] Todos os requisitos do briefing cobertos (nenhum ignorado)
- [ ] Cada requisito funcional tem critérios de aceite específicos
- [ ] Dependências entre frontend e backend mapeadas
- [ ] Riscos com probabilidade, impacto e mitigação

## Veto Conditions

Reject and redo if ANY are true:
1. Requisitos do briefing foram ignorados ou interpretados incorretamente
2. Requisitos funcionais sem critérios de aceite
