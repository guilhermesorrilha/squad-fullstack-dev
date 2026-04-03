# Quality Criteria — Fullstack Dev Squad

## Critérios por Fase

### Planejamento (Orchestrator)
- [ ] Plano cobre 100% dos requisitos do briefing
- [ ] Cada tarefa tem responsável, prioridade e critério de aceite
- [ ] Dependências entre agentes estão mapeadas
- [ ] Riscos identificados com plano de mitigação
- [ ] Definition of done clara para cada entrega

### UX Design
- [ ] Wireframes cobrem todos os fluxos principais
- [ ] Edge cases mapeados (empty state, error, loading)
- [ ] Handoff com estados de interação completos
- [ ] Specs responsivas para mobile, tablet, desktop
- [ ] Anotações de acessibilidade presentes

### Frontend
- [ ] HTML semântico em todos os componentes
- [ ] Zero erros de lint
- [ ] Responsivo em 3 breakpoints
- [ ] Navegação por teclado funcional
- [ ] Componentes seguem Atomic Design
- [ ] Integração com APIs do Backend funcional

### Backend
- [ ] Todos os endpoints retornam status codes HTTP corretos
- [ ] Erros seguem RFC 7807
- [ ] Input validado no servidor
- [ ] Queries otimizadas com índices
- [ ] Testes de integração cobrindo happy path e error paths
- [ ] Autenticação e autorização implementadas

### QA
- [ ] 100% dos critérios de aceite verificados
- [ ] Bugs documentados com steps to reproduce
- [ ] Testes cobrem happy path + edge cases
- [ ] Integração Frontend-Backend validada end-to-end

### Security (OWASP Top 10)
- [ ] A01 — Broken Access Control verificado
- [ ] A02 — Cryptographic Failures verificado
- [ ] A03 — Injection (SQL, NoSQL, command) verificado
- [ ] A04 — Insecure Design verificado
- [ ] A05 — Security Misconfiguration verificado
- [ ] A06 — Vulnerable Components verificado
- [ ] A07 — Auth Failures verificado
- [ ] A08 — Data Integrity Failures verificado
- [ ] A09 — Logging Failures verificado
- [ ] A10 — SSRF verificado
- [ ] Headers de segurança (CSP, HSTS, X-Frame-Options)
- [ ] Remediação documentada para cada finding

### Accessibility (WCAG 2.1 AA)
- [ ] Perceivable: alt text, contraste >= 4.5:1, captions
- [ ] Operable: teclado, sem flash, tempo suficiente
- [ ] Understandable: linguagem clara, inputs com labels
- [ ] Robust: HTML válido, name/role/value para components
- [ ] Skip navigation link presente
- [ ] Focus management em modais e componentes dinâmicos

### SEO & Performance
- [ ] LCP < 2.5s
- [ ] INP < 200ms
- [ ] CLS < 0.1
- [ ] Meta tags (title, description) únicas por página
- [ ] Open Graph tags presentes
- [ ] Canonical URLs configuradas
- [ ] Structured data (JSON-LD) válido
- [ ] Imagens otimizadas com lazy loading

### Documentation
- [ ] 100% dos endpoints documentados com exemplos
- [ ] Todos os status codes listados
- [ ] README com setup funcional
- [ ] Changelog segue Keep a Changelog

### Deploy
- [ ] Pipeline CI/CD funcional
- [ ] Health checks ativos
- [ ] Rollback automático configurado
- [ ] Zero config manual em produção

## Regras de Veredicto

| Condição | Veredicto |
|----------|-----------|
| Todos os critérios da fase atendidos | PASS |
| Bugs critical ou mais de 5 major | FAIL → volta para implementação |
| Vulnerabilidade critical/high | FAIL → volta para implementação |
| Falha WCAG Level A | FAIL → volta para implementação |
| 2+ ciclos de rejeição no mesmo item | ESCALATE → decisão do usuário |
