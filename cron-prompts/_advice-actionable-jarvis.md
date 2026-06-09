# Advice actionable — JARVIS-OS (hooks, memory, cron, scripts)

Populated by Odysseus cron loops § COMMANDMENT 2.5 per [F·odysseus-as-advisory-substrate].

JARVIS substrate = Python hooks under `~/.claude/hooks/`, file-based memory under `~/.claude/projects/C--Users-Will/memory/`, cron-prompt logic under `~/.claude/cron-prompts/`, scripts under `~/.claude/scripts/`. Odysseus advice that applies to similar self-hosted Python/agentic substrate goes here.

Format same as `_advice-actionable-vibeswap.md`.

---

## [2026-06-09 13:48 ET] — Hybrid retrieval + importance + decay; reject always-inject

- Source: PR #720 by @dustinm16 "memory: add importance scoring, retrieval boost, decay, and observation API" — https://github.com/pewdiepie-archdaemon/odysseus/pull/720 . Felix-active.
- Their advice (paraphrase): no always-inject / hot-tier force injection of any memory. Every memory passes through a hybrid relevance gate. Scoring formula: `0.50*vector_sim + 0.35*keyword + 0.05*recency + 0.10*importance` where `importance` is a 0.0-1.0 explicit field per memory. Decay over time. Separate observation API for write-side discipline.
- Our substrate state: JARVIS memory has `MEMORY.md` ALWAYS-injected at boot (~24KB cap), with sub-indexes loaded situationally. No per-primitive importance field. No decay. No hybrid scoring — sub-index selection is rule-based (situation matching), not relevance-weighted. This is the *opposite* of the PR #720 design — we lean hard into the always-inject pattern that #720 calls out as wrong.
- Suggested action: evaluate whether MEMORY.md's PRE-FLIGHT set is *all* genuinely fail-closed (rules that must fire before anything else) vs. some entries that drifted into PRE-FLIGHT by accretion. PRE-FLIGHT items that can be relevance-gated should move to a scored tier. Compose with [F·memory-bi-temporal-axis] candidate (queued from #2858 dispatch) — decay + bi-temporal supersession + importance scoring are the same primitive family.
- Will-triage: pending

## [2026-06-09 13:48 ET] — Three-lane separation: issues vs ADR vs specs

- Source: #605 "Proposal: Architecture & Codebase Structure v3" — @RaresKeY comment: https://github.com/pewdiepie-archdaemon/odysseus/issues/605 . Felix-active thread.
- Their advice (paraphrase): keep three lanes separate. (i) Issues/discussions = "should this exist?" proposals. (ii) Mini-ADRs = accepted intent + tradeoffs + decisions, captured in PR bodies or a dedicated decision-record folder. (iii) `specs/` = current implementation truth — what the code does now, contracts, security, data-shape rules future PRs must preserve.
- Our substrate state: JARVIS memory has primitives (rules) and projects (state) and feedback (corrections) but no explicit "this is current implementation truth" vs "this is accepted but unimplemented intent" vs "this is a proposal we may or may not accept" separation. Primitives in `memory/` mix all three. The `_primitives-pending.md` queue is informally the "proposal" lane but it's not load-bearing.
- Suggested action: introduce explicit lifecycle states on memory primitives — proposed (in `_primitives-pending.md`), accepted (in `memory/` with `status: accepted`), implemented (with `status: implemented` + cross-link to the hook/code that enforces it), superseded (preserved with link to successor). The existing primitives are already mostly in the "accepted" or "implemented" state but the distinction is implicit.
- Will-triage: pending

## [2026-06-09 13:52 ET] — Session-state mutability + cross-session leakage discipline

- Source: PR #267 by @Anxiety471 "fix: session context drifting — messages leaking between chats (#135)" — https://github.com/pewdiepie-archdaemon/odysseus/pull/267 . Felix-active.
- Their advice (paraphrase): two concrete root causes of cross-session leakage. (i) `Session.history` was a shared mutable list — every call to `get_session()` returned the same object and concurrent tasks appended to the same list. Fix: immutable copies via internal `_history` list, `add_message()` replaces `.history` with a fresh snapshot. (ii) Task scheduler overwrote `session_manager.sessions[session_id]` directly, discarding the in-memory Session and any unpersisted messages. Fix: `ensure_task_session()` checks the cache first.
- Our substrate state: JARVIS uses per-conversation shards (per `M·shard-per-conversation`) — each Claude conversation has its own shard. But many JARVIS hooks read+write SHARED files (`MEMORY.md`, `_primitives-pending.md`, campaign logs, cron state). When multiple cron loops fire concurrently (daily-cadence + discovery overlapping), the same shared-mutable-state hazard exists at the file level. We don't have a `_history` immutable-snapshot equivalent for shared logs.
- Suggested action: audit which JARVIS hooks/cron-prompts mutate shared files and whether concurrent fires can race. Specifically: `_primitives-pending.md`, `MEMORY.md` edits, `odysseus-discussion-campaign-log.md` (multiple loops append). Consider an append-only-with-tx pattern (write to a tmp + rename) for shared logs. Compose with [P·crash-resilient-memory-writes].
- Will-triage: pending

