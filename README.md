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
```

You say `go`, it locks the frame and works. You say `fix`, it corrects the read first. The frame comes before the work.

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

`orient` is the front door to my larger setup. It references `goalify`, `workflow-architect`, and `grill-me-codex`, which turn a goal into an autonomous run or multi-agent workflow. Those skills live only in my setup. `orient` works on its own. The references show possible next steps. Build your own back ends, or use only the mirror-and-confirm.

My setup also pairs `orient` with a `UserPromptSubmit` nudge hook, `orient-detect.js`, for more reliable auto-triggering. The hook lives outside this repo; Claude Code still auto-fires from description matching, just less reliably.

---

## License

MIT. Take it, fork it, bend it to your own voice. See [LICENSE](./LICENSE).
