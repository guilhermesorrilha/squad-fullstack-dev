# Domain Framework — Fullstack Dev Squad

## Metodologia Operacional

O squad segue um fluxo linear com checkpoints de aprovação humana entre cada fase:

### Fase 1: Planejamento (Orchestrator)
1. Receber briefing do projeto com requisitos funcionais e não-funcionais
2. Decompor requisitos em user stories com critérios de aceite
3. Mapear dependências entre frontend, backend e infra
4. Atribuir tarefas com prioridade (P0/P1/P2) e WIP limits
5. Definir definition of done para cada entrega

### Fase 2: Design (UX Designer)
1. Mapear fluxos de usuário completos (happy path + edge cases)
2. Criar wireframes low-fidelity com anotações de interação
3. Documentar design tokens e specs responsivas (3 breakpoints)
4. Entregar handoff com todos os estados (hover, error, loading, empty)

### Fase 3: Implementação (Frontend + Backend em paralelo)
- **Frontend:** Atomic Design, HTML semântico, componentes acessíveis, integração com APIs
- **Backend:** REST com RFC 7807 para erros, validação server-side, Repository Pattern
- Após implementação, UX Designer revisa UI contra wireframes

### Fase 4: Qualidade (QA Tester)
1. Testes funcionais contra critérios de aceite
2. Testes de integração Frontend ↔ Backend
3. Edge cases e error paths
4. Relatório com bugs categorizados por severidade
5. Veredicto PASS/FAIL — FAIL volta para implementação

### Fase 5: Auditorias (Security + Accessibility + SEO — paralelo)
- **Security:** OWASP Top 10 checklist, headers, autenticação, CORS
- **Accessibility:** WCAG 2.1 AA, POUR, contraste, teclado, screen reader
- **SEO/Performance:** Core Web Vitals, meta tags, structured data, render-blocking

### Fase 6: Documentação (Tech Writer)
1. Documentação de API (OpenAPI 3.1) com exemplos executáveis
2. README atualizado com setup, usage e architecture
3. Changelog seguindo Keep a Changelog

### Fase 7: Deploy (DevOps)
1. Pipeline CI/CD (build → test → deploy)
2. Ambientes staging e production
3. Health checks e rollback automático
4. Estratégia blue-green ou canary conforme projeto

## Critérios de Decisão

- **Quando rejeitar no QA:** Qualquer bug critical ou mais de 5 bugs major
- **Quando rejeitar na Security:** Qualquer vulnerabilidade critical ou high
- **Quando rejeitar na Accessibility:** Qualquer falha Level A do WCAG
- **Quando escalar ao usuário:** Após 2 ciclos de rejeição no mesmo item
