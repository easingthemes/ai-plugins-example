# example-project

A sample consumer project that uses **my-marketplace** and enables **my-first-plugin** (which ships `/my-skill`) — scoped to *this project only*.

Both Claude Code and GitHub Copilot CLI use the **same declarative keys** (`extraKnownMarketplaces` + `enabledPlugins`); only the file location differs.

```
example-project/
├── .claude/settings.json            # Claude Code  — project-level marketplace + plugin
└── .github/copilot/settings.json    # Copilot CLI  — project-level marketplace + plugin
```

## Enable a plugin only in this project

### Claude Code — `.claude/settings.json`

```jsonc
{
  "extraKnownMarketplaces": {
    "my-marketplace": {
      "source": { "source": "github", "repo": "easingthemes/ai-plugins-example" },
      "autoUpdate": true
    }
  },
  "enabledPlugins": {
    "my-first-plugin@my-marketplace": true
  }
}
```

### Copilot CLI — `.github/copilot/settings.json`

```jsonc
{
  "extraKnownMarketplaces": {
    "my-marketplace": {
      "source": { "source": "github", "repo": "easingthemes/ai-plugins-example" }
    }
  },
  "enabledPlugins": {
    "my-first-plugin@my-marketplace": true
  }
}
```

Open the project in either tool and run `/my-skill`.

## Copilot CLI settings precedence

Settings cascade lowest → highest; a repo-level key overrides the user-level value for the same key:

| Scope | File | Committed? |
|-------|------|-----------|
| User-global | `~/.copilot/settings.json` | no (your machine) |
| **Project (shared)** | `.github/copilot/settings.json` | **yes** |
| Project (personal) | `.github/copilot/settings.local.json` | no — add to `.gitignore` |
| Per-invocation | CLI flags (`--allow-tool`, …) | n/a |

> Note: `~/.copilot/config.json` is a *separate, auto-managed* file (trusted dirs, installed-plugin cache). Don't hand-edit it — put your declarative config in `settings.json`.
> Caveat: as of mid-2026 some Copilot CLI versions don't *auto-install* a plugin from `enabledPlugins` if it isn't downloaded yet (github/copilot-cli#2249). If `/my-skill` doesn't appear, run `/plugin install easingthemes/ai-plugins-example/my-first-plugin` once; `enabledPlugins` then controls on/off per project.

## Manual install (either tool)

```bash
# Claude Code
/plugin marketplace add easingthemes/ai-plugins-example
/plugin install my-first-plugin@my-marketplace

# Copilot CLI (marketplace + plugin in one step)
/plugin install easingthemes/ai-plugins-example/my-first-plugin
```
