# Backcraft

> Agent skills for writing a backlog you can build from, in GitHub Issues and Projects. No extra tools, no databases, no webhooks.

## Why

Every developer learns to write code. Few learn to write a backlog item, and it shows. "Add payment retry logic" sits in the queue for a month, then someone picks it up and spends a week building on guesses.

Writing backlog items is a craft, and Backcraft is a set of skills for practicing it. A good item says what you're building, why it matters, who it's for and what done looks like, before anyone opens an editor. Think of a sketch next to a blueprint. Hand a blueprint to a teammate or an agent and you get back what you meant.

Backcraft works in GitHub, where your code and issues already are. Buildable work has to pass [INVEST](https://en.wikipedia.org/wiki/INVEST_(mnemonic)) before anyone picks it up, because that is the lowest bar for saying anyone understands it. An item that fails, or still has open questions, carries `needs-clarification`, and `/pick-item` skips it until `/refine-item` brings it up to standard. Rough ideas don't have to wait for that. `/add-idea` parks one at the bottom of the queue so it isn't lost, and `/refine-item` turns it into a real item when you get to it. Blockers are GitHub dependencies, so blocked work never gets picked.

Order is a decision too. Priority says how much an item matters. Rank, the order in the Project, says what comes next. `/add-item` proposes a Rank and gives its reason when that disagrees with the priority. Nothing gets re-ranked without your OK, so when the order changes, someone chose it.

The agent enforces the structure and you set the priorities. It flags vague items, suggests dependencies for you to confirm and picks the next item. What you do with it is up to you.

Backlogs rot when nobody tends them. Items lose their acceptance criteria, blockers go unrecorded, and the order drifts away from the work until people stop reading it. A backlog you trust is one you follow.

## Breaking changes

- The plugin is now `backcraft`, and the repository is `gringolito/backcraft`. Run `/plugin uninstall github-backlog-management@gringolito` and `/plugin marketplace remove gringolito`, then follow [Installation](#installation).
- `.claude/backlog-project.json` is gone. `/setup` writes the Project and label vocabulary to `docs/agents/backlog.md` and links it from `CLAUDE.md` or `AGENTS.md`.
- Permission modes and the plugin's user configuration are gone. Allow `gh` and `git` in your own Claude Code settings if you want fewer prompts.
- The SessionStart hook and preflight check are gone.
- Issue Forms templates are gone.
- There is no Active Release. A repo usually has one open Milestone; when several are open, skills ask which one.
- Removed or merged skills:

| Removed | Use instead |
|---|---|
| `initialize` | `/setup` |
| `github-backlog-management` | none; the agent picks skills from their descriptions |
| `execute-item` | `/pick-item`, then implement as usual |
| `setup-permissions` | none |
| `add-external-blocker`, `resolve-external-blocker`, `block-item` | `/external-blocker` |

## Requirements

- An agent harness that loads `SKILL.md` skills, such as [Claude Code](https://claude.ai/code)
- [GitHub CLI](https://cli.github.com/) (`gh`), authenticated
- A GitHub repository with Issues enabled and an `origin` remote pointing to it

## Installation

In Claude Code, install Backcraft as a plugin:

```text
/plugin marketplace add gringolito/backcraft
/plugin install backcraft@gringolito
```

Restart Claude Code if it was already running. If installation fails with an SSH error, see [Troubleshooting](#troubleshooting).

In another harness, copy or symlink the folders under `skills/` into its skills directory.

Your `gh` token needs the `repo`, `project` and `read:user` scopes, plus `read:org` for organization repos. Add missing ones with `gh auth refresh --scopes repo,project,read:user,read:org`. With a personal access token, create a new one with these scopes.

## Skills

Run `/setup` once per repo. The other skills read `docs/agents/backlog.md` for the Project and labels.

| Skill | What it does |
|---|---|
| `/setup` | Links a GitHub Project, creates the label vocabulary, and documents both in `docs/agents/backlog.md`. Safe to re-run. |
| `/add-item` | Turns a request into one well-formed, ranked backlog item. |
| `/add-idea` | Parks a rough idea at the bottom of the backlog, with no priority or effort, so it isn't lost. |
| `/migrate` | Imports an existing `TODO.md`, `BACKLOG.md` or other list into GitHub Issues. |
| `/refine` | Runs a refinement session over items that need clarification or labels. |
| `/refine-item` | Brings one item up to standard and clears `needs-clarification`, or turns an idea into a defined item. |
| `/pick-item` | Chooses the next unblocked item by rank, checks it is ready and assigns it to you. |
| `/spike` | Investigates a spike and delivers a findings pull request with follow-on items. |
| `/external-blocker` | Records, links and resolves constraints outside the team's control that block items. |
| `/plan-release` | Creates a Milestone with a version, due date and scope, or re-plans one. |
| `/release-status` | Reports how a Release is tracking: progress, blocked items, items needing clarification. |
| `/close-release` | Closes a Milestone and publishes its release. |
| `/health` | Reports the overall shape of the backlog: distribution, age, overdue priorities, stale work. |
| `/audit` | Finds conflicting labels, malformed items, broken dependencies and milestone inconsistencies, with a fix for each. |

## Conventions

Every Workable Item carries one `type:*`, one `priority:*` and one `effort:*` label. Priority is severity; execution order is the manual rank in the Project. Items that fail [INVEST](https://en.wikipedia.org/wiki/INVEST_(mnemonic)) get `needs-clarification` until refined. Blockers use GitHub's native dependencies (`blocked_by`). Edit `docs/agents/backlog.md` to change the label vocabulary.

## Troubleshooting

### Plugin install fails with SSH authentication error

Symptom: `git@github.com: Permission denied (publickey).` or `Host key verification failed.` during install.

Claude Code clones marketplace plugins over SSH, even for public repos ([anthropics/claude-code#26588](https://github.com/anthropics/claude-code/issues/26588)). Either rewrite SSH URLs to HTTPS:

```bash
git config --global url."https://github.com/".insteadOf git@github.com:
```

or configure SSH for GitHub: trust its host key with `ssh-keyscan -t ed25519 github.com >> ~/.ssh/known_hosts`, and add your key to your GitHub account and `ssh-agent`.

## Contributing

Open an Issue for a bug (which skill, what you expected, what happened) or a feature idea (the workflow gap it closes). For a pull request, fork, branch, and change the skill in `skills/<name>/`. Commits follow [Conventional Commits](https://www.conventionalcommits.org/).

## License

MIT. See [LICENSE](LICENSE).

### On Beer-ware and the spirit that lives on

Poul-Henning Kamp wrote the Beerware License in the 1990s: *if you think this software is worth it, and we ever meet in person, you can buy me a beer.* It is one of the most honest licenses ever written. Sadly, it isn't OSI-approved, and corporate legal teams can't wave it through, so this project is MIT. Lawyers can sleep soundly.

But the spirit is still here. If Backcraft saved you an afternoon of backlog wrangling, or simply made your GitHub a little less of a mess, and we ever happen to meet, you can buy me a beer.
