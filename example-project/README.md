# example-project

A sample consumer project that uses **my-marketplace** and installs **my-first-plugin** (which ships `/my-skill`).

It shows the marketplace settings for both **Claude Code** and **GitHub Copilot CLI**.

```
example-project/
├── .claude/settings.json     # Claude Code — declarative marketplace + plugin enablement
└── .copilot/config.json      # Copilot CLI — installed-plugins format (reference)
```

## Claude Code (declarative)

`.claude/settings.json` is read automatically when you open the project. It both **registers** the marketplace and **enables** the plugin — no manual commands needed.

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

Open the folder in Claude Code and run `/my-skill`. To do it manually instead:

```bash
/plugin marketplace add easingthemes/ai-plugins-example
/plugin install my-first-plugin@my-marketplace
```

## GitHub Copilot CLI (command-driven)

Copilot CLI installs plugins via a command and records them in the **user-global** `~/.copilot/config.json` (auto-managed). There is no committed per-project marketplace file — `.copilot/config.json` here is included only to show the resulting format.

```bash
# Marketplace + plugin in one step (owner/repo/plugin)
/plugin install easingthemes/ai-plugins-example/my-first-plugin
```

After install, `~/.copilot/config.json` contains an `installedPlugins` entry like:

```jsonc
{
  "installedPlugins": [
    { "name": "my-first-plugin", "marketplace": "my-marketplace", "version": "1.0.0", "enabled": true }
  ]
}
```

Then run the skill the same way: `/my-skill`.

## Summary

| Platform | File | Mechanism |
|----------|------|-----------|
| Claude Code | `.claude/settings.json` (project) | Declarative — `extraKnownMarketplaces` + `enabledPlugins` |
| Copilot CLI | `~/.copilot/config.json` (user-global, auto-managed) | Command-driven — `/plugin install owner/repo/plugin` |
