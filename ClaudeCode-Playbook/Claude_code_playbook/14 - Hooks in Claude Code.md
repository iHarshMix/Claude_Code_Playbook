# 14 - Hooks in Claude Code

> Hooks are scripts you write that Claude Code runs automatically at specific moments in its lifecycle — adding a layer of deterministic, guaranteed behavior on top of a probabilistic LLM.

---

## What It Is

To understand hooks, you first need to understand what Claude Code actually is at a system level.

Claude Code is a **coding harness** — a software layer built on top of the Claude LLM that converts raw model intelligence into a reliable engineering system. The harness handles file reading, terminal output, conversation history, context window tracking, API calls to Anthropic, tool execution, permission requests, memory management, and subagent spawning. The LLM provides the thinking; the harness executes the actions.

Within every session, Claude works through an **agent loop**: it receives a task, decides on a tool call, the harness executes it, returns the result, the model decides the next step, and this continues until the task completes. This loop nests inside a **session lifecycle** — from the moment you type `claude` to the moment you type `exit`.

The lifecycle produces predictable events: `session_start`, `pre_tool_use`, `post_tool_use`, `stop`, `session_end`, `subagent_start`, `subagent_stop`, and others.

**Hooks are scripts attached to these events.** Whenever a configured event fires, the harness runs your script automatically — before proceeding.

> [!info] Added Context
> The LLM is the brain; the coding harness is the nervous system and body that turns thoughts into actions. Hooks let you intercept that nervous system at specific moments and enforce rules the brain might occasionally forget.

---

## Why It Matters

The LLM is probabilistic — the same context doesn't always produce the same output. Instructions in `CLAUDE.md` are followed 98% of the time, but in long sessions with complex tasks or a full context window, the model can override or forget them. That 2% failure rate is acceptable for style preferences but dangerous for production code.

Examples of what that 2% looks like:
- Claude decides to delete a file it considers redundant (including your database)
- Claude edits `.env` when reorganizing the project
- Claude writes f-string SQL queries instead of parameterized ones
- Claude applies a scaler to test data, causing data leakage

Hooks solve this by introducing **determinism**. A hook is software — it runs 100% of the time, every time, regardless of what the LLM decides. You can't hallucinate past a hook.

---

## How to Use It

### Hook configuration file

Hooks live in `.claude/settings.json`. Each hook entry has three parts:

```json
{
  "hooks": [
    {
      "event": "pre_tool_use",
      "matcher": "Bash",
      "action": {
        "type": "command",
        "command": "python3 /path/to/your/script.py"
      }
    }
  ]
}
```

| Field | What it does |
|-------|-------------|
| `event` | Which lifecycle event triggers this hook |
| `matcher` | Optional filter — only fire when this tool is involved (e.g. `Bash`, `Write`, `Edit`) |
| `action` | The script or command to run |

### Exit codes: the hook's language

Your hook script communicates back to the harness through its exit code:

| Exit code | Meaning |
|-----------|---------|
| `0` | All clear — proceed with the tool call |
| `2` | Block — abort this operation, send the error message to the LLM |

When exit code 2 fires, Claude Code stops the tool call and sends your script's printed output as context to the model, so the LLM understands why it was blocked and can self-correct.

### Hook data: what your script receives

The harness passes a JSON payload via stdin to your hook script. It contains the tool name and its input parameters — enough to inspect what Claude is about to do.

```python
import json, sys

data = json.load(sys.stdin)
tool_input = data.get("tool_input", {})
command = tool_input.get("command", "")

# Example: block deletion of a protected file
protected = ["spendly.db", ".env"]
if any(f in command for f in protected) and "rm" in command:
    print("BLOCKED: Cannot delete protected file.")
    sys.exit(2)

sys.exit(0)
```

### Common hook patterns

**Auto-formatting (post_tool_use, Write/Edit):**
```json
{
  "event": "post_tool_use",
  "matcher": "Write|Edit",
  "action": {
    "type": "command",
    "command": "black $CLAUDE_FILE_PATH"
  }
}
```

**Protecting sensitive files (pre_tool_use, Bash):**
```json
{
  "event": "pre_tool_use",
  "matcher": "Bash",
  "action": {
    "type": "command",
    "command": "python3 .claude/hooks/block_dangerous.py"
  }
}
```

---

## Best Practices

- Set up hooks at the **start** of a project, not after problems emerge. They're safeguards — they work best when established before the codebase grows.
- Use `pre_tool_use` with `Bash` matcher for blocking dangerous operations (file deletion, env edits, unsafe SQL patterns).
- Use `post_tool_use` with `Write|Edit` matcher for formatting and linting — run after Claude writes, so every generated file meets your standards automatically.
- Keep hook scripts simple and fast. A hook that takes 3 seconds runs on every tool call and will noticeably slow down your session.
- Version-control your `.claude/settings.json`. Hooks are part of your project's safety infrastructure, not personal config.

> [!tip] Best Practice
> Use the `session_start` event to auto-generate a project status summary whenever you open a new session: what features are complete, what's in progress, what's next. This eliminates the "getting back up to speed" cost at the start of each work session.

> [!tip] Best Practice
> Domain-specific hooks are more valuable than generic ones. A data science project should have hooks blocking `df.dropna()` without column names, or `fit()` calls on test data. A web app should block f-string SQL. Tailor your hooks to the actual failure modes in your domain.

---

## Common Mistakes

> [!warning] Common Mistake
> Relying on `CLAUDE.md` instructions alone for safety-critical rules. Instructions are probabilistic — they can be overridden under pressure. If a rule must hold 100% of the time, it belongs in a hook, not a text instruction.

> [!warning] Common Mistake
> Using an overly broad matcher (or no matcher) on a `pre_tool_use` hook. A hook with no matcher fires on every single tool call — including reads — which adds unnecessary overhead. Always narrow with a matcher to the tool types that actually need the check.

> [!warning] Common Mistake
> Writing hook scripts that silently fail. If your Python script has a syntax error, it exits with code 1 (not 0, not 2) — the harness may treat this as "proceed" rather than "block." Always test your hook scripts independently before connecting them.

---

## To Explore Later

- The `agents-observe` library: a real-time observability dashboard for subagents, built entirely on hooks (`subagent_start`, `subagent_stop` events). Good reference for what hooks can produce.
- Notification hooks: connecting a push notification service (e.g., ntfy.sh) to the `stop` event so your phone alerts you when a long-running task completes.
- Telemetry hooks: logging tool calls and timing data to a local file to understand where Claude spends most of its token budget in complex sessions.

---

*Related: [[11 - Subagents (Built-in)]], [[06 - CLAUDE.md - Instructing the Agent]]*
