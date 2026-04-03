# Research Brief — Fullstack Dev Squad

## 1. Project Management (Kanban)

**Framework:** Kanban com WIP limits. Visualizar trabalho, limitar WIP, otimizar fluxo. Preferido sobre Scrum para squads pequenos por ter menos cerimônia.

**Key Concepts:** WIP limit, cycle time, throughput, definition of done, retrospective.

**Anti-patterns:** Zombie sprints (tarefas carregadas sem re-estimativa), sem WIP limits, estimation theater.

---

## 2. UX Design (Double Diamond)

**Framework:** Double Diamond (Discover > Define > Develop > Deliver). Handoff via specs anotadas com estados de interação, design tokens e specs responsivas.

**Key Concepts:** User flow, information architecture, design token, affordance, design system.

**Anti-patterns:** Pular wireframes low-fi, projetar telas isoladas sem fluxo, handoff sem estados de interação.

---

## 3. Frontend Development (Atomic Design / CDD)

**Framework:** Component-Driven Development com Atomic Design (atoms > molecules > organisms > templates > pages). HTML semântico antes de ARIA.

**Key Concepts:** Hydration, tree shaking, critical rendering path, compound component, design token.

**Anti-patterns:** CSS specificity wars, prop drilling, div soup, ignorar navegação por teclado.

---

## 4. Backend Development (REST / RFC 7807)

**Framework:** REST com RFC 7807 (Problem Details) para erros padronizados. Repository Pattern para desacoplar acesso a dados de regras de negócio.

**Key Concepts:** Idempotency, pagination cursor, query plan, circuit breaker, contract testing.

**Anti-patterns:** Chatty APIs (N+1), leaking domain models, silent failures, hardcoded secrets.

---

## 5. QA Testing (Testing Trophy)

**Framework:** Testing Trophy (Kent C. Dodds) — integration tests como camada principal, unit tests menores, e2e seletivos. Bug reports: Steps / Expected / Actual / Environment.

**Key Concepts:** Test pyramid, flaky test, test double, coverage threshold, smoke test.

**Anti-patterns:** Testar só happy path, tolerar flaky tests, testar detalhes de implementação.

---

## 6. Security (OWASP Top 10 — 2021)

**Framework:** OWASP Top 10: A01 Broken Access Control, A02 Cryptographic Failures, A03 Injection, A04 Insecure Design, A05 Security Misconfiguration, A06 Vulnerable Components, A07 Auth Failures, A08 Data Integrity Failures, A09 Logging Failures, A10 SSRF.

**Key Concepts:** Threat model, attack surface, CVE, least privilege, defense in depth.

**Anti-patterns:** Security como gate final, hardcoded secrets, confiar em validação client-side.

---

## 7. Accessibility (WCAG 2.1 — POUR)

**Framework:** WCAG 2.1 POUR (Perceivable, Operable, Understandable, Robust). Target Level AA. Key criteria: 1.4.3 (contrast >= 4.5:1), 2.4.7 (focus visible), 1.1.1 (alt text), 4.1.2 (name/role/value).

**Key Concepts:** ARIA landmark, focus management, screen reader, contrast ratio, skip navigation.

**Anti-patterns:** ARIA misuse, focus traps sem escape, informação só por cor.

---

## 8. SEO & Web Performance (Core Web Vitals)

**Framework:** Core Web Vitals: LCP < 2.5s, INP < 200ms, CLS < 0.1. Structured data via JSON-LD (schema.org). Meta tags essenciais: title, description, OG, canonical.

**Key Concepts:** SERP, crawl budget, hreflang, JSON-LD, page experience signal.

**Anti-patterns:** Render-blocking resources, missing canonical tags, imagens sem dimensões.

---

## 9. Technical Writing (OpenAPI 3.1)

**Framework:** OpenAPI Specification 3.1 como source of truth. READMEs: Standard-Readme spec. Changelogs: Keep a Changelog (Added, Changed, Deprecated, Removed, Fixed, Security).

**Key Concepts:** Endpoint, schema, request body, response envelope, deprecation notice.

**Anti-patterns:** Docs como afterthought, sem exemplos executáveis, error codes não documentados.

---

## 10. DevOps (GitOps / Trunk-Based)

**Framework:** GitOps para Kubernetes, trunk-based development para pipelines rápidos. Deploy: Blue-Green (cutover) ou Canary (progressive traffic shifting). IaC: Terraform ou Pulumi.

**Key Concepts:** Deployment pipeline, artifact, immutable infrastructure, MTTR, feature flag.

**Anti-patterns:** Long-lived branches, manual approval em todo ambiente, deploy sem rollback.
