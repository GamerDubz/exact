# Exact agent marketplace

This fork of [expo/exact](https://github.com/expo/exact) adds a Claude Code and Codex
marketplace with one plugin, `exact`. The plugin is a thin skill that clones upstream
`expo/exact` and sends the agent to its start-here guide. It vendors none of Exact.

Upstream does not take pull requests, so the marketplace lives here. Every added file is
in a path upstream does not use (`.claude-plugin/`, `.agents/`, `plugins/`,
`MARKETPLACE.md`), so merging upstream never conflicts.

## Install

Claude Code:

```sh
claude plugin marketplace add GamerDubz/exact
claude plugin install exact@exact-agent-marketplace
```

Codex: add `GamerDubz/exact` as a marketplace, then enable `exact@exact-agent-marketplace`.

## Automatic install

From a clone of this fork, `node plugins/exact/scripts/install.mjs` detects Claude Code and
Codex, shows a plan, and after approval installs the marketplace plugin for a client that
supports plugins, or copies the skill file for a client that does not. Absent clients are
skipped; a skill file that differs from this version's is never overwritten. Options:
`--yes`, `--client claude|codex`, `--mode plugin|skill`.

Without a clone, `npx github:GamerDubz/exact-plugin` does the same from the small standalone
repo. Both register a marketplace named `exact-agent-marketplace`, so use one source per
machine.

## Sync from upstream

```sh
git remote add upstream https://github.com/expo/exact.git   # once
git fetch upstream
git merge upstream/main
git push origin main
```

Do not use `gh repo sync --force` or `git reset --hard upstream/main`: they delete the
marketplace commits.
