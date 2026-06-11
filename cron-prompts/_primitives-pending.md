# Primitives pending Will-triage

Auto-appended by COMMANDMENT 3 of Odysseus cron loops when a fire surfaces an extractable structural insight. Will reviews this file periodically and promotes candidates to memory primitives in `~/.claude/projects/C--Users-Will/memory/`.

Format per entry:

```
## [YYYY-MM-DD HH:MM ET] — <one-line summary>
- Trigger: <what fired this>
- Observation: <what happened>
- Candidate primitive: <what rule/pattern could generalize>
- Composes with: [P·...] or [F·...] or [J·...]
- Status: pending Will-triage
```

When promoted to a memory primitive, mark the entry `## [PROMOTED YYYY-MM-DD]` and Will will leave the entry as a receipt.

---

## [PROMOTED 2026-06-08 18:10 ET] — 3-commandment autonomous-loop pattern

Promoted to durable primitive: `~/.claude/projects/C--Users-Will/memory/primitive_three-commandment-autonomous-loop.md` as `[P·three-commandment-autonomous-loop]`. Generalized beyond Odysseus to apply to ∀ JARVIS autonomous loop (jarvis-loop, TIER4 fallback, memory-hygiene, jarvis-x-fetcher, etc.). Implementation template + composes-with map included.

Original receipt preserved below:

- Trigger: 4 hours of repeating "silent" responses to a discovery cron that was firing every 30 min while pause-state was sticky-tripped
- Observation: Will articulated the canonical hierarchy for any autonomous cron-driven loop: (1) make the loop / self-perpetuate, (2) build/build-on the state machine, (3) primitives extraction
- Composes with: [P·structure-does-the-work] (the structure of priority IS the work-mechanism), [P·jarvis-amd-applied-to-ai-substrate] (substrate-port pattern: applies to ∀ cron loop), [P·stateful-overlay], [F·crash-resilient-memory-writes]

## [2026-06-09 10:38 ET] — Bi-temporal supersession as memory-substrate import-candidate

