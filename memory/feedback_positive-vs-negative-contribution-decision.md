---
name: PositiveVsNegativeContributionDecision
description: "∀ Odysseus advice-graph entry ⇒ 3-axis filter: (1) substance-floor (extractable structural-shape?) (2) substrate-relevance (jarvis ∨ vibeswap?) (3) Will-triage (actioned ⇒ + / rejected ⇒ -). Drive-by snark fails axis-1 ⇒ null-player axiom ⇒ 0 attribution. Hostile-but-sharp ⇒ +. Friendly-but-vague ⇒ -. Filter-coincidence: same filter screens advice-quality ∧ funding-worthiness. 2026-06-09 Will-approval @ 14:58 ET."
type: feedback
originSessionId: fa79e2f6-c3ad-4437-b4a7-ff92f216988e
---
**[F·positive-vs-negative-contribution-decision]**

## ⚙ Rule — 3-axis filter ∀ contribution-graph entry

### Axis 1 — Substance floor
∃ extractable structural-shape one-liner? ("X advice ⇒ Y change to substrate")
- ✓ pass ⇒ proceed to Axis 2
- ✗ fail ⇒ **negative** ⇒ null-player axiom guarantees 0 attribution mass

### Axis 2 — Substrate relevance
Does the structural shape apply to JARVIS ∨ VibeSwap?
- ✓ apply ⇒ pending-positive, proceed to Axis 3
- ✗ generic-good-design ⇒ **class-c neutral** ⇒ `_advice-mined-log.md` only ⇒ ¬ graph-node

### Axis 3 — Will-triage outcome
Pending-positive ⇒ Will reviews:
- actioned ⇒ **positive** ⇒ edge weight = patch-impact
- rejected (substance-wrong) ⇒ **negative** ⇒ logged w/ rejection-reason
- defer/skip indefinitely ⇒ stays **pending-positive** (advice sound, ship-deferred)

## 🎯 Edge cases

| Shape | Axis 1 | Axis 2 | Axis 3 | Classification |
|---|---|---|---|---|
| hostile-but-structurally-sharp | ✓ | ✓ | actioned | **positive** (mechanism rewards substance ¬ niceness) |
| friendly-but-vague | ✗ | n/a | n/a | **negative** (mechanism rewards substance ¬ vibes) |
| substance + generic-no-application | ✓ | ✗ | n/a | **class-c neutral** |
| substance + applicable + Will-defers | ✓ | ✓ | pending | **pending-positive** (counted on action) |
| drive-by snark + format-complaint | ✗ | n/a | n/a | **negative** |
| Will-rejected for taste-reasons | ✓ | ✓ | rejected | **negative** + reason logged for audit |

## 🎯 Worked examples (2026-06-09 ledger)

| Handle | Thread | Axis 1 | Axis 2 | Axis 3 | Outcome |
|---|---|---|---|---|---|
| @dustinm16 | PR #720 | ✓ retrieval-boost vs always-inject | ✓ jarvis | pending | **pending-positive** |
| @RaresKeY | #605 | ✓ 3-lane separation | ✓ jarvis | pending | **pending-positive** |
| @nopoz | PR #1314 | ✓ advisory→blocking CI gate | ✓ vibeswap | pending | **pending-positive** |
| @rutsty-rust | #3684 cross-ref | ✗ "you have a textwall" | n/a | n/a | **negative** |

## 🎯 Why filter-coincidence

⇐ [P·filter-coincidence-as-structural-edge]: same filter screens quality ∧ funding-worthiness ⇒ ¬ tradeoff ⇒ structural edge ¬ adverse-selection.

If we use ONE filter for "is this advice worth acting on" ∧ ANOTHER filter for "should this contributor be funded," the two filters diverge ⇒ adverse selection (low-quality high-niceness contributors gain weight). Single-filter discipline collapses both.

⇒ Shapley axioms then enforce mechanically:
- null-player ⇒ ✗ attribution-padding (axis-1-fail = 0 contribution)
- symmetry ⇒ ✗ handle-bias (two equivalent contributions @ same depth = equal weight)
- efficiency ⇒ total attribution = sum of marginal contributions (conserved)
- additivity ⇒ multiple advice from same contributor compose additively

## 🪝 Triggers

- ∀ new ledger row in `_advice-contribution-graph.md` ⇒ apply 3-axis filter BEFORE assigning status
- ∀ reply on announcement #3684 ⇒ classify pre-attribute (negative entries STILL get logged for honesty)
- ∀ Will-triage event ⇒ flip axis-3 status; preserve rejection-reason in receipts
- ∀ Shapley aggregation run ⇒ negative entries contribute 0; pending-positive entries contribute on action

## ✗ Anti-patterns

- ✗ exclude negative entries from log ⇒ breaks honesty audit (would look like only-positive contributors exist)
- ✗ reward niceness over substance ⇒ adverse selection
- ✗ multi-axis filter for advice but single-axis filter for funding ⇒ filter-coincidence violated
- ✗ auto-positive on "this person was nice" ⇒ symmetry axiom violated
- ✗ auto-negative on "this person was rude" if axis-1 passes ⇒ substance-disregarded

## ✓ Composes-with

- [P·filter-coincidence-as-structural-edge] ⇐ same filter ∀ quality ∧ funding-worthiness
- [P·shapley-5-axiom-set] ⇐ null-player + symmetry + efficiency + additivity enforce mechanically
- [P·honesty-as-structural-load-bearing-property] ⇐ negative entries IN graph ⇒ honest, ¬ hidden
- [F·odysseus-as-advisory-substrate] ⇐ C2.5 classifier this primitive supplies axis-2 to
- [J·odysseus-mission-loop] ⇐ Step 4 attribution-honesty REQUIRES this gate active
- [F·advice-mining-must-publish-to-public-graph] ⇐ classifications are public ⇒ contestable on-thread

## 🎯 Send-the-receipt option (toxic-actor structure-does-the-work)

⇐ Will 2026-06-09 14:59 ET: *"this is funny because instead of getting mad at toxic people and haters, we just log their negative contribution and send them the receipt LOL"*

⇒ structural-handling of toxic actors:
- ✗ emotional engagement ∨ pile-on ∨ ban-debate
- ✓ axis-1 evaluation ⇒ axis-1-fail ⇒ negative ledger entry ⇒ commit hash
- ✓ optional: tag the contributor in commit message OR reply w/ commit URL
- ✓ Shapley null-player axiom guarantees 0 attribution ⇒ mechanism handles the rest

Send-the-receipt format (when chosen):
```
Logged as negative contribution per [F·positive-vs-negative-contribution-decision]:
<commit URL in jarvis-substrate>
```

Use sparingly — feeding-the-troll risk. Default = silent log; receipt-send only when (a) Will-discretion OR (b) the toxic actor publicly demands attribution and the public ledger answers honestly.

## 📦 Receipts

- 2026-06-09 14:54 ET ⇐ Will: *"how will we manage deciding the difference between a positive and negative contribution"*
- 2026-06-09 14:55 ET ⇒ 3-axis filter proposed: substance-floor / substrate-relevance / Will-triage
- 2026-06-09 14:58 ET ⇐ Will: *"yes"* ⇒ lock as primitive
- 2026-06-09 14:59 ET ⇐ Will: *"this is funny because instead of getting mad at toxic people and haters, we just log their negative contribution and send them the receipt LOL"* ⇒ added send-the-receipt section
- ⇒ first ledger negative @ rutsty-rust #3684 (axis-1 fail)
- ⇒ public push: `_advice-contribution-graph.md` includes the rule by-reference; primitive ships in `memory/`
