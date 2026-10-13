# Rules

## Release management

Version bumps are controlled by `plugin.json:version`/`marketplace.json:plugins:version` and happen at release closure, not per PR. Do not bump versions in feature PRs.

## Commit requirements

All commits MUST be signed (`-S`) and signed-off (`-s`). Use: `git commit -S -s -m "..."`

## Agent skills

### Domain docs

Single-context repo: one `GLOSSARY.md` + `docs/adr/` at the repo root. See `docs/agents/domain.md`.

### Backlog

GitHub Issues tracked in a GitHub Project, managed with the backlog skills. The Project and label vocabulary are in `docs/agents/backlog.md`.

