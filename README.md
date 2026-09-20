# claude-skills

A small public shelf of the [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills I run. These pieces proved useful enough to hand to someone else.

## The shelf

| Skill | What it does | Install |
| --- | --- | --- |
| [`orient`](./orient) | Turns a session-opening braindump into a confirmed frame before any work starts | `cp -r orient ~/.claude/skills/` |
| [`cold-email`](./cold-email) | B2B cold emails and follow-up sequences: subject lines, openers, CTAs, personalization, benchmarks | `cp -r cold-email ~/.claude/skills/` |
| [`lead-magnets`](./lead-magnets) | Plans a lead magnet from an audience and an offer, with format guide and conversion benchmarks | `cp -r lead-magnets ~/.claude/skills/` |
| [`signal-interpreter`](./signal-interpreter) | Reads a raw GTM signal (a hire, a funding round, a tech change) into relevance, strength, confidence, and what to say | `cp -r signal-interpreter ~/.claude/skills/` |
| [`linkedin-intelligence`](./linkedin-intelligence) | Hook formulas, timing, and format rules from an analysis of 62,130 viral posts (credit: David Arnoux, viralbrain.ai) | `cp -r linkedin-intelligence ~/.claude/skills/` |
| [`stop-slop`](./stop-slop) | Strips AI writing tells from prose: banned phrases, negation patterns, rhythm fixes | `cp -r stop-slop ~/.claude/skills/` |
| [`radical-candor`](./radical-candor) | A simplicity and candor audit for a project, feature, architecture, or strategy | `cp -r radical-candor ~/.claude/skills/` |
| [`harden`](./harden) | Makes an interface resilient: error states, text overflow, localization, edge cases | `cp -r harden ~/.claude/skills/` |
| [`gtm-engineer`](./gtm-engineer) | Composes the marketing skills into one recurring client system: input an outcome, output a routed job spec and the skills that run each step | `cp -r gtm-engineer ~/.claude/skills/` |

Every folder has a `SKILL.md` that Claude Code loads on its own once the folder sits in `~/.claude/skills/`. Some carry a `references/` folder the skill reads when it runs, and `cold-email` and `lead-magnets` ship an `evals/` file with test prompts. Nothing here depends on anything outside its own folder.

The long write-up below is for `orient`, the first skill on the shelf and the one with the most moving parts.

---

## orient

I start most sessions by talking, not typing. Voice-to-text, half-formed, six things at once.

> "ok so today i wanna get back into the dashboard, the attribution thing, and also i keep meaning to close out that flag, oh and at some point the invoice table but that's not really today honestly"

Left alone, the agent grabs sentence three and starts building. Wrong thing. Full speed.

`orient` catches the dump before work starts. It mirrors the goals, concrete steps, parked ideas, and open questions. Then it stops. Nothing runs until I say `go`.

That's the whole move. Reflect before you sprint.

It's an alignment step, not an execution step. It stops a confident agent from sprinting three files deep on a misread voice note.

```
Goals — this session
  1. Client marketing-metrics dashboard — finish the attribution view
  2. RLS flag — close it out

Objectives & tasks
  #1 finish the attribution view
     - wire the funnel chart to the live data
     - verify the attribution query returns correct numbers
  #2 set the RLS flag on accounts; confirm it sticks

Not today (heard it, parked it)
  - investor invoice table ("not really today")

Open questions (answer before I sprint)
  - #1: "half wired" — is the funnel chart rendering at all, or stubbed?

  go            → lock this frame, work normally from here
  goalify <#>   → structure goal # into a locked autonomous goal-loop
  workflow <#>  → hand goal # to a workflow architect (build + run a multi-agent harness)
  …or reply in plain words — corrections, "look again", "break goal N down"
```

The standing menu is a three-way router: `go` locks the frame, `goalify` structures one goal into an autonomous run, and `workflow` hands a workflow-shaped goal to a multi-agent process. Plain words are first-class too: corrections, "look again," and "break goal N down" work without special syntax. The cut came from 82 real menu renders; 60% of replies were free text.

`grill <#>` appears only when the mirror flags a goal as high-stakes. `blindspot <#>` appears only when it flags unfamiliar territory.

### What's actually inside

The mirror is the visible output. The parse rules behind it do the work, all specified in `PROTOCOL.md`:

- **The verb test.** Asks travel with commitment verbs ("i want", "can you", "let's"). Musings travel with "i wonder", "at some point", "it'd be cool if". A musing never becomes a goal; it parks in Not-today. Building a musing is the most expensive misread available.
- **Repetition outranks position.** The topic that comes back twice is the real priority, even phrased as an aside. The last thing dictated is merely the freshest thought, not the most important.
- **Quote, don't smooth.** "make the dashboard not suck" stays in quotes as an open question. Polishing it into "improve dashboard UX" hides the exact ambiguity that needed resolving.
- **A silent self-test before the mirror renders.** Five questions, including "which phrase carries the most unstated intent, and does it appear verbatim in the frame?" Any "no" forces a re-parse, never a render.
- **A pass/fail quality bar.** Seven checks: every sentence of the dump maps somewhere, three goals max, zero invented questions, any twice-mentioned topic surfaces explicitly, zero work before `go`.
- **Five probe lenses for real ambiguity.** Evidence, Specificity, Counterfactual, Attachment, Durability. They recognize open questions already present in the dump. Fabricating questions is banned; a clear dump gets "No open questions, confirm and go."
- **High-stakes goals get flagged unprompted.** A goal touching outbound sends, client data writes, pricing, or real money gets named as high-stakes in the mirror itself, with `grill` recommended before any build.

### What's in the folder

| File          | What it is                                                              |
| ------------- | ---------------------------------------------------------------------- |
| `SKILL.md`    | The skill Claude Code loads: when to fire, the Claude-specific bits    |
| `PROTOCOL.md` | The parse → mirror → confirm logic, tool-agnostic (Codex reads it too)  |
| `EXAMPLES.md` | Worked few-shots in real dictation voice, including an anti-example     |

### Install

Drop the folder into your skills directory:

```bash
cp -r orient ~/.claude/skills/orient
```

Claude Code auto-discovers it. Trigger it by dictating a messy multi-topic braindump at the start of a session, or type `/orient <your dump>`.

### One caveat

`orient` is the front door to my larger setup. The escalation verbs (`goalify`, `workflow`, and the contextual `grill` / `blindspot`) route to sibling skills (`goalify`, `workflow-architect`, `grill-me-codex`, `finding-unknowns`) that live only in my setup. `orient` works on its own: the mirror, the parse rules, and the confirm gate need nothing else. Treat the escalation verbs as a list of where a goal could route, and build your own back ends, or use only the mirror-and-confirm.

My setup also pairs `orient` with a `UserPromptSubmit` nudge hook, `orient-detect.js`, for more reliable auto-triggering. The hook lives outside this repo; Claude Code still auto-fires from description matching, just less reliably.

---

## License

MIT. Take it, fork it, bend it to your own voice. See [LICENSE](./LICENSE).
