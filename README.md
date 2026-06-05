# ai-plugins-example

A minimal example of a **Claude Code plugin marketplace** with one plugin and one skill.

## Structure

```
ai-plugins-example/
├── .claude-plugin/
│   └── marketplace.json          # my-marketplace — lists available plugins
├── plugins/
│   └── my-first-plugin/
│       ├── .claude-plugin/
│       │   └── plugin.json        # plugin manifest
│       └── skills/
│           └── my-skill/
│               └── SKILL.md       # the skill itself
└── README.md
```

| File | Purpose |
|------|---------|
| `.claude-plugin/marketplace.json` | Marketplace manifest (`my-marketplace`). Points at each plugin via a relative `source` path. |
| `plugins/my-first-plugin/.claude-plugin/plugin.json` | Plugin manifest. **Do not** add `skills`/`agents` fields when using the default `skills/`+`agents/` directories — they're auto-discovered, and listing them breaks Claude Code validation. |
| `plugins/my-first-plugin/skills/my-skill/SKILL.md` | A skill: Markdown with YAML frontmatter (`name`, `description`) and instructions in the body. |

## Try it

```bash
# 1. Add this marketplace (use the repo URL or a local clone path)
/plugin marketplace add easingthemes/ai-plugins-example

# 2. Install the plugin
/plugin install my-first-plugin@my-marketplace

# 3. Run the skill
/my-skill Dragan
```

## How it fits together

1. Claude Code reads `marketplace.json` to learn which plugins exist.
2. Installing `my-first-plugin` registers its `plugin.json`.
3. Skills in `skills/*/SKILL.md` are auto-discovered and exposed as `/<skill-name>` commands.

Edit `SKILL.md` to change what the skill does — no build step required.

## License

MIT
