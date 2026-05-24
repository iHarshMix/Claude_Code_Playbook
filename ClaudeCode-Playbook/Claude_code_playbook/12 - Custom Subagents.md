# 12 - Custom Subagents

> Custom subagents are tailor-made Claude instances for specialized, repeatable tasks — built when built-in subagents are too generic for your workflow.

---

## What It Is

A custom subagent is a Markdown file with a YAML front matter that defines a specialized Claude instance. You configure its name, tools, model, system prompt, and behavior. Claude Code reads that file and can invoke the subagent automatically or on demand.

Custom subagents live inside `.claude/agents/` — either at the project level (project-specific) or in your home directory (available across all projects).

> [!info] Added Context
> The distinction between built-in and custom subagents mirrors the difference between a general contractor and a specialist you hire for a specific job. Built-in subagents know how to explore code or write plans generically. Custom subagents know your codebase, your standards, and your checklist.

### Subagent file structure

```yaml
---
name: my-agent-name
description: When and why to invoke this agent (Claude uses this to auto-trigger)
tools:
  - Read
  - Edit
model: claude-sonnet-4-5
color: red
---

# Agent Instructions

Detailed instructions for what this agent does and how it should behave.
Include a system prompt here if needed.
```

Key YAML fields:

| Field | Purpose |
|-------|---------|
| `name` | Identifier used when referencing the agent |
| `description` | Tells Claude when to auto-trigger this agent |
| `tools` | Restrict to only the tools this agent needs |
| `model` | Can differ per agent (Opus for deep reasoning, Sonnet for speed) |
| `color` | Visual identifier in the observability dashboard |

---

## Why It Matters

Built-in subagents are generic. They know how to review code in the abstract — but they don't know your company's security checklist, your test framework conventions, or your API contract standards.

Custom subagents close that gap. You encode your project's specific requirements once, in the agent file, and every invocation applies them consistently — without repeating them in every prompt.

> [!note] From the Video
> "You create a tailor-made subagent that will do your task exactly the way you want it done."

The practical impact is a more reliable, predictable workflow. Instead of hoping Claude follows your conventions, you build an agent that enforces them.

---

## How to Use It

### Creating a custom subagent

**Option 1 — via Claude Code UI:**

Run `/agents` → Agents tab → Create New Agent → choose Project or Personal → describe what the agent does → configure tools and model.

Claude generates the Markdown file. Review it carefully before using it in production — generate it as a starting point, then edit.

**Option 2 — manually:**

Create a `.md` file directly in `.claude/agents/` and write the YAML front matter and instructions yourself. Faster once you know the format.

> [!tip] Best Practice
> After Claude generates an agent file, review it in a separate Claude or ChatGPT session — paste the file and describe your project. Ask whether the agent's instructions are appropriate for your specific codebase and workflow. Don't use a generated agent file blindly.

### Triggering custom subagents

**Auto-trigger:** Claude reads the `description` field of all agents in `.claude/agents/` and decides which one fits the current task. No instruction needed from you.

**Manual trigger:** Name the agent explicitly in your prompt.

```
Use the security-reviewer agent to audit the auth module.
```

**Via custom slash command:** Wire a subagent into a slash command so it triggers as part of a defined workflow (see example below).

### Building a multi-subagent workflow

The most powerful pattern: combine multiple subagents into a slash command that runs them in sequence or in parallel.

**Sequential example — testing pipeline:**

```markdown
## Steps

### Step 1 — Write Tests
Use the `test-writer` agent. Read the spec file at $ARGUMENTS.
Generate pytest test cases based on what the feature *should* do, not the implementation.

### Step 2 — Run Tests
Use the `test-runner` agent. Execute the tests written in Step 1.
Return a pass/fail summary with root cause notes for any failures.
```

**Parallel example — code review:**

```markdown
## Steps

### Step 1 — Parallel Review
Launch both agents simultaneously:
- `security-reviewer`: check for injection, auth bypass, exposed secrets
- `quality-reviewer`: check for best practices, naming, structure

### Step 2 — Unified Report
Merge both agents' findings into a single report with an overall verdict.
```

> [!tip] Best Practice
> Separate the agent that *writes* tests from the one that *runs* them. An agent that writes and runs its own tests tends to be biased toward passing them. Two agents with distinct roles produce more honest results.

---

## Best Practices

- Write the `description` field carefully — Claude uses it to decide when to auto-trigger the agent. Vague descriptions lead to wrong invocations or missed ones.
- Give each agent only the tools it actually needs. A test-writer needs Read and Edit; a test-runner needs Read and Bash but not Edit; an explorer needs Read only.
- Assign models deliberately: use Opus for agents doing complex planning or security analysis; use Sonnet for agents doing fast, pattern-based tasks like running tests.
- Build one agent per responsibility. Resist combining test-writing and test-running into a single agent — the separation keeps each agent's role clear and its results more reliable.
- Commit your `.claude/agents/` folder to version control. Subagent definitions are part of your project's tooling, not ephemeral config.

> [!tip] Best Practice
> Run your new agent on a small, known feature first before deploying it on critical code. Validate that its output matches your expectations before wiring it into a slash command workflow.

---

## Common Mistakes

> [!warning] Common Mistake
> Assigning parallel subagents to the same file. Concurrent writes to the same file cause conflicts. The main agent then has to manually reconcile the changes. Parallel subagents should own separate files or modules.

> [!warning] Common Mistake
> Trusting a Claude-generated agent file without reviewing it. Claude generates a reasonable starting point, but it doesn't know your codebase's conventions, your team's standards, or your edge cases. The file needs a human review before use.

> [!warning] Common Mistake
> Writing a vague system prompt. Phrases like "review the code carefully" give the agent no actionable criteria. Effective agent prompts specify exactly what to check, what to flag, and what format to return results in.

---

## To Explore Later

- Agent composition: chaining multiple slash commands across sessions (e.g., `/test-feature` → `/code-review-feature` → `/push`) as a fully automated release pipeline.
- Conditional agent dispatch: triggering different agents based on which files changed (e.g., security-reviewer only when auth files are modified).
- Shared agent libraries across teams: storing personal-scope agents in dotfiles and syncing them via version control.

---

*Related: [[11 - Subagents (Built-in)]]*
