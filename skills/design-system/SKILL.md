---
name: design-system
description: Design-discipline system for frontend/UI work — wireframes, prototypes, design-token extraction, accessibility/polish audits. Use when building or reviewing any UI, page, deck, or HTML artifact and the locked project aesthetic alone doesn't cover the task. Wraps Trystan-SA/claude-design-system-prompt (MIT, vendored 2026-06-10).
---

# Design System (vendored wrapper)

This wraps the reverse-engineered design system prompt at this directory's `system-prompt.md` plus 14 modular phase-skills under `skills/`.

## How to use
1. Read `system-prompt.md` (20-chapter design doctrine) — the 8 quality dimensions: content (no filler), aesthetics (reject AI tropes: gradients, emoji, rounded-card genericism), hierarchy, accessibility (WCAG/semantic/keyboard), interaction states, system-thinking (tokens over one-offs), medium respect (real CSS Grid, oklch()), polish (depth over breadth).
2. Match the request to a phase-skill in `skills/` (Production = wireframes/prototypes · System = design-token extraction · Review = accessibility/polish audit) and follow it.

## Precedence rule (JARVIS-local, load-bearing)
For VibeSwap frontend work, the LOCKED terminal-console aesthetic in `vibeswap/CLAUDE.md` (matrix-green #00ff41 on true black, JetBrains Mono labels, op-signature headers) OVERRIDES any aesthetic suggestion from this system. Use this skill's discipline dimensions (accessibility, hierarchy, states, no-filler) WITHIN the locked palette — never to replace it. Its anti-AI-trope chapter and the locked aesthetic agree; where they conflict, vibeswap/CLAUDE.md wins.

## Source
- Upstream: https://github.com/Trystan-SA/claude-design-system-prompt (MIT)
- Vendored: 2026-06-10, shallow clone. To update: `git -C ~/.claude/skills/design-system pull`.
