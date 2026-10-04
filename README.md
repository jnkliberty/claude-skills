# gtm-run-skills

A small public shelf of the skills I run, for any agent that reads skill files: Claude Code, Codex, and others. These pieces proved useful enough to hand to someone else.

## The shelf

| Skill | What it does |
| --- | --- |
| [`orient`](./orient) | Turns a session-opening braindump into a confirmed frame before any work starts |
| [`linkedin-intelligence`](./linkedin-intelligence) | Hook formulas, timing, and format rules from an analysis of 62,130 viral posts (credit: David Arnoux, viralbrain.ai) |
| [`radical-candor`](./radical-candor) | A simplicity and candor audit for a project, feature, architecture, or strategy |
| [`gtm-engineer`](./gtm-engineer) | Composes the marketing skills into one recurring client system: input an outcome, output a routed job spec and the skills that run each step |

Every folder has a `SKILL.md` that your agent loads on its own once the folder sits in its skills folder. Some carry a `references/` folder the skill reads when it runs. Nothing here depends on anything outside its own folder.

## Install

Clone the repo, then copy a skill folder into your agent's skills folder:

- **Claude Code:** `~/.claude/skills/` ([docs](https://code.claude.com/docs/en/skills))
- **Codex:** `~/.agents/skills/` ([docs](https://developers.openai.com/codex/skills))
- **Any other agent:** point the agent at the folder's `SKILL.md`.

For example, to install `orient`:

```bash
git clone https://github.com/jnkliberty/gtm-run-skills

# Claude Code
mkdir -p ~/.claude/skills && cp -r gtm-run-skills/orient ~/.claude/skills/

# Codex
mkdir -p ~/.agents/skills && cp -r gtm-run-skills/orient ~/.agents/skills/
```

## GTM brain

The [GTM brain](https://github.com/jnkliberty/gtm-brain) is a separate MIT starter for shared marketing and sales records. It includes `account-handoff` and nine CRM skills, plus the account, signal, rules, and sample CSV files those skills read. Follow its five-minute walkthrough to run the fictional Northwind Robotics example. Keep the brain files with the skills; copying a skill folder alone leaves out its inputs.

## Skills from other authors

I also run skills other people wrote. Get them from their authors:

- `cold-email` and `lead-magnets`: Corey Haines, [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills)
- `signal-interpreter`: Din Arbel, in Swan's [swan-gtm/gtm-skills](https://github.com/swan-gtm/gtm-skills)
- `stop-slop`: Hardik Pandya, [hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop)
- `harden`: part of Paul Bakaus's [Impeccable](https://github.com/pbakaus/impeccable)

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

`grill <#>` appears only when the mirror flags a goal as high-stakes. `blindspot <#>` appears only when it flags unfamiliar territory. `workflow` and `grill` are Claude Code legs; other agents leave them out of the menu.

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
| `SKILL.md`    | The skill your agent loads: when to fire, plus an optional Claude Code section |
| `PROTOCOL.md` | The parse → mirror → confirm logic, tool-agnostic (Codex reads it too)  |
| `EXAMPLES.md` | Worked few-shots in real dictation voice, including an anti-example     |

### Install and trigger it

Copy the `orient` folder into your agent's skills folder (steps in [Install](#install)).

Trigger it by dictating a messy multi-topic braindump at the start of a session. To call it by name, type `/orient <your dump>` in Claude Code or `$orient <your dump>` in Codex.

### One caveat

`orient` is the front door to my larger setup. The escalation verbs (`goalify`, `workflow`, and the contextual `grill` / `blindspot`) route to sibling skills (`goalify`, `workflow-architect`, `grill-me-codex`, `finding-unknowns`) that live only in my setup. `orient` works on its own: the mirror, the parse rules, and the confirm gate need nothing else. Treat the escalation verbs as a list of where a goal could route, and build your own back ends, or use only the mirror-and-confirm.

In Claude Code, my setup also pairs `orient` with a `UserPromptSubmit` nudge hook, `orient-detect.js`, for more reliable auto-triggering. The hook is a Claude Code feature and lives outside this repo. Without it, an agent still fires `orient` from description matching, just less reliably.

---

## License

MIT. Take it, fork it, bend it to your own voice. See [LICENSE](./LICENSE).
