# claude-skills

A small public shelf of the [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills I run. These pieces proved useful enough to hand to someone else.

First one up: `orient`.

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
  fix <thing>   → correct the frame first
  deepen        → re-scan the dump for anything this frame dropped
  tasks <#>     → break goal # all the way down into its task tree
  goalify <#>   → structure goal # into a locked, autonomous /goal run
  /goal <#>     → push goal # straight into an autonomous run, raw
  grill <#>     → goal # is high-stakes: interview me, lock a plan, have a second model attack it
  workflow <#>  → hand goal # to a workflow architect (build + run a multi-agent harness)
```

The menu is a router. `go` locks the frame and works normally. The other seven verbs escalate a single goal to the right amount of machinery: a full task breakdown, a locked autonomous contract, an adversarial plan review, or a multi-agent workflow. One voice note in, the right weight of process out.

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

`orient` is the front door to my larger setup. The escalation verbs (`goalify`, `/goal`, `grill`, `workflow`) route to sibling skills (`goalify`, `grill-me-codex`, `workflow-architect`) that live only in my setup. `orient` works on its own: the mirror, the parse rules, and the confirm gate need nothing else. Treat the escalation verbs as a list of where a goal could route, and build your own back ends, or use only the mirror-and-confirm.

My setup also pairs `orient` with a `UserPromptSubmit` nudge hook, `orient-detect.js`, for more reliable auto-triggering. The hook lives outside this repo; Claude Code still auto-fires from description matching, just less reliably.

---

## License

MIT. Take it, fork it, bend it to your own voice. See [LICENSE](./LICENSE).
