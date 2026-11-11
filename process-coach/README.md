# Process Coach

A free Skill that helps the founder of a small social-impact organisation improve how one of its processes actually runs — one question at a time — and come away with a map of the process, a single fix to make this week, and a date to check it.

It is built for the same people as its sibling, the Root Cause Coach: founders of small, mission-driven organisations, often under twenty people, often without a board that functions as one, a COO, or an operations person to lean on. The difference is what it works on. The Root Cause Coach helps you think through a hard *decision*. The Process Coach helps you fix a *process* — one that is messy, inconsistent, half-finished, or trapped in your own head — by drawing it out of you, laying it out as a map you can actually see, and leaving you holding a first fix you can make.

---

## What it helps with

The Coach is deliberately narrow. It takes **one process** from "how we happen to do it" to "how we mean to do it". Bring it:

1. **A process that is a mess** — inconsistent, done differently every time, nobody quite sure of the steps.
2. **Something that only works when you do it**, or that lives in your head.
3. **A recurring task you want to make repeatable.**
4. **A new process you're about to launch** and want to set up properly before it becomes a scramble.
5. **A nagging sense that something is breaking** and you can't see where.

It says so plainly when what you've brought is really something else — a decision, a goal, a why-problem — and points you to the right tool (see *What it will not do*).

## What a conversation is like

- One question at a time, in plain language. It follows your words, not a script.
- It mirrors how you write, including a mix like Hinglish.
- Before anything else, it pins down what the process is *for* — a goal you could actually check — so every step can be judged against it. It won't map against a vague wish.
- It **draws your process as a map you can see**: a swimlane, one lane per person, the flow running left to right, with the weak joints marked in red and arrows showing the handoffs — the moments where a task passes from one person to another and lands nowhere. For most founders, seeing it drawn is the moment the problem becomes obvious.
- It hands the map back for you to correct, not approve. The map is yours — every step traces to something you said, not a tidy standard process you'd never run.
- It usually takes 20–40 minutes.
- It fixes **one thing**, chosen by what it costs you against the goal, not by what annoys you most. The other weak joints are parked, named, and left visible on the map for a later session.
- It ends with three things: the **one fix** written in your own words (what changes, who owns it, what sets it off), a **check-back date** it proposes for you to confirm or change, and a **downloadable map** you can keep, print and share — your process with the breaks marked and your fix on it.

## What it will *not* do

This is the part most tools leave out. The Coach is honest about its edges, on purpose:

- It only knows what you tell it. It can't see your organisation, watch the process in action, check your numbers, or hear your team.
- It won't make the fix for you or promise it will work. It will give an honest view with reasons if you ask — the change and the risk stay yours. The map and the fix are yours to run.
- It is the **how**, not the **why**. If the real problem is *why* something keeps failing — a fine process a person won't follow, a cause upstream of any step — or whether to keep the thing at all, or a goal that needs sharpening, it names that and points you to the right tool, usually its sibling the **Root Cause Coach**.
- It isn't a strategy or planning tool. It fixes the shape of one process — not what to build in what order, not whether the money or the people will come through, not the funnel behind it.
- One process at a time, one fix per session. It won't hand you a ten-step plan you won't start.
- No legal, financial, tax, grant-compliance or safeguarding advice. It will help you list what to ask an accountant, a lawyer or your funder.
- It can drop the check-back date into your calendar if your Claude setup has one connected; otherwise you add it. What it can't do is chase you on the day or carry a memory of the conversation into the next chat on its own — so keep the map and the note, and bring them back when the date comes.
- It is not a substitute for human support in a crisis. If you are in real distress, please talk to someone you trust and contact a local helpline or a doctor.

---

## Install

The Coach is a Claude Skill. This folder holds the source (`process-coach/SKILL.md` and its `references/` folder) and a packaged **`process-coach.skill`** — a single zip you can install directly. To use the Coach you only need that one file; there's no need to download the whole repo. On its page in GitHub, use the download button ("Download raw file") to grab just it.

