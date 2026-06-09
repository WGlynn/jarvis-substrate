# Advice actionable — VibeSwap frontend / contracts / infra

Populated by Odysseus cron loops § COMMANDMENT 2.5 per [F·odysseus-as-advisory-substrate].

Entries below are advice surfaced on pewdiepie-archdaemon/odysseus that the C2.5 classifier judged directly-applicable to our substrate. Each entry awaits Will-triage before any codebase work.

Format:
```
## [YYYY-MM-DD HH:MM ET] — <shape summary>
- Source: #NNNN comment by @author (URL)
- Their advice (paraphrase): ...
- Our substrate state: ...
- Suggested action: ...
- Will-triage: pending
```

---

## [2026-06-09 13:38 ET] — AI-cosplay single-purpose bloat files (langIcons.js shape)

- Source: Odysseus comment id `58plmahm02xg1` (author handle not in Will's paste; comment exists per `static/js/langIcons.js` being a real file in the repo). Reaction: @georgebrianb +1'd and offered CI/CD + autodeploy + LLM-security-check help as their first OSS contribution.
- Their advice (paraphrase): The static-JS shape (huge manual `langIcons.js` lookup file) is "AI cosplaying Odysseus avoiding the draft" — a sprawling hand-rolled artifact for what should be a library lookup or a config-driven mapping. First-order fix: migrate to a real framework + a component framework themed through ONE file.
- Our substrate state: VibeSwap frontend = React 18 + Vite 5 + Tailwind (already a "real framework"; the Nuxt-specific advice does NOT apply). HOWEVER the meta-shape ("AI generated a huge single-purpose file when a library or 10-line config would do") plausibly applies to several places — needs audit, not assumed.
- Suggested action: audit `vibeswap/frontend/src/` for AI-cosplay bloat shapes specifically: hardcoded large arrays/maps (chains, tokens, icons, locale strings), components that re-implement well-known library primitives, theming spread across many files instead of a single source. Output: ranked list of bloat-candidates with size + estimated library replacement.
- Will-triage: pending

## [2026-06-09 13:50 ET] — CI security-scanning baseline with blocking-vs-advisory split

- Source: PR #1314 by @nopoz "ci: security scanning suite and governance (consolidates #305-310)" — https://github.com/pewdiepie-archdaemon/odysseus/pull/1314 . Felix-active.
- Their advice (paraphrase): adds 8 new `.github/` workflows, each scanner is its own workflow with explicit blocking-vs-advisory classification, so the security gate can be required *incrementally* (start advisory, ratchet to blocking per-scanner) rather than all-or-nothing. Consolidates 6 prior per-scanner PRs into one reviewable change. Nothing existing modified.
- Our substrate state: VibeSwap CI status unknown from my context — known to use Foundry tests + Vercel deploy for the frontend. No explicit security-scanning baseline visible in CLAUDE.md. The repo has Solidity contracts + a Python oracle + React frontend, each with different scanner needs (slither for Solidity, bandit/pip-audit for Python, npm audit / Trivy for FE).
- Suggested action: audit `vibeswap/.github/workflows/` to see what scanners exist; if absent, adopt the same advisory-first-then-blocking pattern. Specifically: slither (Solidity), bandit + pip-audit (Python oracle), npm audit + Trivy filesystem (FE).
- Will-triage: pending

## [2026-06-09 15:09 ET] — Pain-points-first audit before structural rewrites

- Source: Issue #605 comment by @hinode-codes. https://github.com/pewdiepie-archdaemon/odysseus/issues/605
- Their advice (paraphrase): pushing back on "rewrite everything in React" with a list of concrete pain points to solve FIRST: dev-server hot reload (currently full rebuild on every change), established project structure for separation of concerns + tooling discipline (pnpm, biome), routing. Principle: identify the actual operational pain before committing to a structural rewrite that might not address it.
- Our substrate state: VibeSwap-FE is React + Vite + Tailwind. Vite already handles dev-server HMR, so hinode-codes' specific React-critique does not apply directly. BUT the meta-principle (audit current pain points before structural rewrite) IS relevant: VibeSwap has a backlog of refactor temptations (state-management consolidation, component library migration, design-token unification). Each should pass a "what concrete operational pain does this solve" test before going on the roadmap.
- Suggested action: before any VibeSwap-FE structural change leaves the discussion phase, write a one-paragraph "current pain that triggered this" alongside the proposed change. If the pain is not articulable in plain terms, defer the change. Compose with [P·full-leverage-only-moves] — wait until a real pain is total, not partial.
- Will-triage: pending
