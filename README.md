# Backcraft

Agent skills for writing a backlog you can build from, right in GitHub Issues and Projects. Nothing to host.

Most of us learned to write code. Hardly anyone taught us to write a backlog item. So we jot down "add payment retry logic", leave it for a month, and whoever picks it up spends a week guessing what it meant.

A good item answers four questions before anyone opens an editor. What are we building, why, for whom, and how will we know it's done? Write those down and you can hand the item to a teammate or an agent and get back what you asked for. Backcraft walks you through writing items like that, and keeps them that way.

## How it works

Everything lives in GitHub. Each item is an issue on a Project board, and buildable work carries one label each for type, priority and effort. There's no second database to drift out of sync.

An item has to pass [INVEST](https://en.wikipedia.org/wiki/INVEST_(mnemonic)) before anyone can pick it up. I treat that as the minimum for saying anyone understands it. When an item falls short or has open questions, it gets `needs-clarification`, and `/pick-item` passes over it until `/refine-item` sorts it out. Half-formed ideas are fine too. `/add-idea` parks one at the bottom of the queue so you don't lose it.

Priority and order are separate on purpose. Priority is how much something hurts. Rank, the item's position in the Project, is what you do next. When `/add-item` suggests a position that disagrees with the priority, it tells you why, and nothing moves without your say-so. If the order changed, you changed it.

The agent checks the structure. You make the calls.

## Getting started

You'll need:

- an agent harness that loads `SKILL.md` skills, such as [Claude Code](https://claude.ai/code), [Codex](https://github.com/openai/codex), [pi](https://github.com/earendil-works/pi) or [oh-my-pi](https://github.com/can1357/oh-my-pi)
- the [GitHub CLI](https://cli.github.com/) (`gh`), signed in
- a GitHub repo with Issues turned on

### Install

```bash
npx skills@latest add gringolito/backcraft
```

### Claude Code plugin

If you'd rather use Claude Code's plugin marketplace:

```text
/plugin marketplace add gringolito/backcraft
/plugin install backcraft@gringolito
```

Restart Claude Code if it was already open.

### First run

Run `/setup` once in the repo you want to use Backcraft with. It links a Project, creates the labels and writes both to `docs/agents/backlog.md`, which the other skills read. Edit that file when you want different labels. Running `/setup` again is safe.

### Upgrading from github-backlog-management

Backcraft used to be called `github-backlog-management`. Remove the old plugin and marketplace, then install as above:

```text
/plugin uninstall github-backlog-management@gringolito
/plugin marketplace remove gringolito
```

## Skills

| Skill | What it does |
|---|---|
| `/setup` | Links a GitHub Project, creates the labels and records both in `docs/agents/backlog.md`. |
| `/add-item` | Turns a request into one well-formed, ranked backlog item. |
| `/add-idea` | Parks a rough idea at the bottom of the backlog, with no priority or effort. |
| `/migrate` | Imports an existing `TODO.md`, `BACKLOG.md` or other list into GitHub Issues. |
| `/refine` | Runs a refinement session over items that need clarification or labels. |
| `/refine-item` | Brings one item up to standard, or turns an idea into a defined item. |
| `/pick-item` | Picks the top unblocked item, checks it's ready and assigns it to you. |
| `/spike` | Investigates a spike and opens a findings pull request with follow-on items. |
| `/external-blocker` | Records, links and resolves blockers outside the team's control. |
| `/plan-release` | Creates a Milestone with a version, due date and scope, or re-plans one. |
| `/release-status` | Shows how a release is going: progress, blocked items, items needing clarification. |
| `/close-release` | Closes a Milestone and publishes its release. |
| `/health` | Shows the shape of the whole backlog: distribution, age, overdue priorities, stale work. |
| `/audit` | Finds conflicting labels, malformed items, broken dependencies and milestone mix-ups, with a fix for each. |

## Contributing

Found a bug or a gap in your workflow? Open an issue. For a bug, say which skill, what you expected and what happened. For an idea, describe the gap you hit.

Pull requests are welcome. Fork, branch and edit the skill under `skills/<name>/`, following [CODING_STANDARDS.md](CODING_STANDARDS.md). Commits follow [Conventional Commits](https://www.conventionalcommits.org/).

## License

MIT. See [LICENSE](LICENSE).

### On Beer-ware

Poul-Henning Kamp wrote the Beerware License in the 1990s: *if you think this software is worth it, and we ever meet in person, you can buy me a beer.* It's one of the most honest licenses ever written. Sadly, it isn't OSI-approved, and corporate legal teams can't wave it through, so this project is MIT. Lawyers can sleep soundly.

The spirit stays, though. If Backcraft saved you an afternoon of backlog wrangling, or just made your GitHub a little less of a mess, and we ever happen to meet, you can buy me a beer.
