# 11 - Subagents (Built-in)

> Subagents are isolated Claude instances with their own context windows — they do heavy work in a separate space and return only what the main agent needs, solving the context explosion problem.

---

## What It Is

When you interact with Claude Code, you are talking to the **main agent**. That main agent can spawn **subagents** — separate Claude instances, each with a fresh context window — to handle specific tasks. When a subagent finishes, it returns only its result to the main agent, then its context is discarded.

> [!info] Added Context
> Subagents work like functions in programming: you don't care what happens inside, only what comes out. The main agent delegates, gets a result, and moves on — without carrying the subagent's work in its own context.

Claude Code ships with three built-in subagent types:

| Subagent | Triggered When |
|----------|---------------|
| **Explore** | Claude needs to read/analyze the codebase |
| **Plan** | Claude generates an implementation plan (plan mode) |
| **General Purpose** | Claude needs to perform a read or write task in isolation |

---

## Why It Matters

Without subagents, every turn of a long conversation carries the full conversation history — including any large files loaded early on. This causes two compounding problems.

**Context window overflow** — a 30,000-token codebase loaded in turn 1 gets re-sent in every subsequent turn. By turn 8, a single API call can exceed 76,000 tokens.

**Lost-in-the-middle effect** — when context fills up, LLMs tend to under-weight information in the middle of the window. Quality degrades as the conversation grows.

Subagents break this pattern. The codebase is loaded once inside the subagent, analyzed, and a compact summary (e.g., 500 tokens) is returned to the main agent. The main agent carries only that summary going forward — not the raw files.

> [!note] From the Video
> "Subagents are specialized AI assistants that run in their own isolated context windows — doing heavy lifting in a separate space and handing back only what matters."

---

## How to Use It

### Implicit triggering (automatic)

Claude Code recognizes when a task warrants a subagent and spawns one without being told. When you ask Claude to explore your codebase, the Explore subagent fires automatically. You don't need to ask for it.

### Explicit triggering (manual)

You can instruct Claude to use a subagent directly in your prompt. Useful when you want to force isolation for a specific task.

```
Use a subagent to analyze the auth module and return a summary.
```

### Requesting parallel subagents

When tasks are independent of each other, you can ask Claude to split the work across multiple subagents running simultaneously.

```
Implement the following three features in parallel using separate subagents:
- Subagent 1: summary stats section
- Subagent 2: recent transactions table
- Subagent 3: category breakdown chart
```

> [!warning] Common Mistake
> Don't assign parallel subagents to the same file. Concurrent writes cause conflicts that the main agent then has to resolve manually. Parallel subagents work best when each one owns a separate file or module.

### Checking context usage

Run `/context` before and after a subagent-heavy task to confirm how little of the main context was consumed compared to loading files directly.

---

## Best Practices

- Let Claude trigger subagents implicitly where possible — it usually makes the right call.
- Use explicit triggering when you need to control isolation deliberately (e.g., for code review or security audit tasks).
- Reserve parallel subagents for tasks that are genuinely independent — different files, different services, different datasets.
- Treat the subagent's returned summary as the source of truth going forward. Don't ask Claude to re-load the original files.

> [!tip] Best Practice
> After any major codebase exploration via subagent, use `/compact` rather than continuing the session raw. The subagent already summarized the codebase; compacting the main context keeps the session lean from that point on.

---

## Common Mistakes

> [!warning] Common Mistake
> Assuming subagents are free. Each subagent call consumes tokens — it just does so in an isolated context. The savings come from not re-sending that data in every subsequent main-context turn, not from avoiding token costs entirely.

> [!warning] Common Mistake
> Using subagents for tasks that don't need isolation. If a task is small and self-contained, spawning a subagent adds overhead without benefit. Reserve them for heavy lifting — large file reads, multi-file analysis, parallel workstreams.

---

## To Explore Later

- Real-time subagent observability: the `agents-observe` library (uses Hooks) shows which subagent is running and what tools it's invoking — useful for debugging complex multi-agent flows.
- How Claude internally decides to spawn multiple Explore subagents for a single planning task (observed in the video: two Explore subagents fired before one Plan subagent).

---

*Related: [[12 - Custom Subagents]]*
