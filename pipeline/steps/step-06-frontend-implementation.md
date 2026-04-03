---
execution: subagent
agent: frontend-dev
model_tier: powerful
inputFile: squads/fullstack-dev/output/wireframes.md
outputFile: squads/fullstack-dev/output/frontend-output.md
---

# Step 06: Frontend Implementation

## Context Loading

Load these files before executing:
- `squads/fullstack-dev/output/wireframes.md` — wireframes aprovados do UX Designer
- `squads/fullstack-dev/output/project-plan.md` — plano com contratos de API e critérios de aceite
- `squads/fullstack-dev/pipeline/data/research-brief.md` — Frontend best practices (Atomic Design, CDD)
- `squads/fullstack-dev/pipeline/data/quality-criteria.md` — critérios de qualidade para Frontend
- `_opensquad/_memory/company.md` — contexto da empresa

## Instructions

### Process
1. Analisar wireframes e extrair a lista completa de componentes necessários
2. Definir arquitetura de componentes seguindo Atomic Design (átomos → moléculas → organismos → templates → páginas)
3. Implementar cada componente com HTML semântico, acessibilidade nativa e responsividade
4. Implementar todos os estados de interação documentados nos wireframes (default, hover, focus, error, loading, empty)
5. Integrar com APIs do Backend usando os contratos definidos no plano (com error handling)
6. Verificar navegação por teclado em todos os elementos interativos

## Output Format

O output MUST follow this exact structure:
```markdown
# Frontend Implementation: {projeto}

## Arquitetura de Componentes
{diagrama de componentes — Atomic Design}

## Componentes Implementados
### {ComponentName}
- Tipo: {atom/molecule/organism}
- Props: {lista}
- Estados: {lista}
- Acessibilidade: {notas}
- Código: {implementação completa}

## Integração com Backend
{endpoints consumidos e tratamento de erros}

## Código Completo
{todo o código organizado por arquivo}
```

## Output Example

```markdown
# Frontend Implementation: Auth System

## Arquitetura
Page: LoginPage
├── Organism: LoginForm
│   ├── Molecule: OAuthButton
│   └── Atom: ErrorBanner
└── Organism: Header

## Componentes
### OAuthButton
- Tipo: molecule
- Props: provider, onLogin, disabled
- Estados: default, hover, focus, loading
- Código:
function OAuthButton({ provider, onLogin }) {
  // implementação completa...
}
```

## Veto Conditions

Reject and redo if ANY of these are true:
1. Estados de interação dos wireframes não implementados
2. Elementos interativos inacessíveis via teclado

## Quality Criteria

- [ ] HTML semântico em todos os componentes
- [ ] Responsivo em 3 breakpoints
- [ ] Todos os estados de interação implementados
- [ ] Navegação por teclado funcional
- [ ] Integração com APIs funcional
