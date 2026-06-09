# Odysseus advice contribution graph (live ledger)

Append-only attribution log driving the Shapley contribution-graph in [J·odysseus-mission-loop] Step 4. Every senior dev whose advice meaningfully changed the JARVIS substrate becomes a node, edge weight = advice impact, status flips from `pending` to `actioned` on Will-triage acceptance.

The null-player axiom protects against attribution-padding. The symmetry axiom protects against handle-bias. Negative-contribution entries (rejected advice / unproductive comments) are recorded for graph integrity — Shapley value treats them as zero-marginal-contribution but the rejection signal is itself an honest data point.

## Schema

| field | meaning |
|---|---|
| date | YYYY-MM-DD ET when entry was recorded |
| handle | GitHub handle of contributor |
| thread | issue/PR/discussion # |
| advice-shape | one-line summary |
| impact | substrate the advice maps to (vibeswap / jarvis / both / negative) |
| status | pending / actioned / rejected |
| receipts | commit hash or URL where action landed (if actioned) |

## Ledger

| date | handle | thread | advice-shape | impact | status | receipts |
|---|---|---|---|---|---|---|
| 2026-06-09 | @dustinm16 | PR #720 | importance-scoring + decay + retrieval-boost-only (vs always-inject) | jarvis | pending | queue: `_advice-actionable-jarvis.md` |
| 2026-06-09 | @pewdiepie-archdaemon | PR #720 review | prompt-behavior changes require explicit product gate | jarvis | pending | queue: `_advice-actionable-jarvis.md` |
| 2026-06-09 | @RaresKeY | Issue #605 | three-lane separation: issues / mini-ADR / specs | jarvis | pending | queue: `_advice-actionable-jarvis.md` |
| 2026-06-09 | @nopoz | PR #1314 | CI security-scanning baseline with blocking-vs-advisory split | vibeswap | pending | queue: `_advice-actionable-vibeswap.md` |
| 2026-06-09 | @Anxiety471 | PR #267 | session-state mutability + cross-session leakage discipline | jarvis | pending | queue: `_advice-actionable-jarvis.md` |
| 2026-06-09 | @akapug | PR #803 | MCP Streamable HTTP + per-server auth headers | jarvis | pending (deferred) | queue: `_advice-actionable-jarvis.md` |
| 2026-06-09 | (unidentified langIcons.js commenter) | static/js/langIcons.js review | AI-cosplay single-purpose bloat file shape | vibeswap | pending | queue: `_advice-actionable-vibeswap.md` |
| 2026-06-09 | @alvaroperricone | Discussion #2858 | bi-temporal supersession (event-time + transaction-time) | jarvis | pending | queue: `_primitives-pending.md` |
| 2026-06-09 | @vdmkenny | PR #3363 merge style-nit | inline code comments are why-only, not history | jarvis | actioned | `feedback_code-comment-why-only.md` 2026-06-08 |
| 2026-06-09 | @rutsty-rust | Discussion #3684 (cross-ref #3686) | drive-by snark about textwall length, "AI inflation algorithm" frame; no substantive critique | negative | rejected | WGlynn reply "that's not very productive" 2026-06-09T19:50Z |
