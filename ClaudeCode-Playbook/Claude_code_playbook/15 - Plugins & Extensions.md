# 15 - Plugins & Extensions

> Plugins are distributable packages of your Claude Code customizations — skills, agents, hooks, slash commands, and MCP servers bundled together so your workflow can be shared, replicated, and installed by anyone in one step.

---

## What It Is

Everything you build in Claude Code — skills, custom subagents, hooks, custom slash commands, MCP server configurations — lives in scattered files across your `.claude/` folder. Plugins are the packaging format that bundles all of that into a single, installable unit.

A plugin is a folder with a specific structure. Anyone who installs it gets an exact replica of your workflow configuration, without manual copying or setup.

> [!note] From the Video
> "A plugin is a place where you put everything you've created — skills, MCP tools, hooks, custom commands — in one folder, and you distribute it. The moment someone installs that package, an exact replica of your workflow is created on their machine."

### Plugin folder structure

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json          ← required manifest file
├── skills/
│   └── eda-skill.md
├── agents/
│   └── test-runner.md
├── commands/
│   └── model-eval.md
├── hooks/
│   └── block_unsafe.py
└── mcp.json                 ← MCP server config
```

The `.claude-plugin/plugin.json` manifest is mandatory. Without it, Claude Code does not recognize the folder as a valid plugin.

### plugin.json format

```json
{
  "name": "data-science-workflow",
  "version": "1.0.0",
  "description": "Credit risk modeling workflow for fintech teams",
  "author": "your-name",
  "repository": "https://github.com/yourname/plugin-repo",
  "license": "MIT"
}
```

---

## Why It Matters

Individual customizations are powerful but siloed. A senior engineer who has spent months refining their Claude Code workflow — domain-specific skills, safety hooks, evaluation commands, MCP integrations — has no easy way to share that setup with new team members.

Without plugins, sharing means: "copy this skill file here, this hook config there, manually edit your settings.json, add these MCP servers." That process breaks, loses pieces, and doesn't update when the original workflow changes.

Plugins collapse all of that into a single install command. New team members get the full, working workflow immediately. When the workflow improves, it can be updated and reinstalled.

> [!info] Added Context
> The analogy from the video is exact: plugins are to Claude Code what apps are to an app store. A marketplace is the store; a plugin is the app. You browse, install, and get the capability — without understanding how it was built.

---

## How to Use It

### Installing plugins from the official marketplace

The official Anthropic marketplace is pre-installed. Browse and install:

```
/plugin → Discover
```

Select any plugin and install it. No marketplace setup needed.

### Adding a third-party marketplace

```
/plugin → Marketplaces → Add Marketplace
```

Paste the GitHub repository URL of the marketplace. It must contain a `.claude-plugin/marketplace.json` file. Once added, its plugins appear in Discover alongside the official ones.

### Installing a specific plugin via command

```bash
claude plugin install <plugin-name>
```

When prompted, choose scope:
- **User scope** — available across all your projects
- **Project scope** — available only in the current repo

### Creating your own plugin

1. Create a folder with the structure shown above.
2. Add `.claude-plugin/plugin.json` with your manifest.
3. Place your skills in `skills/`, agents in `agents/`, hooks in `hooks/`, commands in `commands/`.
4. Push to a GitHub repo.
5. Share the repo URL — others install it by adding your repo as a marketplace or directly installing the plugin.

### Publishing to a marketplace

Create a GitHub repo containing `.claude-plugin/marketplace.json`:

```json
{
  "name": "My Team Marketplace",
  "owner": "team-name",
  "plugins": [
    {
      "name": "data-science-workflow",
      "repository": "https://github.com/team/ds-plugin"
    },
    {
      "name": "backend-workflow",
      "repository": "https://github.com/team/backend-plugin"
    }
  ]
}
```

---

## Best Practices

- Build your plugin incrementally: start with the skills and slash commands that are already working, then add hooks and MCP config once those are stable.
- Version your plugin semantically. Breaking changes (removing a tool, renaming a command) should increment the major version.
- Write a clear `description` in `plugin.json`. This is what users see in the Discover tab — it needs to communicate what workflow the plugin supports.
- For team plugins: store the plugin repo in the same organization as your codebase and require it in your project's setup documentation, so new team members run one install step during onboarding.

> [!tip] Best Practice
> Treat your plugin as a living document of your team's best practices for AI-assisted development. When you discover a new hook pattern that prevents a class of mistakes, add it to the plugin. When a custom command becomes standard practice, include it. The plugin should reflect how your team actually works.

> [!tip] Best Practice
> Don't install every plugin that looks interesting. Plugins add MCP servers and skills to your context. Too many installed plugins degrade performance the same way too many MCP servers do — each one loads tool descriptions into your context window at session start.

---

## Common Mistakes

> [!warning] Common Mistake
> Forgetting the `.claude-plugin/plugin.json` manifest. The folder structure can be perfect, but without this file Claude Code does not treat it as a valid plugin. The manifest is not optional.

> [!warning] Common Mistake
> Installing plugins at the wrong scope. A deployment plugin for a specific project should be project-scoped, not user-scoped. Installing it user-scoped means it appears in every project, loading irrelevant tool descriptions every session.

> [!warning] Common Mistake
> Distributing a plugin without testing a clean install. Skills, hooks, and MCP configs have path dependencies that can break on a different machine. Always do a clean install on a second machine (or a fresh directory) before sharing.

---

## To Explore Later

- Building a private team marketplace: a GitHub repo your organization controls, versioned, with access controls, that serves as the canonical source of approved Claude Code workflows.
- Plugin composition: installing multiple plugins and managing conflicts when two plugins define hooks for the same event or commands with the same name.
- Useful plugins from the official marketplace: `superpower` (general software development workflow), `context7` (live library docs), `code-simplifier` (readability improvements), `playwright` (browser automation), `skill-creator` (building new skills inside Claude Code).

---

*Related: [[13 - MCP (Model Context Protocol)]], [[10 - Claude Code Skills]], [[12 - Custom Subagents]]*
