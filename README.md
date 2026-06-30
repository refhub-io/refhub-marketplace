# refhub-claude

> // claude_code_plugin_registry for [refhub.io](https://refhub.io)

Claude Code plugin marketplace for first-party RefHub agent integrations.

Codex integrations live separately in [`refhub-codex`](https://github.com/refhub-io/refhub-codex) so each agent runtime keeps native packaging instead of sharing the Claude plugin manifest.

---

## // install

```sh
claude plugin marketplace add \
  https://raw.githubusercontent.com/refhub-io/refhub-claude/main/.claude-plugin/marketplace.json
```

then install any plugin from the registry:

```sh
claude plugin install refhub-skill@refhub-claude
```

---

## // plugins

| plugin | description | version |
|--------|-------------|---------|
| [`refhub-skill`](https://github.com/refhub-io/refhub-skill) | agent skill for API-key RefHub vault/item/search/import/export/audit, Semantic Scholar discovery/enrichment, and item-scoped PDF uploads including large-PDF resumable Drive upload | `1.0.2` |

---

## // structure

```
.claude-plugin/
  marketplace.json   ← plugin registry manifest
```

the manifest lists plugin sources. claude code reads this to discover and install plugins. adding a plugin here makes it available to any user who has registered this marketplace.

## // ssh gotcha

`claude plugin marketplace add refhub-io/refhub-claude` uses GitHub shorthand, and Claude resolves that by cloning over SSH:

```text
git@github.com:refhub-io/refhub-claude.git
```

That fails on machines without a GitHub SSH key. Use the raw manifest URL above, or an explicit HTTPS repo URL:

```sh
claude plugin marketplace add https://github.com/refhub-io/refhub-marketplace
```

or the renamed repo directly:

```sh
claude plugin marketplace add https://github.com/refhub-io/refhub-claude
```

The declared marketplace name is still `refhub-claude`, so installation is:

```sh
claude plugin install refhub-skill@refhub-claude
```

---

## // adding a plugin

edit `.claude-plugin/marketplace.json` and add an entry:

```json
{
  "name": "your-plugin-name",
  "description": "...",
  "source": { "source": "github", "repo": "refhub-io/your-plugin-repo" },
  "version": "x.x.x"
}
```

the plugin repo must have `.claude-plugin/plugin.json` and a `skills/` directory at its root.

---

## // related

- [refhub-skill](https://github.com/refhub-io/refhub-skill) — agent skill for RefHub API-key workflows: vault and item management, import, search, export, vault audit, Semantic Scholar discovery/enrichment through `/semantic-scholar/*`, and item-scoped Google Drive PDF uploads after Drive is connected in the RefHub web UI. Small PDFs use the raw item route; larger vault-item PDFs use API-key `/pdf/session`, direct Drive `PUT` to the returned `upload_url`, then `/pdf/complete`. Account setup/admin flows such as API-key lifecycle, Google Drive connect/disconnect, and global audit remain browser/session-JWT workflows.
- [refhub-codex](https://github.com/refhub-io/refhub-codex) — Codex-native RefHub skill packaging backed by the same `@refhub/cli` execution layer.
- [refhub.io](https://refhub.io) — the platform