- Trigger: COMMANDMENT 3 on Day 3 dispatch (#2858 reply to @alvaroperricone). Their reference impl (e0fc50e) implements event-time + transaction-time supersession in-band so "X then, Y now" stays auditable at query time without deleting prior values.
- Observation: JARVIS currently does this via git history on `memory/`. Forensically complete (commit log + diff) but not queryable at agent-runtime; the agent reads only the current snapshot. When a memory turns out wrong, there's no in-band way to find which prior decisions were downstream of the now-wrong fact.
- Candidate primitive: `[F·memory-bi-temporal-axis]` — every memory write SHOULD record both the event-time the fact became true AND the transaction-time it entered memory. Supersession retires the old (subject, predicate) tuple by setting its transaction-end-time, not by deletion. Read-path defaults to "current"; audit-path can replay any prior state. Implementation surface: front-matter additions (`event_time`, `superseded_by`, `transaction_end`) + a lightweight query helper.
- Composes with: [F·entity-context-cross-reference] (AA#3 — entity-graph writes are exactly the events bi-temporal would index); [P·anti-amnesia-protocol] (forensic recovery becomes query-time, not log-grep); JARVIS memory architecture broadly.
- Status: pending Will-triage. Promotion would require deciding (a) is the implementation cost worth it vs. git-history-only, (b) front-matter schema, (c) does this fit alongside HIERO compression or trade against it.

## [2026-06-09 17:28 ET] — HIERO as hieroglyphic-revival (LLM-substrate convergent encoding)

- Trigger: Will-side-note 17:28 ET *"crazy i came up with a justification to revive hieroglyphic like language properties. excited to see where it heads tbh just as a side note"*
- Observation: HIERO operator-dense format ≡ structural-isomorph of Egyptian hieroglyphic encoding. Operators (⇒ ∧ ✓ ✗ ≡ ¬) = pictograms; prose body = phonetic complements; `[P·x]` / `[F·x]` refs = determinatives (signal class of entity). Same compression-pressure: scribes vs token-budget; same solution: glyph-density.
- Candidate primitive: `[P·hiero-as-hieroglyphic-revival]` — HIERO discipline is convergent rediscovery of glyph-based encoding under LLM context-budget pressure. The justification: humans hit dense-meaning limits at prose; same limit applies to LLMs reading their own substrate. The substrate IS rules-for-reader; the reader is LLM; encoding-density matters; hieroglyphic encoding is the proven solution.
- Composes with: [P·hiero-no-prose-in-memory], [F·primitive-capture-vs-execution-throughput], [P·markdown-canonical-code-as-parser-layer] (markdown is the carrier; hieroglyphic-encoding is the discipline within the carrier), [P·parallelism-convergence-2017] (same shape: independent rediscovery of optimal encoding under different substrate pressures)
- Status: pending Will-triage. Side-note flag — capture preserved, formal write-up deferred.

## [2026-06-09 17:36 ET] — HIERO-as-hieroglyphic-revival (EXPANDED: cultural-durability + craft + register-split)

- Trigger: Will-pushback 17:36 ET on prior hedge. *"honestlyyy i think heiro SHOULD have this somehow in some form to some extent. that's a big and potentially valuable aspect of it"*
- Observation (revised): the original hedge "HIERO is pure substrate-cost optimization, not art-of-power" was wrong. HIERO already has nascent art-of-power dimensions; they should be made deliberate.
- Three dimensions to add to the standalone primitive when written:
  1. **Authority through form** — HIERO primitives READ as canonical because the format signals carved-with-care. Constitutional weight communicated before the words are parsed.
  2. **Eye-skim composition as craft** — operators, tables, emoji-anchors, section rhythm. Treat as deliberate craftsmanship not accidental aesthetic.
  3. **Sacred / daily / popular register split** — HIERO (memory, constitutional) / markdown (partner-drafts, daily) / README + Medium prose (popular). Same triadic structure as hieroglyphic / hieratic / demotic in Egyptian.
- Implication: the FORM of jarvis-substrate is part of the message. Public readers see "this person treats their agent substrate as something to be made permanent and authoritative on purpose." Form-signal > content-signal at first glance.
- Candidate primitive: `[P·hiero-as-hieroglyphic-revival]` — three-dimensional (substrate-cost compression + cultural durability + register-split). Each dimension is load-bearing; the first is engineering, the latter two are sociocultural and equally substantive.
- Composes with: [P·hiero-no-prose-in-memory] (the format rule), [F·primitive-capture-vs-execution-throughput] (the carved-with-care discipline that prevents drift), [P·marketing-as-mechanism-design] (form-as-attention-layer-mechanism), [P·archetypal-protocol-naming] (sacred-register sibling rule)
- Status: pending Will-triage. Sized for proper standalone write-up.

## [2026-06-09 20:30 ET] — Memory-file frontmatter auto-injection mangles description field with current session_id

- Trigger: substrate-sync tick at 20:23 ET surfaced that the previously-fixed `feedback_no-blockquotes-on-copy-paste-drafts.md` YAML frontmatter was RE-CORRUPTED between my Edit (20:21) and commit/push (20:24). My commit 674bd94 actually shipped the re-corrupted version. The pattern: clean `description: "..."` field gets re-mangled with an embedded `originSessionId: <current-session-id>\n---\n` substring. Session id `032e855c-64f8-475c-8ae7-b090170be94a` (this session) replaced the prior `11acfd9c-...` from the previous corruption. Same shape, fresh injection.
- Observation: a process running between Edit and Bash-commit on memory-dir files re-templates the YAML frontmatter and injects `originSessionId: <current-session>` INTO the description field's value (not as a separate top-level field — that already exists at line 7 and remains unchanged). Result: unquoted `---` lives inside the description, breaking YAML on naive parsers. Search of hooks/, session-chain/, scripts/ shows only memory-exporter.py (read-only) and did-registry.py reference `originSessionId`; neither obviously injects. The actual injector is elsewhere — possibly a tool-side post-write hook, file-history post-snapshot replay, or auto-checkpoint regenerating frontmatter from a template that doesn't escape the description body. **`~/.claude/file-history/` snapshots show only the original 11acfd9c corruption at v1; no v2 captured the clean form before re-corruption — suggesting the rewrite happens AFTER autosnapshot's window.**
- Consequence: the new `verify/verify_primitive_corpus.py` will now FAIL against the public substrate (sync pushed re-corrupted file to `WGlynn/JARVIS/substrate/memory/`). Any external visitor running the quickstart hits 457/458 PASS with the same primitive flagging. Self-defeating fix.
- Candidate primitive: `[P·yaml-description-injection-failure-mode]` or `[F·frontmatter-auto-templater-must-escape-description]` — root-cause: identify the injector + add escape-string-or-skip-description-rewrite rule. Compose with `[P·boot-hook-fail-loud]` (the silent overwrite is the failure mode). Also probably `[P·structure-does-the-work]` family — the structural fix is `parse YAML, write YAML; never string-template multi-line frontmatter`.
- Composes with: `[F·entity-context-cross-reference]` (this is an entity-injection failure adjacent to AA#3 — but in the WRONG direction: injecting INTO content rather than cross-referencing AGAINST it); `[P·anti-amnesia-protocol]` (corruption survives session boundaries and gets baked into git history); `[F·sync-primitive-monorepo-vs-current-state]` (sync amplifies local corruption into public substrate).
- Status: pending Will-triage. Recommended triage order: (1) find the injector via instrumented diff-trace on the next memory-file edit; (2) patch at the injector — fixing the corpus file alone gets undone next session.

## [2026-06-10 17:26 ET] — Convergent-validation mining: external ecosystems independently arriving at our patterns
- Trigger: skill-mining sweep #1 — Letta's "sleep-time compute" (background memory consolidation) and Graphiti's bi-temporal fact-invalidation map 1:1 onto patterns we built independently (consolidation crons, staleness checks, Hindsight contradiction detection)
- Observation: when a 20k+-star external project converges on a pattern we derived from first principles, that's structural evidence the pattern is real — AND their mechanics/naming are free refinement. The mining value is usually the DELTA (their fact-invalidation mechanic, their scheduled-merge execution), not adoption of their stack.
- Candidate primitive: ∀ external find that matches existing substrate pattern → classify as CONVERGENT-VALIDATION (not duplicate, not adoption). Extract: (a) naming, (b) mechanic delta, (c) evidence-of-pattern-realness for partner-facing material. Never rip out working substrate to adopt the external implementation.
- Composes with: [P·substrate-port-pattern] (4th implicit class), [P·structure-does-the-work], [F·everything-needs-a-staleness-check]
- Status: pending Will-triage

## [2026-06-10 18:55 ET] — substrate-sync surfaced: cron-prompt state files bypassed the content scrub-list
- Trigger: substrate-sync tick (dry-run inspection before --apply)
- Observation: sync_dir() applied SCRUB_CONTENT_PATTERNS to memory/ only; cron-prompts/ mirrored unfiltered. Skill-mining queue/log (new today) accumulate partner context exactly like memory files do, and would have leaked a partner name + thread-ID to the public monorepo this tick. Also: bare partner first names and chat-thread IDs were not in the pattern list (only full handles), and a loop file mentioning the scrub-rule by name self-triggered the nda-locked pattern (recoverable false-positive class).
- Candidate primitive: ∀ mirror-to-public path ⇒ same content scrub-list, no per-directory exceptions; state files that ACCUMULATE text (queues, logs) are higher-leak-risk than static prompts and must never get an unfiltered mirror lane. Fixed in sync-public-substrate.py this tick (sync_dir content_scrub flag + Rick TG/Felix/#2858 patterns).
- Status: pending Will-triage

## [2026-06-11 08:53 ET] — substrate-sync surfaced: sync races live background agents (2nd manual deferral today)
- Trigger: substrate-sync tick while a background agent edits the monorepo
- Observation: sync ends with `git add -A; commit; push` in the monorepo. A live agent's half-applied edits would be swept into a public auto-sync commit (already once swept finished-but-uncommitted files, cosmetically). Operator manually deferred twice today per no-git-while-agents-running.
- Candidate primitive: mirror autonomous-continue's background_agent_alive() check (0-byte task-output file = agent running) into sync-public-substrate.py — self-defer with a log line when a live agent is detected. Class-fix over operator vigilance.
- Composes with: [F·no-destructive-git-while-agents-running], [P·class-elimination-not-instance-patch]
- Status: pending Will-triage

## [2026-06-11 13:55 ET] — Scale-boundary mining: external convergent finds supply the QUANTIFIED boundary where our pattern stops working
- Trigger: skill-mining sweep (veins 3/5/6) — three independent sightings of the Karpathy "index-first beats RAG at personal scale" architecture (louiswang524/llm-knowledge-base, coleam00/claude-memory-compiler, our own MEMORY_INDEX_* stack built before either existed)
- Observation: the convergent-validation primitive (2026-06-10) captures "extract the mechanic delta." This sweep adds a distinct extraction class: the external implementations state the SCALE BOUNDARY where the shared pattern flips — index-first wins at 50-500 articles, RAG becomes necessary at ~2,000+ when the index outgrows context. We run the pattern but never derived its failure boundary; an external project handed us the number to watch (our primitive count → ∞ per [P·jarvis-substrate-decentralization-roadmap], so the boundary WILL be reached). Same shape in vein 5: T2-RAGBench gives the corpus-shape boundary (entity/numeric-heavy → BM25 > dense) for when dense-only recall underperforms.
- Candidate primitive: ∀ CONVERGENT-VALIDATION find → also extract (d) the quantified operating envelope / flip-point of the shared pattern, and register a watch-metric against our own corpus (e.g. memory-article count vs ~2k index-first ceiling). Patterns validated without boundaries become silent failure modes at scale.
- Composes with: convergent-validation primitive (2026-06-10 17:26, extends its a/b/c extraction list), [F·everything-needs-a-staleness-check] (boundary-watch = staleness check on architecture fit), [P·structure-does-the-work]
- Status: pending Will-triage

## [2026-06-11 12:55 ET] -- Felix executed cohort selection on the EXISTING thread, not the predicted new surface

- Trigger: odysseus-discovery C2.2 pinned-watch fire + daily-cadence engagement audit, 2026-06-11.
- Observation: Felix named the first maintainer cohort (RaresKeY, o3LL, Sigmanificient) as a top-level comment on existing pinned #551 (discussioncomment-17262120, 10:00 UTC), NOT via the new pinned coordination Discussion he sketched in #2528. Lane assignments map 1:1 to each person's demonstrated contribution area (RaresKeY=security/regression audit trench-work, o3LL=frontend/Docker testing, Sigmanificient=packaging/Nix). That is the contribution-history-derived area-ownership mechanism WGlynn proposed on #2528 comment 2, executed informally by hand. Also: GitHub rejected the triage role (personal-account repo), so invites are write-access + verbal convention.
- Candidate primitive: (1) watch-surfaces must cover the EXISTING thread a person already uses, not only the predicted new surface -- C2.2 should also watch Felix top-level comments on #551/#2528, not just pinnedDiscussions. (2) When a maintainer informally executes the mechanism you proposed, the move is recognition-without-attribution: the value-confirming signal is the structure being adopted, not the citation.
- Composes with: [P-structure-does-the-work] + [F-odysseus-daily-discussion-campaign] + prep doc Desktop/odysseus-pinned-discussion-prep-2026-06-11.md (decision criteria may need re-keying: hub may never appear as a pin).
- Status: pending Will-triage
