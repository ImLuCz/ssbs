# Second Brain

A personal knowledge and task system, run as a plain git repo and driven mostly
through conversation with [Pi](https://pi.dev), a terminal coding agent. You
don't file things by hand — you just talk, and Pi sorts things into the right
place based on the rules in `AGENTS.md`.

## Why this exists

Most note-taking systems fail because filing things takes effort you don't have
in the moment. This system tries to remove that friction: you say things out
loud (or type them) the way you'd naturally say them — "I need to do this
today," "that's interesting, I'll look into it" — and the agent does the filing
for you. Review happens on a schedule, not constantly, so you're not maintaining
this system, you're just using it.

## Layout

```
second-brain/
  AGENTS.md          Instructions Pi reads every session — this is the system's brain
  INBOX.md            Unsorted catch-all, cleared out during review
  TODO.md              Tasks, grouped by deadline: Today / This Week / This Month / Someday
  ideas/                 One file per idea worth researching later
  projects/                One file per thing you're actively working on
  knowledge/                  One file per topic you're learning
  archive/projects/               Finished projects, moved here instead of deleted
  .pi/prompts/                        Slash-command templates (see below)
```

### TODO.md

Four sections, by how soon it's due: **Today**, **This Week**, **This Month**,
**Someday**. "Someday" is for things you don't want to forget but haven't
committed to a deadline on. Undone daily tasks don't just vanish — they get
surfaced again during review, not silently dropped.

### INBOX.md

The landing zone for anything that doesn't obviously belong somewhere else yet.
Better to dump something here than force a decision in the moment. Gets sorted
out during `/review`.

### ideas/

Things worth looking into later, not things to *do*. Created automatically when
you say "that's interesting" or similar, or manually with `/idea <topic>`. Each
file is dated and links back to whatever project or knowledge topic prompted it,
if relevant.

### projects/

Active work: what it is, current status, what's left. Updated as you talk about
the project — you don't edit these by hand. When something's finished, it's
moved (not deleted) to `archive/projects/`, so it stays searchable.

### knowledge/

Topics you're learning — separate from *projects* (which are things you're
building) and *ideas* (which are things you haven't started researching yet).
Each file tracks what you know and what's still an open question.

## How capture works

You don't need to remember commands for most of this. Just talk normally:

- *"I need to finish the deck by Friday"* → added to `TODO.md` under This Week
- *"Huh, I should look into how vector databases handle updates"* → new file in
  `ideas/`
- *"I've been reading about Rust's async model"* → `knowledge/rust-async.md`
  gets created or updated

If Pi isn't sure where something belongs, it goes to `INBOX.md` instead of being
guessed at — you sort it out later.

## Commands (prompt templates)

Pi supports slash commands defined as markdown files in `.pi/prompts/`. These
only load once you've marked the project as trusted (Pi will prompt you the
first time).

| Command | What it does |
|---|---|
| `/capture <note>` | Quick dump into `INBOX.md`, no triage — for when you want to note something without thinking about where it goes |
| `/todo <today\|week\|month\|someday> <task>` | Add a task directly to the right `TODO.md` section |
| `/idea <topic>` | Create a new dated file in `ideas/` |
| `/review` | Full triage pass: sorts `INBOX.md`, rolls over unfinished daily tasks, flags projects that have gone quiet, asks what to do with stale ideas |

Run `/review` roughly once a week. It's the only maintenance this system asks of
you — everything else happens passively while you talk.

## Versioning

This is a git repo, so:

- **History** — every change is a commit; you can always see what changed and
  when.
- **Archive** — nothing is deleted, only `git mv`'d to `archive/`.
- **Backup** — push it to a private remote if you want it off your machine too.

Commit whenever, or have Pi commit after each session — either works, since the
files themselves are the source of truth, not the commit history.

## Getting started

```bash
git clone https://github.com/ImLuCz/ssbs.git
mv ssbs/ second-brain/
cd second-brain/
rm -rf .git/
git init
git add -A
git commit -m "Initial second brain scaffold"
pi   # then trust the project when prompted, so .pi/prompts/ loads
```

From there, just start talking to Pi about what you're working on.
