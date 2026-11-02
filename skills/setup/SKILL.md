---
name: setup
description: >-
  Link a GitHub Project and create the label vocabulary for this repo's backlog, and document both
  in docs/agents/backlog.md. Run once per repo, and again to change either.
disable-model-invocation: true
---

Make this repo ready for the backlog skills. When you finish, a GitHub Project is linked to the
repo, the label vocabulary exists, and `docs/agents/backlog.md` names the Project and the labels.
The repo's `CLAUDE.md` or `AGENTS.md` links to that file, so the other skills load it only when
they need it.

Explore first. If Issues or Projects are disabled on the repo, tell the user which setting to turn
on and stop. Otherwise find the Projects linked to the repo, its labels, which of `CLAUDE.md` and
`AGENTS.md` exist, and whether `docs/agents/backlog.md` and a Backlog section already do. An
existing `docs/agents/backlog.md` is the source of truth on a re-run, so keep its choices.

Reuse a Project already linked to the repo, preferring one titled `<owner>/<repo> Backlog`. If none
exists, create one with that title and the short description `Backlog for <owner>/<repo>`, private
unless the user asks otherwise, and link it. Leave the Status field as GitHub created it.

The default label vocabulary is in [backlog.md](./backlog.md), which is also the template for the
repo's file. The user can keep the defaults or map any of them to labels the repo already uses.
Create only the labels that are missing, and leave existing labels, Projects and their settings
alone.

Give each label you create a color that tells the reader something. Priority and effort are
ordered, so each group runs as a gradient along one hue or ramp, `P0` to `P3` and `XS` to `XL`,
with `P0` the most alarming. Each new type label gets a color that fits its meaning, such as red
for `type:bug` and a warning color for `type:security`, and that no other type label in the repo
uses. Existing type labels keep their colors even when they already collide. `needs-clarification`
gets an attention color that stands out from the other groups.

Write the repo's `docs/agents/backlog.md` from the template, filled in with the Project and the
labels in use. Then add a `## Backlog` section to `CLAUDE.md` if it exists, otherwise `AGENTS.md`,
that links to it. If neither exists, ask the user which to create. Re-running updates the file and
that section in place, and changes nothing that is already right.

When you finish, report what you created, reused and changed.
