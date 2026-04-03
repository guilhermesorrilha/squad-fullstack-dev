---
execution: inline
agent: ux-designer
inputFile: squads/fullstack-dev/output/project-plan.md
outputFile: squads/fullstack-dev/output/wireframes.md
---

# Step 04: UX Wireframes & User Flows

## Context Loading

Load these files before executing:
- `squads/fullstack-dev/output/project-plan.md` — plano do projeto com user stories e requisitos
- `squads/fullstack-dev/pipeline/data/research-brief.md` — UX Design best practices (Double Diamond)
- `squads/fullstack-dev/pipeline/data/quality-criteria.md` — critérios de qualidade para UX
- `_opensquad/_memory/company.md` — contexto da empresa

## Instructions

### Process
1. Analisar todas as user stories do plano e identificar as telas necessárias
2. Mapear fluxos de usuário completos (happy path + edge cases: erro, empty, loading)
3. Executar task `create-wireframes` da Uma Usabilidade: criar wireframes low-fidelity em formato texto/ASCII para cada tela
4. Documentar estados de interação para cada componente interativo (default, hover, focus, error, loading, empty)
5. Definir specs responsivas para 3 breakpoints (mobile 375px, tablet 768px, desktop 1280px)
6. Anotar requisitos de acessibilidade (contraste, foco, labels, ARIA)

## Output Format

O output MUST follow this exact structure:
```markdown
# Wireframes: {projeto}

## Fluxos de Usuário
### Fluxo: {nome}
{diagrama textual do fluxo}

## Telas
### Tela: {nome}
**URL:** {rota}
#### Layout (Desktop)
{wireframe ASCII}
#### Estados de Interação
{tabela de estados por componente}
#### Responsividade
{adaptações por breakpoint}
#### Acessibilidade
{anotações de a11y}
```

## Output Example

```markdown
# Wireframes: Auth System

## Fluxos de Usuário
### Fluxo: Login
[Landing] → Click Login → [Google Consent] → Autoriza → [Dashboard]
                                             → Nega → [Landing + Error]

## Telas
### Tela: Landing Page
**URL:** /
#### Layout (Desktop)
┌────────────────────────────────┐
│  Logo                [Entrar]  │
├────────────────────────────────┤
│     Headline                   │
│     ┌────────────────┐         │
│     │ Entrar Google  │         │
│     └────────────────┘         │
│     ┌────────────────┐         │
│     │ Entrar GitHub  │         │
│     └────────────────┘         │
├────────────────────────────────┤
│  Footer                        │
└────────────────────────────────┘
```

## Veto Conditions

Reject and redo if ANY of these are true:
1. Fluxos não cobrem edge cases (erro, empty, loading)
2. Wireframes sem estados de interação

## Quality Criteria

- [ ] Todos os fluxos mapeados com happy path e edge cases
- [ ] Wireframes para todas as telas das user stories
- [ ] Estados de interação documentados para cada componente
- [ ] Specs responsivas para 3 breakpoints
- [ ] Anotações de acessibilidade presentes
