# refhub-claude (archived)

> // deprecated — superseded by self-hosted marketplaces

This repo is archived. It used to be a pure index — no plugin logic of its own — listing `refhub-skill` as a Claude Code marketplace entry.

Each RefHub skill/plugin repo now self-hosts its own Claude Code and Codex marketplace manifests instead of relying on a shared index repo. Install directly from the repo you want:

- [`refhub-skill`](https://github.com/refhub-io/refhub-skill) — agent skill for operating RefHub through its public API v2 (vaults, items, tags, relations, import/export, audit, Semantic Scholar, PDF upload)
- [`refhub-paper-drafter`](https://github.com/refhub-io/refhub-paper-drafter) — HCI/visualization paper drafting skill, built on top of `refhub-skill`

```sh
claude plugin marketplace add https://github.com/refhub-io/refhub-skill
claude plugin install refhub-skill@refhub-skill
```

No further changes will be made to this repository.
