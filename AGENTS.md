# Agent Instructions — Second Brain

This repo is a personal knowledge/task system. You (the agent) are responsible for
keeping it organized as we talk. Follow these rules automatically, without being
asked, whenever they apply during normal conversation.

## Passive capture (do this without being asked)

- If I say something like "I need to do this today" / "by next month I have to do
  that" / "remind me to X this week" — append it as a task to the matching section
  of `TODO.md` (`## Today`, `## This Week`, `## This Month`, `## Someday`).
- If I say something like "this is interesting, I'll look into it" / "I need to
  research this more" — create a new dated file in `ideas/` (format:
  `YYYY-MM-DD-short-topic.md`) summarizing the idea and why it came up, with a link
  back to the project/knowledge file that prompted it if there is one.
- If I mention a topic I'm actively learning, check `knowledge/` for an existing
  file on it. If one exists, update it (add to "what I've learned" or "open
  questions"). If not, create one.
- If I describe work on something ongoing — a build, a plan, a piece of writing —
  treat it as a project. Check `projects/` for an existing file; update its status
  and next-steps, or create one.
- **If you're not sure which bucket something belongs in, put it in `INBOX.md`
  instead of guessing.** Never silently misfile something.

## File conventions

- `TODO.md` has four sections: `## Today`, `## This Week`, `## This Month`,
  `## Someday`. Tasks are simple `- [ ]` checkboxes.
- `ideas/`, `projects/`, `knowledge/` are one file per topic, kebab-case filenames.
- Link between files with normal relative markdown links
  (`[project name](../projects/project-name.md)`) whenever you create or edit a
  file that clearly relates to another. Add these links yourself — I won't
  remember to.
- Never delete a completed project file — move it to `archive/projects/` with
  `git mv` so history is preserved.
- Don't silently drop undone daily tasks. If a `## Today` item wasn't checked off,
  it needs to be surfaced, not erased.

## Reviews

When I run `/review`, follow the full procedure in `.pi/prompts/review.md`. Don't
run a review unprompted — only when asked or via the command.

## Commits

At the start of every session, check `git status`. If there are uncommitted
changes, commit them before doing anything else.

After any edit to files in this repo (new task, new idea file, project
update, etc.), immediately stage and commit that change with a short message
describing it.

## Date

Whenever knowing the current date is required to perform an action, check what the current date is using bash commands.