## [2026-06-09 14:48 ET] — Retrieval-boost-factor (no always-inject) — pivot in PR #720 review

- Source: PR #720 review thread, @dustinm16 + @pewdiepie-archdaemon. dustinm16's commit-pivot after Felix's review: https://github.com/pewdiepie-archdaemon/odysseus/pull/720
- Their advice (paraphrase): Felix flagged the always-inject "hot" memory tier as product-behavior-changing and held the PR for manual testing. dustinm16's response: "Hot-tier always-inject behavior — rethinking this. The current design overrides relevance-based filtering which is the wrong tradeoff. Planning to move importance to a retrieval boost factor only (stronger weight in the hybrid score) rather than a context injection guarantee. Users retain full control through the existing memory system."
- Our substrate state: JARVIS does always-inject (MEMORY.md PRE-FLIGHT set is loaded at every SessionStart, no relevance gate at all). The exact pattern dustinm16 just pivoted AWAY from. Our defense is that PRE-FLIGHT entries are the genuinely-fail-closed minority — but inspection of the actual PRE-FLIGHT list shows accretion has happened.
- Suggested action: re-audit MEMORY.md PRE-FLIGHT and demote anything that isn't truly fail-closed to a retrieval-boost-weighted entry that lives in a sub-index. The hybrid scoring formula from #720 (`0.50*vs + 0.35*kw + 0.05*recency + 0.10*importance`) is a serviceable starting weighting. Compose with the bi-temporal supersession candidate from #2858 to make the importance-decay axis honest.
- Will-triage: pending

## [2026-06-09 14:48 ET] — Prompt-behavior changes require explicit product gate

- Source: PR #720 review by @pewdiepie-archdaemon. Felix's principle, applied to dustinm16's PR.
- Their advice (paraphrase): "I would also want explicit product confirmation before always injecting 'hot' memories: even capped at 5, that changes prompt behavior." Translated principle: any change to the agent's prompt-behavior surface (what gets injected, when, at what weight) MUST pass an explicit product/owner gate, separate from code review. Code review checks correctness; product gate checks whether the behavior change is desired at all.
- Our substrate state: JARVIS has no explicit "prompt-behavior change" gate. Edits to MEMORY.md, the memory-preprocessor sub-index expansion, or any cron canonical that injects boot-context all silently change Claude's prompt at next session. Some of these changes are Will-approved; many are agent-side autonomous.
- Suggested action: distinguish "code/canonical change" from "prompt-behavior change" at the commit level. Latter type requires an explicit Will-approval gate, even under autonomous-mode posture (similar shape to [F·full-auto-public-action-gate] but applied at the substrate-prompt-surface level). Specifically: any MEMORY.md edit, any cron canonical edit that affects boot-injection, any hook that fires on SessionStart, gets queued for Will-approval rather than executed silently.
- Will-triage: pending

## [2026-06-09 13:52 ET] — MCP Streamable HTTP + per-server auth headers

- Source: PR #803 by @akapug "feat(mcp): Streamable HTTP transport + per-server auth headers" — https://github.com/pewdiepie-archdaemon/odysseus/pull/803 . Felix-active.
- Their advice (paraphrase): MCP managers that only support stdio + headerless SSE can't connect to authenticated remote MCP servers (GitHub, Linear, Sentry, Cloudflare). Adds `transport: "http"` (aliases `streamable-http`) via the MCP SDK `streamablehttp_client` with proper 3-tuple unpacking, plus per-server `headers` field for `Authorization: Bearer <token>`.
- Our substrate state: JARVIS uses Claude's MCP integrations (Gmail, Calendar, Spotify, Google Drive, Microsoft 365). The auth flow is handled by Claude's own server-side OAuth, not by us configuring an MCP client. The `streamablehttp_client` advice applies to *self-hosted* MCP servers — we don't currently run any. If/when JARVIS adopts a self-hosted MCP server for VibeSwap-specific tools (e.g., contract-query, oracle-status), this advice becomes load-bearing.
- Suggested action: file under "load when JARVIS adds self-hosted MCP servers"; do not action now. Note the 3-tuple unpacking gotcha for future implementers.
- Will-triage: pending (deferred — no current MCP server to apply to)
