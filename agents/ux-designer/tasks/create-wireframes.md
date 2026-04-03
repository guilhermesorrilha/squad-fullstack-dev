---
task: "Create Wireframes"
order: 1
input: |
  - project_plan: Plano do Orchestrator com user stories e requisitos
output: |
  - wireframes: Wireframes low-fidelity em formato texto/ASCII
  - user_flows: Mapa de fluxos de usuário
  - design_specs: Especificações de design e estados de interação
---

# Create Wireframes

Cria wireframes low-fidelity e mapeia fluxos de usuário baseado no plano do Orchestrator. Documenta todos os estados de interação e specs responsivas para handoff ao Frontend.

## Process

1. Analisar user stories e critérios de aceite do plano
2. Mapear fluxos de usuário completos (happy path + edge cases)
3. Criar wireframes low-fidelity para cada tela usando representação textual/ASCII
4. Documentar estados de interação para cada componente (default, hover, focus, error, loading, empty, success)
5. Definir specs responsivas para 3 breakpoints (mobile 375px, tablet 768px, desktop 1280px)
6. Anotar requisitos de acessibilidade (contraste, foco, labels)

## Output Format

```markdown
# Wireframes: {projeto}

## Fluxos de Usuário
### Fluxo: {nome}
{diagrama de fluxo textual}

## Telas
### Tela: {nome}
**URL:** {rota}
**Fluxos relacionados:** {lista}

#### Layout (Desktop)
{wireframe ASCII/textual}

#### Estados de Interação
| Componente | Default | Hover | Focus | Error | Loading | Empty |
|------------|---------|-------|-------|-------|---------|-------|
| ...        | ...     | ...   | ...   | ...   | ...     | ...   |

#### Responsividade
- **Mobile:** {adaptações}
- **Tablet:** {adaptações}

#### Acessibilidade
- {anotações de a11y}
```

## Output Example

> Use as quality reference, not as rigid template.

```markdown
# Wireframes: Sistema de Autenticação

## Fluxos de Usuário

### Fluxo: Login com OAuth
[Landing Page] → Clique "Login com Google" → [Google Consent] → Autoriza → [Dashboard]
                                                                → Nega → [Landing Page com erro]
                                                                → Timeout → [Landing Page com erro]

### Fluxo: Primeiro Acesso
[Landing Page] → Login → [Dashboard (empty state)] → [Tooltip de onboarding]

## Telas

### Tela: Landing Page / Login
**URL:** /
**Fluxos relacionados:** Login com OAuth, Primeiro Acesso

#### Layout (Desktop)
┌──────────────────────────────────────────┐
│  Logo                        [Entrar]    │
├──────────────────────────────────────────┤
│                                          │
│     Headline principal                   │
│     Subtítulo explicativo                │
│                                          │
│     ┌──────────────────────┐             │
│     │ 🔵 Entrar com Google │             │
│     └──────────────────────┘             │
│     ┌──────────────────────┐             │
│     │ ⚫ Entrar com GitHub │             │
│     └──────────────────────┘             │
│                                          │
│     Texto de termos de uso               │
│                                          │
├──────────────────────────────────────────┤
│  Footer: links, copyright               │
└──────────────────────────────────────────┘

#### Estados de Interação
| Componente       | Default          | Hover             | Focus             | Error                    | Loading              |
|------------------|------------------|-------------------|-------------------|--------------------------|----------------------|
| Botão Google     | Fundo branco     | Sombra + escurece | Outline azul 2px  | —                        | Spinner + "Entrando" |
| Botão GitHub     | Fundo preto      | Opacity 0.9       | Outline azul 2px  | —                        | Spinner + "Entrando" |
| Error banner     | Oculto           | —                 | —                 | Visível: ícone + mensagem| —                    |

#### Responsividade
- **Mobile (375px):** Botões full-width, headline menor, logo centralizada
- **Tablet (768px):** Layout centrado com max-width 480px

#### Acessibilidade
- Botões com `aria-label` descritivo: "Entrar com conta Google"
- Error banner com `role="alert"` e `aria-live="polite"`
- Focus order: Logo → Botão Google → Botão GitHub → Links footer
- Contraste mínimo 4.5:1 em todos os textos
```

## Quality Criteria

- [ ] Todos os fluxos de usuário mapeados (happy path + edge cases)
- [ ] Wireframes para todas as telas mencionadas nas user stories
- [ ] Estados de interação documentados para cada componente interativo
- [ ] Specs responsivas para 3 breakpoints
- [ ] Anotações de acessibilidade presentes

## Veto Conditions

Reject and redo if ANY are true:
1. Fluxos de usuário não cobrem os edge cases (erro, empty, loading)
2. Wireframes sem estados de interação documentados
