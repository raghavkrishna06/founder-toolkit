# Is This a KPI or a Wish?

A free Claude Skill that checks a goal, KPI, OKR or target and tells you — plainly — whether it's something you can actually measure, or a wish dressed up as a target. If it's not there yet, it shows you exactly what's missing and hands back a version you can use.

"Improve the efficiency of our operations" reads like a target right up until someone tries to measure it. Most goals start life that way. This skill catches that before it reaches a board pack or a funder report.

---

## What it does

Give it a goal — one, or a whole list — and it works out what kind of thing you've written and runs it through a short test: is it defined so two people would measure it the same way, does it have a baseline, a target, a date, an owner, a source, and a real decision it would inform? Then it gives you a verdict:

- **Wish** — can't be measured or reached as written.
- **Not yet** — the idea is sound, but something specific is missing.
- **Ready** — it holds up; here's the tightened version.

It will either give you the verdict, the main gap and a rewrite in one go, or coach you to a good goal one question at a time — starting with the question most goals skip: *what decision is this number actually meant to inform?*

## What it won't do

- Invent numbers, baselines or benchmarks for you — it works from what you tell it.
- Tell you whether the goal is the *right* goal for your strategy. It checks whether it's measurable and real, not whether it's wise.
- It's one focused tool. For thinking a broader decision through — whether to keep a programme, how to stop being the bottleneck — see the [Root Cause Coach](../root-cause-coach), which includes this same goal-checking method as one of its moves.

## Install

This is a single-file skill — just the `SKILL.md` in this folder, nothing else to load.

### On Claude.ai (Pro, Max, Team or Enterprise)
1. Download this `kpi-or-wish` folder and zip it (the zip should contain the folder with `SKILL.md` inside).
2. In Claude, go to **Settings → Features** and upload the zip.
3. Make sure **code execution** is enabled — custom Skills need it.

### In Claude Code
Put the folder in your skills directory so you have `~/.claude/skills/kpi-or-wish/SKILL.md`:

```bash
cp -r founder-toolkit/kpi-or-wish ~/.claude/skills/
```

Claude discovers it automatically.

### On other tools (Gemini, ChatGPT, etc.)
Because it's a single file with no separate references, you can paste the contents of `SKILL.md` straight in as the system prompt or custom instructions, or upload the file to a project, Gem or custom GPT.

For the latest, surface-specific steps, see Anthropic's [Agent Skills documentation](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview).

## Using it

You don't have to name the skill. Just paste a goal and ask "is this any good?", or "how would we measure this?", and it takes it from there.

## Author

Built by Raghav Krishna. I write about running small organisations well at *The Monday Manager* — [add your link].

## Licence

Free to use and adapt. [Choose a licence — MIT is a reasonable default for open reuse.]
