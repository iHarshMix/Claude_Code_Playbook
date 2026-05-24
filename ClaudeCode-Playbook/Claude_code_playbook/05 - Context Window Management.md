# 05 - Context Window Management

> The context window is Claude's working memory — understanding its limits and managing it deliberately is what separates reactive usage from controlled, production-grade agentic coding.

---

## What It Is

The context window is the maximum amount of information (measured in tokens) that Claude can hold and reason over at one time while generating a response. Think of it as working memory: everything the model can see right now.

In a Claude Code session, the context window includes:
- Your messages and Claude's replies
- File contents that were read or written
- Tool outputs (bash results, web search results, etc.)
- The system prompt, tool schemas, `CLAUDE.md` contents, and auto-compaction buffer — all pre-loaded before you type a single message

> [!note] From the Video
> "The context window is the amount of information in tokens that a model like Claude Code can see and remember at one time while generating a response. Think of it as the model's working memory."

---

## Why It Matters

Three reasons context management is non-negotiable:

**Cost.** Token usage maps directly to what you pay. Context bloat means paying for history that isn't helping the current task.

**Workflow shape.** How you structure sessions determines how fast you hit limits. One feature per session is not just a style preference — it's a cost and quality multiplier.

**Response quality.** As the context window fills, Claude's output quality degrades. A 130K-token session produces noticeably weaker responses than a 30K-token session working on the same task.

---

## How to Use It

### Actual usable context: ~150K tokens

The nominal limit for Sonnet models is 200K tokens. In practice, ~50K is pre-occupied at session start:

| Pre-loaded component | Approx. tokens |
|---------------------|---------------|
| System prompt | ~6,000 |
| Tool schemas | ~8,000 |
| Auto-compaction buffer (reserved) | ~33,000 |
| CLAUDE.md, memory files, MCP schemas | varies |

You work with roughly 150K usable tokens. Plan accordingly.

### Why sessions grow faster than expected

Every time you send a message, Claude receives the full conversation history again — it has no persistent memory between turns. So token consumption is cumulative and quadratic:

- Turn 1: sends 1 unit → receives 1 unit → 2 units consumed
- Turn 2: sends 2 units of history + 1 new → receives 1 → 4 units consumed
- Turn 10: you've consumed ~20 units just on quadratic history overhead

Claude's replies also run roughly 6x larger than your input messages (tool calls, code diffs, explanations). The math compounds fast.

> [!info] Added Context
> Running four features in one long session consumes roughly 4x the tokens compared to running each feature in its own session. This is not an estimate — it's the direct consequence of quadratic history accumulation.

### Monitoring context: `/context`

```
/context
```

Shows a live breakdown of what's filling your context window right now. Run this periodically during a session, not just when you suspect a problem.

### Manual compaction: `/compact`

```
/compact
```

Summarizes your full conversation history and stores the compressed version in the auto-compaction buffer (the reserved 33K tokens). Frees up history-consumed space so you can continue without starting a new session.

> [!note] From the Video
> "Don't let Claude auto-compact. Do it yourself. Auto-compaction can trigger in the middle of an important task and lose details from your conversation that matter for the feature being built."

Run `/compact` proactively when you hit ~70–75% of your usable context — not reactively when quality has already degraded.

### When compaction is exhausted: `/clear` or new session

If the 33K compaction buffer is also full, you have two options:
- `/clear` — wipes conversation history, restarts within the same session
- Start a new session — cleaner, preferred

> [!info] Added Context
> `/clear` and starting a new session are functionally similar. The practical difference: a new session gives you a clean, named entry in your session history, which is better for traceability.

### Sub-agents for isolation

Each sub-agent gets its own fresh 200K context window, completely separate from the main agent's. For tasks that can be parallelized or isolated, sub-agents are the highest-leverage tool for context management. Covered in [[11 - Subagents (Built-in)]].

---

## Best Practices

- One session per feature. Start a new session when you start a new feature — not when the old one breaks.
- Run `/context` periodically, not just at crisis point. Treat it like a fuel gauge.
- Run `/compact` manually at ~70–75% usage, between tasks — never mid-feature.
- Write focused, specific prompts. Vague instructions generate verbose responses that consume more context than precise ones.
- Use sub-agents for any isolated or parallelizable work — they don't touch your main context window.
- Add a `.claudeignore` file (like `.gitignore`) to exclude large build artifacts, `venv` directories, and generated files from Claude's view.

> [!tip] Best Practice
> Commit before you compact. Compaction is lossy — some detail from the conversation is always lost in the summary. A git commit ensures your working code is safe before you compress the context.

> [!tip] Best Practice
> A clean, small context window produces better code than a large, stale one. When in doubt, start fresh.

---

## Common Mistakes

> [!warning] Common Mistake
> Relying on auto-compaction. It triggers mid-task, at moments you don't control, and can drop details that matter for the feature in progress. Manual `/compact` between tasks is always safer.

> [!warning] Common Mistake
> Building multiple features in one session. Feels faster — actually costs 4x more tokens and degrades quality as the session grows long.

> [!warning] Common Mistake
> Ignoring context until quality visibly drops. By then you've already wasted tokens on degraded responses. Check `/context` proactively.

> [!warning] Common Mistake
> Treating `/context` as an emergency tool. It should be a routine check after each completed task, like checking git status.

---

## To Explore Later

- Sub-agents for isolated context windows and parallel task execution: [[11 - Subagents (Built-in)]]
- `.claudeignore` — excluding large files from context load (behaviour still maturing as of May 2026)
- Cost optimization at scale — session strategy for large codebases with many parallel features

---

*Related: [[03 - Slash Commands]], [[11 - Subagents (Built-in)]]*
