# BuildBot

The builder for your AI workspace. Interviews you, blueprints on one page, builds only what you ratified, proves it while you watch.

BuildBot constructs the agents, skills, tools, and structures your AI setup grows by. It interviews you in plain English until the job is clear, puts a one-page blueprint in front of you, builds exactly what you approved and nothing more, then proves the result by running it end to end while you watch. It never certifies its own work: acceptance belongs to an independent check and to you actually using the thing once.

Sibling to [BloatBot](https://github.com/jdpolasky/bloatbot). BuildBot grows the system, BloatBot prunes it, and neither grades its own work. Both came out of [chief-of-staff-2](https://github.com/jdpolasky/chief-of-staff-2), an AI Chief of Staff that lives in an Obsidian vault as plain markdown. BuildBot builds new parts for it and BloatBot keeps it lean. BloatBot is optional: BuildBot's SKILL.md uses it for the independent check only if it's installed.

Works on Obsidian vaults, Logseq graphs, plain markdown folders, and agent workspaces (Claude Code, Codex, etc.).

## Install

Get the files first:

```bash
git clone https://github.com/jdpolasky/buildbot
cd buildbot
```

**Claude Code** (bash on macOS, Linux, or Git Bash):

```bash
# all projects
mkdir -p ~/.claude/skills
cp -r buildbot ~/.claude/skills/buildbot

# or one project
mkdir -p your-project/.claude/skills
cp -r buildbot your-project/.claude/skills/buildbot
```

**Claude Code** (Windows PowerShell):

```powershell
# all projects
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null
Copy-Item -Recurse buildbot "$HOME\.claude\skills\buildbot"

# or one project
New-Item -ItemType Directory -Force your-project\.claude\skills | Out-Null
Copy-Item -Recurse buildbot your-project\.claude\skills\buildbot
```

New session, then `/buildbot`.

**Codex:** OpenAI's docs say Codex reads skills in this same SKILL.md format from a `.agents/skills` folder, either in your home folder or in a repo. Copying `buildbot` there should work. BuildBot was tested on Claude Code and hasn't been run on Codex yet.

**Everything else:** `buildbot/SKILL.md` is plain instructions. Paste it into any model that can read and write your files and tell it what you want built.

## Usage

```
/buildbot
> What should this thing do, for whom, how often,
> and what must it never do?
"A weekly review skill for my vault. Reads my daily notes,
drafts a review. It must never edit the notes themselves."
```

It interviews until the job is clear, restates the job in two sentences for your sign-off, then blueprints:

```
BLUEPRINT: weekly-review skill
- Loads: daily notes from the last 7 days, nothing else
- Tools: read-only on the vault; writes one new file per run
- Guardrail: never edits an existing note
- Verify: first run happens while you watch
- You own: one skill file; delete it and the skill is gone

Approve, amend, or kill?
```

Nothing gets built from an unratified blueprint. After the build, it runs the real invocation once, end to end, and reports what actually happened, never what should happen.

## What it enforces

- The smallest artifact that serves the ratified blueprint, never more
- A one-page blueprint before any file exists
- Proof by watching the real thing run, not by "should work"
- Independent acceptance: an audit pass plus you using it once
- Rebuild safety: new built next to old, old archived whole, never deleted
- No self-generated work, ever; it builds what you ordered and stops

## The ledger

Optionally (with your permission) it keeps one file, `buildbot-ledger.md`: the lessons every build gets checked against, your rulings, and a registry of what was built when. Nothing else.

## Why

AI workspaces grow by accretion. A skill bolted on here, a config pasted there, and six months later nobody can say what half of it does or whether it ever worked. The failure pattern is always the same: things declared done that nobody watched working, structure nobody planned, builders grading themselves. BuildBot exists so that everything your system grows is ordered, blueprinted, watched working once, and checked by someone other than its builder.

## Who made this

Built by Joshua Polasky, a strategy and operations consultant. Business first, then AI. If you're an owner or leader who wants help figuring out where AI fits in your business, get in touch: joshua.polasky@gmail.com or [LinkedIn](https://linkedin.com/in/joshuapolasky).
