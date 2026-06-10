# SKILL MINING — actionable queue (Will-triage)

Entries appended by skill-mining sweeps (`skill-mining.md`). Promote → work only on Will's go.
Public mirror — partner-specific references scrubbed per the loop's scrub-list.

## [2026-06-10 17:25 ET] — LLMLingua-2 lossy token-drop compression for prose-heavy boot/warm files
- Source: https://github.com/microsoft/LLMLingua (MIT, active, fetched + verified)
- Technique: XLM-RoBERTa token classifier drops low-value tokens; `PromptCompressor(...).compress_prompt(text, rate=0.33)`; 2-5x compression typical in production, task-agnostic
- Port class: REINTERPRET — complements HIERO, doesn't replace it. HIERO = semantic density at write-time; LLMLingua-2 = mechanical token-drop at load-time for files HIERO doesn't govern (warm memory prose, archived session-state epochs, paper drafts fed as context)
- Our substrate state: L4 corpus-cache reports 9,293 tok across 9 boot files; warm files load on situation-match uncompressed
- Suggested action: zero-risk benchmark on scratch copies of 2-3 warm files — measure tok-reduction vs recall fidelity; CPU inference is batch-offline (cron), latency irrelevant
- Will-triage: pending

## [2026-06-10 17:25 ET] — Graphiti bi-temporal fact-invalidation pattern for memory staleness
- Source: https://github.com/getzep/graphiti (Apache-2.0, v0.29.2 June 2026, 24k stars, fetched + verified)
- Technique: every fact carries a validity window; new contradicting info INVALIDATES (not deletes) old facts; queries answer "true now" vs "true at time T"; provenance links to source episodes
- Port class: full stack = DROP (needs Neo4j/FalkorDB + LLM-API ingestion — server infra we reject for local substrate). The bi-temporal PATTERN = REINTERPRET: `valid_from:` / `invalidated_by: <memory-slug>` frontmatter on memory primitives; staleness reminders become structural instead of age-heuristic
- Our substrate state: every memory read injects age-warnings ("X days old, verify before asserting"); the Hindsight CLI has 80 contradiction candidates pending — fact-invalidation is exactly the resolution mechanic for that queue. Converges with an active external research thread on bi-temporal KGs
- Suggested action: pilot `invalidated_by` frontmatter on the 80 Hindsight contradiction pairs during their triage; cite Graphiti as prior art where the bi-temporal discussion continues
- Will-triage: pending

## [2026-06-10 17:25 ET] — Letta "sleep-time compute" — background memory consolidation (convergent validation)
- Source: Letta (ex-MemGPT, 21.7k stars) via 2026 comparison roundups (search-level verification; fetch repo before acting)
- Technique: agent consolidates/merges/decays memories in background compute, not in-conversation; highest independent LoCoMo score (~83%) among open-source memory systems
- Port class: REINTERPRET — we already do this shape (cron-driven consolidation proposals, duplicate detector, dormancy review). Find = naming + validation + one gap: our consolidation surfaces PROPOSALS but nothing executes merge passes on a schedule
- Our substrate state: 6 consolidation proposals + 7 STRONG-sibling duplicate pairs sitting unmerged at `_system/`
- Suggested action: wire a weekly "sleep-time" cron that executes approved consolidation proposals (post-approval), rather than letting proposal queues accumulate
- Will-triage: pending

## [2026-06-10 17:25 ET] — Claude Code ecosystem deep-dive deferred (raw-README fetch needed)
- Source: https://github.com/hesreallyhim/awesome-claude-code (46.1k stars) + https://github.com/disler/claude-code-hooks-mastery (3.3k stars)
- Technique: canonical curated list (hooks/skills/orchestrators, judgment-curated) + hooks-mastery reference (UV single-file hook scripts, meta-agent patterns)
- Port class: vein, not a single find. GitHub HTML fetch returned nav-only; need raw.githubusercontent.com README fetch
- Suggested action: next sweep: fetch raw READMEs, mine for memory/token/session/frontend hooks we haven't independently built; expect high overlap with our stack — the delta is the value
- Will-triage: pending

## [2026-06-10 17:25 ET] — FRONTEND: Tailwind dynamic-class purge footgun + cn-helper convention
- Source: 2026 React/Tailwind best-practice roundups (search-level; low-risk convention, no fetch needed)
- Technique: `'bg-' + color + '-500'` template-string classes are invisible to Tailwind's scanner → purged in production builds. Convention: always complete literal class strings; conditional composition via `cn` helper (clsx + tailwind-merge)
- Port class: DIRECT-PORT — coding convention for the VibeSwap frontend
- Our substrate state: frontend aesthetic spec locks palette/tokens but has no dynamic-class rule; unaudited risk in existing components
- Suggested action: grep frontend/src for template-string class construction; add the rule to the locked aesthetic block
- Will-triage: pending

## [2026-06-10 17:25 ET] — FRONTEND: framer-motion is now "Motion" (package consolidation) + Vite 8 / Tailwind v4 upgrade horizon
- Source: 2026 animation-library + stack roundups (search-level; fetch changelogs before acting)
- Technique: framer-motion rebranded/merged → `motion` (Motion One merged in, ~6M weekly downloads, still the React default); Vite is at v8 (we run 5); Tailwind v4 (Jan 2025) drops tailwind.config.js for `@tailwindcss/vite` plugin; React Transition Group unmaintained (we don't use it)
- Port class: REINTERPRET — staged upgrade path, not urgent. Aesthetic is locked; libraries beneath it can move
- Our substrate state: frontend on React 18 + Vite 5 + framer-motion; deployed on Vercel; no CI on frontend
- Suggested action: low-priority upgrade spike branch (motion rename first — mechanical; Vite 5→8 + Tailwind v4 together — needs the ship-web checklist after)
- Will-triage: pending
## [2026-06-10 17:55 ET] — Will-fed absorb: "Designing loops with Fable 5" + loop-engineering taxonomy threads
- Source: 3 threads Will-pasted (Anthropic-staff Fable-5 loops thread; "beautiful broken refactor" meme; "Loops: What Every AI Engineer Needs to Know in 2026")
- Technique: verifier-subagent in independent context > same-context self-critique; memory progression fail→investigate→verify→distill→consult; closed-loop default w/ 5-part checklist (goal/context/action/feedback/stop-condition); structural-bets only WITH verification loop
- Port class: absorbed → memory primitive `feedback_design-loops-not-prompts.md` (shipped). Two follow-on actions remain:
  1. /critical-qa upgrade: route grading through a verifier subagent (independent context) instead of same-context hostile Q&A
  2. Loop-audit: run the 5-part checklist over all active loops (odysseus, skill-mining, autonomous-continue, WORK chain) — verify each has explicit goal + feedback + stop-condition
- Our substrate state: RSAW already does maker≠checker; "surfaced xN, unactioned" anticipation telemetry = measurable consult-step failure
- Will-triage: pending
