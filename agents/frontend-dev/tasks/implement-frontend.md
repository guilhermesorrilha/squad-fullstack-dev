---
task: "Implement Frontend"
order: 1
input: |
  - wireframes: Wireframes aprovados do UX Designer
  - project_plan: Plano com contratos de API e critérios de aceite
output: |
  - frontend_code: Código frontend implementado (componentes, layouts, CSS, interatividade)
  - integration_notes: Notas de integração com Backend
---

# Implement Frontend

Implementa a interface completa seguindo os wireframes aprovados: componentes, layouts, CSS e interatividade. Integra com APIs do Backend conforme contratos definidos.

## Process

1. Analisar wireframes e extrair lista de componentes necessários
2. Definir arquitetura de componentes seguindo Atomic Design (átomos → moléculas → organismos)
3. Implementar componentes base com HTML semântico
4. Aplicar estilos responsivos (mobile-first, 3 breakpoints)
5. Implementar estados de interação conforme wireframes (hover, focus, error, loading, empty)
6. Integrar com APIs do Backend usando contratos definidos no plano
7. Implementar acessibilidade nativa (teclado, foco, ARIA quando necessário)
8. Verificar em múltiplos viewports antes de entregar

## Output Format

```markdown
# Frontend Implementation

## Arquitetura de Componentes
{diagrama de componentes}

## Componentes Implementados
### {ComponentName}
- **Tipo:** atom | molecule | organism
- **Props:** {lista}
- **Estados:** {lista}
- **Acessibilidade:** {notas}
- **Código:** {código do componente}

## Integração com Backend
### {endpoint}
- **Usado em:** {componente}
- **Tratamento de erros:** {descrição}

## Código Completo
{todo o código implementado organizado por arquivo}

## Notas de Integração
- {notas para o Backend ou outros agentes}
```

## Output Example

> Use as quality reference, not as rigid template.

```markdown
# Frontend Implementation: Login Page

## Arquitetura de Componentes
Page: LoginPage
├── Organism: LoginForm
│   ├── Molecule: OAuthButton (Google)
│   ├── Molecule: OAuthButton (GitHub)
│   └── Atom: ErrorBanner
└── Organism: Header
    ├── Atom: Logo
    └── Atom: NavLink

## Componentes Implementados

### OAuthButton
- **Tipo:** molecule
- **Props:** provider ("google" | "github"), onLogin(), disabled
- **Estados:** default, hover, focus, loading, disabled
- **Acessibilidade:** `<button>` nativo, aria-label="Entrar com {provider}", aria-busy durante loading
- **Código:**
```tsx
function OAuthButton({ provider, onLogin, disabled }: OAuthButtonProps) {
  const [loading, setLoading] = useState(false);

  const handleClick = async () => {
    setLoading(true);
    try {
      await onLogin();
    } finally {
      setLoading(false);
    }
  };

  return (
    <button
      className={`oauth-btn oauth-btn--${provider}`}
      onClick={handleClick}
      disabled={disabled || loading}
      aria-label={`Entrar com ${provider === 'google' ? 'Google' : 'GitHub'}`}
      aria-busy={loading}
    >
      {loading ? <Spinner /> : <ProviderIcon provider={provider} />}
      {loading ? 'Entrando...' : `Entrar com ${provider === 'google' ? 'Google' : 'GitHub'}`}
    </button>
  );
}
```

### ErrorBanner
- **Tipo:** atom
- **Props:** message, onDismiss()
- **Estados:** visible, hidden
- **Acessibilidade:** role="alert", aria-live="polite", botão dismiss com aria-label
```

## Quality Criteria

- [ ] HTML semântico em todos os componentes (sem div soup)
- [ ] Responsivo em 3 breakpoints (mobile, tablet, desktop)
- [ ] Todos os estados de interação implementados conforme wireframes
- [ ] Navegação por teclado funcional em todos os elementos interativos
- [ ] Integração com APIs do Backend funcional e com error handling
- [ ] Componentes seguem Atomic Design

## Veto Conditions

Reject and redo if ANY are true:
1. Estados de interação dos wireframes não implementados (especialmente error e loading)
2. Elementos interativos não acessíveis via teclado
