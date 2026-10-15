# Root Cause Coach

A free Skill that helps the founder of a small social-impact organisation think through a hard decision — one question at a time — and come away with something written down and a date to look at it again.

It is built for people who carry every decision alone: founders of small, mission-driven organisations, often under twenty people, often without a board that functions as one, a COO, or an advisor to call. The Coach is not a consultant and not a substitute for one. It is a calm, structured thinking partner for the moment you are stuck.

---

## What it helps with

The Coach is deliberately narrow. It works well for seven situations, and it says so plainly when you bring it something else.

1. **Keep, fix or stop** something that already exists — a programme, a school, a product, a service.
2. **Write or sharpen a goal or KPI** — turning "strengthen livelihoods" into something you could actually tell had moved.
3. **Fire or pattern** — when you are always firefighting, telling a real emergency from a habit.
4. **Who decides** — when everything waits on you and you want decisions off your desk.
5. **Hand it off** — delegating a task, or getting a judgment call out of your own head.
6. **Test a new idea** — before you commit money and time to it.
7. **Make it stick** — setting up a change so it survives, and reviewing honestly what happened.

## What a conversation is like

- One question at a time, in plain language. It follows your words, not a script.
- It mirrors how you write, including a mix like Hinglish.
- It usually takes 15–30 minutes.
- It ends with three things: a short note in **your own words** (a decision record, a sharpened goal, a delegation brief), a **check-back line with a date**, and **one next step** for this week.
- If the problem keeps happening, it won't just treat the surface of it — it helps you work out whether you're fixing the real cause or a symptom of something upstream.
- Sometimes the honest answer is to leave a thing alone. If something isn't worth your scarce attention, it will say so rather than manufacture a decision.

## What it will *not* do

This is the part most tools leave out. The Coach is honest about its edges, on purpose:

- It only knows what you tell it. It can't see your organisation, check your numbers, or hear your team.
- It won't make the decision for you, or tell you something will work. It will give an honest view with reasons if you ask — the decision and the risk stay yours.
- No legal, financial, tax, grant-compliance or safeguarding advice. It will help you list what to ask an accountant, a lawyer or your funder.
- It can drop the check-back date into your calendar if your Claude setup has one connected; otherwise you add it. What it can't do is chase you on the day or carry a memory of the conversation into the next chat on its own — so keep the note and bring it back when the date comes.
- It isn't a general business coach. For hiring or firing a specific person, fundraising strategy, a co-founder or board conflict, or legal and financial structure, it will say so and point you to who can help.
- It is not a substitute for human support in a crisis. If you are in real distress, please talk to someone you trust and contact a local helpline or a doctor.

---

## Install
 
The Coach is a Claude Skill. This folder holds the source (`SKILL.md` and the `references/` folder) and a packaged **`root-cause-coach.skill`** — a single zip you can install directly. To use the Coach you only need that one file; there's no need to download the whole repo. On its page in GitHub, use the download button ("Download raw file") to grab just it.
 
### On Claude.ai (Pro, Max, Team or Enterprise)
1. Download `root-cause-coach.skill` from this folder and rename it to `root-cause-coach.zip`.
2. In Claude, go to **Settings → Features** and upload the zip.
3. Make sure **code execution** is enabled — custom Skills need it.
Custom Skills are per-user: each person uploads their own copy.
 
### In Claude Code
Unzip it into your skills folder so you have `~/.claude/skills/root-cause-coach/SKILL.md`:
 
```bash
unzip root-cause-coach.skill -d ~/.claude/skills/
```
 
Use `.claude/skills/` inside a project instead if you want it only there. Claude discovers it automatically — no restart needed.

### Using it
You don't have to name the skill. Just describe where you're stuck — "I don't know whether to shut this down", "is this KPI any good", "everything comes to me" — and the Coach takes it from there.

For the latest, surface-specific steps, see Anthropic's Agent Skills documentation: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview

---

## Using it on other tools (Gemini, ChatGPT, Codex, etc.)
 
The Coach is plain-text instructions, so it works on any capable model — only the auto-trigger and the on-demand loading of the module files are specific to Claude.
 
- **Agents with file access** (Codex, Gemini CLI, Cursor, and the like): point them at this folder. The "read `references/…`" instructions work because the agent can open the files itself.
- **Plain chat** (the Gemini or ChatGPT app, without a project): these can't open the reference files mid-conversation. Use **`root-cause-coach-combined.md`** — the whole Coach flattened into one file — and paste it in as the system prompt / custom instructions, or upload it to a Project, Gem or custom GPT.
On any tool other than Claude you activate it yourself (paste it in or set it as instructions); it won't trigger on its own, and the calendar step only works where the tool has a calendar connected.

---

## How it was built and tested

The Coach was written from one operator's experience of what small-organisation founders actually get stuck on, then stress-tested in simulation: founders of different temperaments (terse, rambling, defensive, sceptical, overwhelmed), and a round of deliberately adversarial founders written to break it — people who agree without thinking, give self-serving accounts, drift, or present an in-scope decision that is really masking something the Coach shouldn't touch. A separate, independent agent scored the transcripts. Those tests drove real fixes: it now notices when you're only agreeing and hands the thinking back, and it names when a decision is really about something outside its scope instead of coaching the surface of it.

If you use it, telling me where it helped and where it fell short is the most valuable thing you can do.

## Feedback and contributions

This is a free tool meant to be useful on its own. Issues and pull requests are welcome — especially real-world accounts of where a conversation worked or went wrong.

## Author

Built by Raghav Krishna. I help social impact founders stop firefighting and start growing their impact — https://www.raghavkrishna.com/
