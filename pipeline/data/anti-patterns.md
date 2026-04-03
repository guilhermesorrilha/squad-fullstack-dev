# Anti-Patterns — Fullstack Dev Squad

## Planejamento
1. **Estimation theater** — Gastar horas estimando tarefas em pontos/horas que nunca são revisitados. Use timebox e priorização ao invés de estimativas detalhadas.
2. **Zombie sprints** — Carregar tarefas inacabadas de sprint em sprint sem questionar se ainda são relevantes.
3. **Sem definition of done** — Cada agente interpreta "pronto" de forma diferente. DoD deve ser explícita e acordada.

## UX Design
4. **Pular wireframes low-fi** — Ir direto para mockups polidos desperdiça tempo com visual antes de validar fluxo.
5. **Design-to-dev cliff** — Entregar um Figma bonito sem estados de interação, edge cases ou specs responsivas.
6. **Telas isoladas** — Projetar cada tela sem considerar o fluxo completo do usuário.

## Frontend
7. **CSS specificity wars** — Uso de `!important`, seletores aninhados profundamente, sem convenção de nomes.
8. **Div soup** — Usar `<div>` para tudo ao invés de elementos semânticos (`<nav>`, `<main>`, `<article>`).
9. **Prop drilling** — Passar estado por 5+ camadas de componentes ao invés de usar contexto/store.
10. **Ignorar teclado** — Elementos interativos construídos sobre `<div>` sem `tabindex`, `role` ou event handlers de teclado.

## Backend
11. **Chatty APIs (N+1)** — Exigir múltiplos roundtrips para montar uma única tela. Oferecer endpoints compostos ou includes.
12. **Leaking domain models** — Expor schema interno do banco diretamente como resposta de API. Usar DTOs.
13. **Silent failures** — Retornar HTTP 200 com um corpo de erro dentro do JSON. Use status codes corretos.
14. **Hardcoded secrets** — Credenciais no código fonte ou em commits. Use variáveis de ambiente e secrets management.

## QA
15. **Testar só happy path** — Ignorar edge cases (inputs vazios, limites, caracteres especiais, erros de rede).
16. **Tolerar flaky tests** — Testes que falham intermitentemente destroem confiança no pipeline. Corrigir ou remover.
17. **Testar implementação, não comportamento** — Testes que quebram em refatorações que não mudam funcionalidade.

## Security
18. **Security como gate final** — Encontrar vulnerabilidades só no final do ciclo, quando o custo de correção é máximo. Shift-left.
19. **Confiar em validação client-side** — Qualquer validação no browser pode ser bypassada. Sempre revalidar no servidor.
20. **Hardcoded secrets em repos** — API keys, passwords, tokens commitados. Use .env + secrets manager.

## Accessibility
21. **ARIA misuse** — Adicionar `role` e `aria-*` em elementos que já tem semântica nativa (ex: `<button role="button">`).
22. **Focus traps sem escape** — Modais que capturam foco do teclado sem oferecer forma de sair.
23. **Informação só por cor** — Erros indicados apenas por vermelho, sem ícone, texto ou padrão visual complementar.

## SEO & Performance
24. **Render-blocking resources** — JS/CSS síncronos no `<head>` atrasando LCP. Use async/defer e critical CSS.
25. **Missing canonical tags** — URLs duplicadas (www/non-www, trailing slash) diluindo sinais de ranking.
26. **Imagens sem dimensões** — `<img>` sem width/height causando CLS.

## Documentation
27. **Docs como afterthought** — Documentação escrita post-launch quando o código já divergiu.
28. **Sem exemplos executáveis** — Docs descrevem endpoints mas não incluem curl/SDK snippets copiáveis.
29. **Error codes não documentados** — Documentar só respostas 200, deixando 4xx/5xx como surpresa.

## DevOps
30. **Long-lived feature branches** — Branches vivendo semanas causam merge conflicts massivos. Trunk-based + feature flags.
31. **Deploy sem rollback** — Todo deploy deve ter rollback automatizado baseado em health checks.
32. **Infra manual** — Configuração manual em produção é risco. Everything as Code.
