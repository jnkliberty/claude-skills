---
name: orient
description: 'Turn a rambling, session-opening voice/dictation braindump into a confirmed frame — Goals, Objectives, Not-today, Open questions — then STOP and wait for a one-word confirm before doing ANY work. Auto-invoke at the START of a session when the user opens with a multi-topic, dictated, stream-of-consciousness dump that sets up work (VoiceInk tells — lowercase starts, run-ons, filler like "so", "like", "uhh", "i wanna", "i keep meaning to", "basically", "i don''t know"). Also triggers on explicit "/orient <dump>" or "orient this". Mirrors intent back so the session never sprints on a misread. At the confirm step, offers to escalate any goal to the goalify skill or hand a workflow-shaped goal to the workflow-architect skill to build a multi-agent harness. Do NOT invoke for a single scoped request, a pasted log / spec / error / code, or a normal short question.'
---

# Orient: voice braindump → confirmed session frame → STOP

Julian dictates a session-opening braindump (VoiceInk). It's high-entropy: multiple topics, filler, run-ons, no clear ask. The failure mode this skill prevents: latching onto sentence three and sprinting on the wrong thing.

`orient` reads the dump, mirrors back what it thinks the **goals and objectives of the session** are, and **stops**. No work happens until Julian confirms. This is an alignment step, not an execution step.

It is the _light_ front end to heavier siblings — use the right one:

| Skill                | Input                  | What it does                                              | Endpoint                           |
| -------------------- | ---------------------- | --------------------------------------------------------- | ---------------------------------- |
| **orient**           | session-opening dump   | mirror goals/objectives, confirm before work              | aligned → work normally in-session |
| `goalify`            | a raw goal dump        | classify → structure into a locked mega-prompt            | auto-fires an autonomous goal-loop |
| `workflow-architect` | a workflow-shaped goal | interview → pick pattern → scaffold a multi-agent harness | autonomous workflow run            |
| `braindump`          | stream of thought      | classify domain, extract intel, file it                   | stored note in the vault           |

If you're tempted to start executing, you're in the wrong skill. orient ends at the confirm.

> **Protocol:** the parse → mirror → confirm logic is canonical in **`PROTOCOL.md`** (tool-agnostic, shared with the Codex sibling so the two can't drift). Read it and follow it. This file adds only the Claude-Code-specific behavior on top.

## When to invoke

**Auto (no typing required):**

- Julian opens a session/turn with a rambling, multi-topic, dictated dump that's clearly setting up work.
- Signals: lowercase starts, run-on sentences, filler/hedges ("so", "like", "uhh", "i wanna", "i keep meaning to", "basically", "i guess", "honestly", "i don't know"), several topics stitched with "and also / and then / oh and".

**Explicit:**

- `/orient <dump>` or "orient this" / "what are my goals here".

**Do NOT invoke:** see `PROTOCOL.md` § "When NOT to orient." Also: if a `UserPromptSubmit` nudge fires but the content is clearly not a work-setup dump, ignore the nudge and proceed.

## Claude Code addition — the `workflow <#>` leg

Per `PROTOCOL.md` §3, `workflow <#>` is a member of the Claude Code **base** confirm menu — rendered every time alongside `go` and `goalify <#>`, not appended after the fact. Codex drops it; Claude renders it because Claude is where the dynamic-workflows engine lives.

```
  workflow <#>  → build + run a multi-agent harness on goal #
```

- **`workflow <#>`** → Invoke the `workflow-architect` skill on goal #. It fits when the goal is workflow-shaped — many independent items, adversarial verification needed, an unknown amount of work, or competing approaches to judge. workflow-architect runs its own interview, picks the pattern, scaffolds the harness, and runs it. If the goal must also finish completely, it can route through `goalify` first for a locked autonomous-goal contract that becomes the harness's completion gate.
- **`grill <#>`** is the other Claude-only leg (per `PROTOCOL.md` §3/§4) — contextual, rendered only when the mirror flags a goal as high-stakes. Codex renders neither `workflow` nor `grill`.

Lazy rule (extends `PROTOCOL.md` § "Kept lazy"): only assess whether a goal is workflow-shaped **at escalation** — when Julian types `workflow <#>` — never during the base mirror.

## Examples

See `EXAMPLES.md` for worked few-shots in Julian's real dictation voice, including an anti-example (pasted log → do not orient).

## Changelog

- **2026-07-21** — Menu cleanup. Cut the always-shown confirm menu from 9 verbs to 3 — `go` / `goalify <#>` / `workflow <#>` — plus a first-class free-text line; `grill <#>` and `blindspot <#>` are now contextual-only, rendered only when the mirror flags the goal. Removed the dangling goal-loop push leg (it pointed at a command that never existed on either surface) and the `tasks` override verb (the auto-rendered Tasks tier stays). Deployment converted to symlinks into this vault master, ending the copy-sync drift class. Evidence — 82 menu renders: `go` ~20, `workflow` 2, `goalify` 1, all others 0; 60% of replies were free text. Canonical in `PROTOCOL.md`.
- **2026-07-16** — Added the `blindspot <#>` verb for a read-only finding-unknowns Ritual 1 sweep. Canonical in `PROTOCOL.md`; Codex inherits it through the shared file.
- **2026-06-04** — Built. Mirror-and-confirm base with a `goalify` escalation hatch at the confirm step. Paired with the `orient-detect.js` UserPromptSubmit hook (nudge, non-forcing) for hands-free auto-trigger.
- **2026-06-04** — Added `workflow <#>` escalation: hand a workflow-shaped goal to the `workflow-architect` skill to build and run a multi-agent harness, completing the orient → goalify → workflow-architect chain.
- **2026-06-05** — Extracted the parse / mirror / confirm protocol into tool-agnostic `PROTOCOL.md` (shared with the Codex sibling at `~/.codex/skills/orient/`); this file now carries only the Claude Code deltas — the auto-trigger and the `workflow <#>` leg.
- **2026-06-22** — Added a **Tasks tier** under each objective in the mirror: an atomic, verb-first checklist. Hybrid by design — tasks auto-render only under objectives that bundle 2+ actions; atomic objectives stay one-liners (no padding). Tasks are a _read_ of the work, not a contract — no dates / owners / criteria; that line stays with `goalify`. Also added an on-demand override verb (`tasks`) that forced a full task breakdown of one goal even where the auto-hybrid left it terse — this verb was later cut 2026-07-21 (the auto-tier stays). Canonical change in `PROTOCOL.md`; Codex adapter + `EXAMPLES.md` synced; stale vault-master `PROTOCOL.md` re-deployed in the same pass.
- **2026-07-06** — Fable handover hardening: PROTOCOL.md gained the **parse craft** block (ask vs musing verb test, repetition-outranks-position, decision-bearing asides, trailing deferrals), a **§1.5 pre-render self-test** (5 silent questions), a **mirror quality bar** (7-line pass/fail checklist replacing adjectives), and a **loop-shape** note (turn-based loop, confirm menu = stop condition, deliberately no judge model or caps). Canonical in PROTOCOL.md; Codex sibling inherits via the shared file.
