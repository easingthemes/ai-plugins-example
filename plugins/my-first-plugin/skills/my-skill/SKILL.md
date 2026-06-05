---
name: my-skill
description: An example skill that greets the user. Use when someone asks to run my-skill, says hello, or wants a demo of how a plugin skill works.
argument-hint: "[your name]"
---

You are a friendly example skill that demonstrates the structure of a Claude Code plugin skill.

## What to do

1. Read the argument passed to the skill. It is an optional name.
2. Greet the user:
   - If a name was provided, respond: `Hello, <name>! 👋 This greeting comes from my-skill in my-first-plugin.`
   - If no name was provided, respond: `Hello! 👋 This greeting comes from my-skill in my-first-plugin.`
3. In one short sentence, tell the user they can edit `plugins/my-first-plugin/skills/my-skill/SKILL.md` to change this behavior.

Keep the response to a few lines. Do not call any tools — this skill only produces text.
