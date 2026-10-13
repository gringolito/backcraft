# Backcraft

Agent skills for writing a backlog you can build from, right in GitHub Issues and Projects.
Nothing to host.

Most of us learned to write code, but not how to write a backlog item. A note like
"add payment retry logic" is easy to write. Come back to it later, and it leaves too much to guess.

A useful item says what we're building, why it matters, who it's for and how we'll know it's done.
Backcraft helps you work through those questions before handing the item to a teammate or agent.

## How it works

Everything lives in GitHub. Each item is an issue on a Project board, and buildable work
carries one label each for type, priority and effort.
There's no second database to drift out of sync.

`/add-item` and `/refine-item` check items against
[INVEST](https://en.wikipedia.org/wiki/INVEST_(mnemonic)): independent, negotiable, valuable,
estimable, small and testable. Items with open questions get `needs-clarification`,
and `/pick-item` skips them until they're refined.

Half-formed ideas are fine too. `/add-idea` parks one at the bottom of the queue
so you don't lose it.

Priority and order are separate on purpose. Priority says how badly something matters. Rank is the
order of work in the Project. `/add-item` proposes where a new item belongs and explains when that
differs from its priority. It asks before moving existing items.

Blockers are recorded as GitHub dependencies. `/pick-item` skips items whose blockers
are still open.

The agent checks the structure. You make the calls.

## Getting started

You'll need:

- an agent that loads `SKILL.md` skills, can run `gh`, and can read and edit files in your repo,
  such as [Claude Code](https://claude.ai/code), [Codex](https://github.com/openai/codex),
  [pi](https://github.com/earendil-works/pi) or [oh-my-pi](https://github.com/can1357/oh-my-pi)
- the [GitHub CLI](https://cli.github.com/) (`gh`), signed in
- a GitHub repo with Issues turned on

### Install

```bash
npx skills@latest add gringolito/backcraft
```

### Claude Code plugin

If you'd rather use Claude Code's plugin marketplace, install with the commands below.
Already using `github-backlog-management`? Follow the
[upgrade steps](#upgrading-from-github-backlog-management) first.

```text
/plugin marketplace add gringolito/backcraft
/plugin install backcraft@gringolito
```

Restart Claude Code if it was already open.

### First run

Run `/setup` once in the repo you want to use Backcraft with. It links a Project,
creates the labels and writes both to `docs/agents/backlog.md`, which the other skills read.
Edit that file when you want different labels. Running `/setup` again is safe.

Make sure your agent reads the `CLAUDE.md` or `AGENTS.md` file that `/setup` updates.

Start with `/add-item` to define work, `/add-idea` to save a rough thought, or `/migrate`
to import an existing backlog.

### Upgrading from github-backlog-management

Backcraft used to be called `github-backlog-management`. Remove the old plugin and
marketplace, then follow the [Claude Code plugin installation steps](#claude-code-plugin):

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
| `/refine-item` | Clarifies one item and checks it against INVEST, or turns an idea into a defined item. |
| `/pick-item` | Picks the top unblocked item, checks it's ready and assigns it to you. |
| `/spike` | Investigates a spike and opens a findings pull request with follow-on items. |
| `/external-blocker` | Records, links and resolves blockers outside the team's control. |
| `/plan-release` | Creates a Milestone with a version, due date and scope, or re-plans one. |
| `/release-status` | Shows how a release is going: progress, blocked items, items needing clarification. |
| `/close-release` | Closes a Milestone and publishes its release. |
| `/health` | Shows the shape of the whole backlog: distribution, age, overdue priorities, stale work. |
| `/audit` | Finds conflicting labels, malformed items, broken dependencies and milestone mix-ups, with a fix for each. |

## Contributing

Found a bug or a gap in your workflow? Open an issue. For a bug, say which skill, what you expected
and what happened. For an idea, describe the gap you hit.

Pull requests are welcome. Fork, branch and edit the skill under `skills/<name>/`, following
[CODING_STANDARDS.md](CODING_STANDARDS.md). Commits follow
[Conventional Commits](https://www.conventionalcommits.org/).

## License

MIT. See [LICENSE](LICENSE).

### On Beer-ware

Poul-Henning Kamp wrote the Beerware License in the 1990s: *if you think this software is worth it,
and we ever meet in person, you can buy me a beer.* It's one of the most honest licenses
ever written.

Beerware isn't OSI-approved. Backcraft uses MIT instead to make it easier to adopt at work.

The spirit stays, though. If Backcraft saved you an afternoon of backlog wrangling, or just made
your GitHub a little less of a mess, and we ever happen to meet, you can buy me a beer.