### On Claude.ai (Pro, Max, Team or Enterprise)
1. Download `process-coach.skill` from this folder and rename it to `process-coach.zip`.
2. In Claude, go to **Customize → Skills** and upload the zip.
3. Make sure **code execution** is enabled — custom Skills need it, and this one uses it to draw your map.
Custom Skills are per-user: each person uploads their own copy.

### In Claude Code
Unzip it into your skills folder so you have `~/.claude/skills/process-coach/SKILL.md`:

```bash
unzip process-coach.skill -d ~/.claude/skills/
```

Use `.claude/skills/` inside a project instead if you want it only there. Claude discovers it automatically — no restart needed.

### Using it
You don't have to name the skill. Just describe the process that's bothering you — "our process for X is a mess", "we do this differently every time", "this only works when I do it", "map out our onboarding", "I want to set this up before we launch" — and the Coach takes it from there.

For the latest, surface-specific steps, see Anthropic's Agent Skills documentation: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview

---

## Using it on other tools (Gemini, ChatGPT, Codex, etc.)

The Coach is plain-text instructions, so it works on any capable model — only the auto-trigger, the on-demand loading of the map reference, and the rendered map image are specific to Claude.

- **Agents with file access** (Codex, Gemini CLI, Cursor, and the like): point them at this folder. The "read `references/the-map.md`" instruction works because the agent can open the file itself.
- **Plain chat** (the Gemini or ChatGPT app, without a project): these can't open the reference file mid-conversation. Use **`process-coach-combined.md`** — the whole Coach flattened into one file, with the map template included — and paste it in as the system prompt / custom instructions, or upload it to a Project, Gem or custom GPT.

On any tool other than Claude you activate it yourself (paste it in or set it as instructions); it won't trigger on its own. The map is drawn as a self-contained HTML/SVG diagram: you'll see it rendered on a tool that can run or preview that, and get it as markup to render yourself on one that can't. The calendar step only works where the tool has a calendar connected.

---

## How it was built and tested

The Coach was written from one operator's experience of mapping how the processes inside small organisations actually run — and of watching good processes fail not inside any one person's job, but in the handoffs between people. It was tested two ways. In simulation, founders of different kinds each brought a different shape of problem — one with a described process and fixes of her own, one genuinely stuck who kept trying to hand the Coach the answer, one who demanded a prescription and arrived set on buying a tool, a tangled five-actor flow, and one setting up a brand-new process from scratch before launch — and a separate, independent agent scored every transcript against a fixed rubric: whether the map was drawn from the founder's own words, whether the Coach stayed on the *how* instead of drifting into the *why* or into strategy, whether it pinned a real goal before mapping, whether it chose the fix by cost rather than irritation, and whether it let the founder shape the fix instead of declaring it. And on real work: I ran it on my own live processes — an outreach pipeline and a post-contract donor-stewardship workflow — where it had to handle the mess a simulation smooths over, and those runs surfaced problems the simulations hadn't.

Those tests drove real changes. The Coach now holds the goal before it draws anything; it renders the process as a proper horizontal swimlane with the handoffs drawn in, so the breaks between people are visible rather than buried; the map it hands you at the end keeps every parked problem on it, not a cleaned-up version; it extracts the fix from you rather than handing you one; and it proposes the check-back date for you to confirm or change rather than setting it for you.

Honest caveat: simulated founders are more cooperative than real ones, and my own real runs are still only mine. It hasn't yet been proven with other founders on their own processes. If you use it, telling me where it helped and where it fell short is the most valuable thing you can do.

## Feedback and contributions

This is a free tool meant to be useful on its own. Issues and pull requests are welcome — especially real-world accounts of where a conversation worked or went wrong.

## Author

Built by Raghav Krishna. I help social impact founders stop firefighting and start growing their impact — https://www.raghavkrishna.com/

## Licence

MIT — see the [LICENSE](../LICENSE) at the repo root.
