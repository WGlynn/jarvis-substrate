# Odysseus advice-mined rolling log

Class-(c) entries (generic-good-design-no-action) and brief notes from each C2.5 sweep. Class-(a)/(b) entries go to `_advice-actionable-vibeswap.md` / `_advice-actionable-jarvis.md`.

Format per row:
```
| date | thread | author | shape (1-line) | class |
```

---

| date | thread | author | shape | class |
|---|---|---|---|---|
| 2026-06-09 | PR #3683 | @max-freddyfire | multi-lingual intent regex coverage extension (Swedish/Norwegian/Danish/German/Spanish/French) | c-neutral |
| 2026-06-09 | Issue #3672 | @RaresEduard-Tudor | duplicate route handler is dead code (FastAPI matches first registration); class: dead-code/route-collision detection | c-neutral |
| 2026-06-09 | PR #3508 | @holden093 | generic OIDC SSO via authlib (.well-known discovery, JWT/JWKS verify); standards-based auth | c-neutral (deferred-to-multi-user-phase) |
| 2026-06-09 | PR #1122 | @RosenTomov | provider-specific behavior detection via native API (LM Studio doesn't accept stream_options); auto-detection over port-heuristic | c-neutral |
| 2026-06-09 | Issue #2475 | @glenn2223 | cross-platform unified launcher CLI (.sh + .ps1 with --launch/--update flags); install/launch UX | c-neutral (deferred-to-JARVIS-publication-phase) |
| 2026-06-09 | PR #3697 | @OdWar420 | dep migration discipline (duckduckgo-search → ddgs) with graceful fallback through prior package names; no-regress on existing installs | c-neutral |
| 2026-06-09 | PR #2104 | @RosenTomov | keyboard-driven command palette UI (double-tap Shift, fuzzy-search across windows/actions/settings, ARIA combobox semantics) | c-neutral |
| 2026-06-09 | PR #3424 | @hinode-codes | UI dropdown state-management fix (group selection recreation/repopulation) | c-neutral |
| 2026-06-09 | PR #3384 | @wwardaww | skills file upload + rename feature (POST /upload, PUT /rename); standard CRUD on uploaded artifacts | c-neutral |
| 2026-06-09 | PR #3549 | @kydno | provider API integration fix (Kimi Code 403 + reasoning_content loss in multi-turn tool-calling) | c-neutral |
| 2026-06-09 | PR #3689 | @Cookiejunky | NVIDIA CUDA Docker path for llama.cpp serving (containerized GPU tooling vs host-dep) | c-neutral |
| 2026-06-09 | PR #3647 | @Cookiejunky | Serve panel restore — shared server-profile resolver injection (DI pattern fix) | c-neutral |
| 2026-06-09 | Issue #3670 | @RaresEduard-Tudor | defensive-DOM-insertion bug (banner inserted-before non-existent element); class: null-check on DOM-anchor before insertBefore | c-neutral |
| 2026-06-09 | Issue #2918 | @glenn2223 | AMD GPU acceleration via HIP (RDNA3+) and Vulkan (RDNA2); platform-specific build path | c-neutral |
| 2026-06-09 | PR #3661 | @TimHoogervorst | UI feature: import from library directly into chat | c-neutral |
