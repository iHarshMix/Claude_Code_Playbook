# 03 - Slash Commands

> Typed shortcuts that trigger predefined workflows inside a Claude Code session — no full prompt needed.

---

## What It Is

Slash commands are shorthand triggers you type at the start of any input, prefixed with `/`. Instead of writing out a full prompt to perform a repetitive action, a single command invokes the entire workflow instantly.

There are two types:

- **Built-in commands** — shipped with Claude Code, available immediately after installation.
- **Custom commands** — created by you for your own repeating workflows. Covered in [[09 - Custom Slash Commands]].

> [!note] From the Video
> "Slash commands are shortcuts you type inside a Claude Code session, starting with `/`, that trigger a specific predefined action or workflow instantly — without writing out a full prompt."

---

## Why It Matters

Every AI interaction normally requires a prompt. Claude Code's developers noticed that programmers repeat a fixed set of actions constantly — compressing context, switching models, checking usage, exporting sessions. Slash commands replace those repeated prompts with a single word.

Without them, every context management or session operation would require writing and re-writing natural language instructions — noisy, error-prone, and slow.

---

## How to Use It

Type `/` anywhere in the Claude Code input, then scroll through the autocomplete list with arrow keys. Each command shows a description inline.

### Core built-in commands

| Command | What it does |
|---------|-------------|
| `/exit` | Ends the current session |
| `/resume` | Switches to a different past session mid-conversation |
| `/rename <name>` | Renames the current session |
| `/export <filename.md>` | Saves the full conversation to a file in the project directory |
| `/btw <question>` | Asks a one-off question that does not become part of conversation history |
| `/model` | Switches the active model (Opus / Sonnet / Haiku) |
| `/usage` | Shows token usage for the current session and weekly limit |
| `/compact` | Manually compresses conversation history to free context space (see [[05 - Context Window Management]]) |
| `/clear` | Wipes conversation history entirely within the current session |
| `/context` | Shows a breakdown of what is currently filling the context window |
| `/permissions` | Opens the tool permission manager (allow / ask / deny per tool) |
| `/config` | Opens Claude Code configuration (thinking mode, verbosity, language) |
| `/logout` / `/login` | Switches accounts |
| `/stats` | Usage statistics across all sessions |
| `/insights` | Generates an HTML report with usage patterns and improvement suggestions |
| `/theme` | Changes the terminal colour theme |
| `/voice` | Enables voice input mode (hold space to speak) |

### Resuming sessions from outside

```bash
claude -r
```
Opens a list of past sessions to resume. Select with arrow keys and enter.

### /btw in practice

Use `/btw` when a tangential question comes up mid-task. The answer is shown inline but never appended to conversation history — keeping the main context clean.

```
/btw what does the __init__ method do in Python?
```
Press space to dismiss the answer. It disappears from the thread.

### /permissions in practice

Navigate to Allow → Add a new rule → type the tool name or bash command.

Three scope options when saving:
- Local project — applies only to you in this project
- Global project — applies to everyone who clones/forks the repo
- User — applies to you across all projects on this machine

```
# Example: always allow web search without asking
Allow: WebSearch

# Example: always allow git init without asking
Allow: Bash(git init)
```

> [!warning] Common Mistake
> Adding unsafe or irreversible bash commands to the Allow list. Only grant permanent permission to commands you'd run without thinking. Destructive operations (file deletion, force pushes) should always stay on Ask.

---

## Best Practices

- Rename every new session immediately after creating it — before the AI auto-names it from your first message.
- Use `/btw` for any quick lookup or side question. Don't pollute the main context with tangential exchanges.
- Check `/usage` after each feature is done. Stay aware of where you are before the limit surprises you.
- Export key sessions before major refactors so you can provide the conversation as context later.

> [!tip] Best Practice
> Keep a habit: rename → work → commit → check usage. That four-step rhythm per feature keeps sessions clean and usage visible.

> [!info] Added Context
> The model selector matters for cost. Opus burns tokens at a much higher rate than Sonnet. A common workflow: use Opus for planning and architecture decisions, switch to Sonnet for implementation. The `/model` command makes this switch instant.

---

## Common Mistakes

> [!warning] Common Mistake
> Letting the AI name your session. Auto-generated names are based on your first message and are usually meaningless. Rename immediately with `/rename <feature-name>`.

> [!warning] Common Mistake
> Treating `/clear` and starting a new session as equivalent. `/clear` wipes history inside the same session. A new session gives a genuinely fresh context window. Prefer new sessions when starting a new feature.

---

## To Explore Later

- Custom slash commands — building your own reusable prompt shortcuts: [[09 - Custom Slash Commands]]
- `/insights` report — worth running after 10–15 sessions to understand your own usage patterns

---

*Related: [[05 - Context Window Management]], [[09 - Custom Slash Commands]]*
