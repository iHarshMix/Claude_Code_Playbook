# 06 - CLAUDE.md - Instructing the Agent

> A persistent instruction file that tells Claude Code how to behave across all sessions — the closest thing to a memory system Claude Code has.

---

## What It Is

`CLAUDE.md` is a Markdown file that Claude Code automatically reads at the start of every new session. It lives in your project directory and acts as a persistent system prompt — project context, coding conventions, preferred tools, and critical constraints, all loaded without you having to re-explain anything.

> [!note] From the Video
> "CLAUDE.md is basically a special project-level instruction file used by Claude Code to guide how it behaves while working on your codebase. You can think of it as a persistent system prompt."

It is not magic — it is just a Markdown file. Its power comes from being read automatically every session.

---

## Why It Matters

LLMs have no memory across sessions. Every time you start a new Claude Code session, it has zero context about your project. Without `CLAUDE.md`, you repeat the same explanations every time — your tech stack, naming conventions, build commands, what not to touch. This is both tedious and error-prone: miss one detail, and Claude generates inconsistent or broken code.

`CLAUDE.md` solves this by front-loading the context once. Every subsequent session starts informed.

---

## How to Use It

### Creating the file

Two approaches:

- **Manual** — create `CLAUDE.md` in your project root and write the contents yourself.
- **`/init` command** — run `/init` inside Claude Code and it will scan your codebase, analyse key config files (`package.json`, `requirements.txt`, `README`), and generate a starting `CLAUDE.md` for you.

> [!tip] Best Practice
> Always start with `/init`, then edit the result. The generated file covers roughly 30% of what you need — the structural skeleton. The remaining 70% (workflows, constraints, naming conventions, what to avoid) is yours to fill in.

### What to include

A well-structured `CLAUDE.md` covers these sections:

- **Project overview** — one precise line describing what the project is and does.
- **Architecture** — where things live: which folder holds routes, services, schemas, etc.
- **Coding style** — type hints, model conventions, function size expectations.
- **Preferred libraries and tools** — what Claude is allowed to use. Naming tools here prevents Claude from introducing unwanted dependencies.
- **Commands** — exact commands to install, run, test, and deploy the project.
- **Critical rules** — things Claude must never do (e.g. "do not modify `database.py` unless explicitly asked").
- **Development roadmap** (optional) — a list of planned features with status markers. Keeps Claude oriented across many sessions.

### Where to put it

`CLAUDE.md` can live in several places, each with different scope:

| Location | Loaded when | Shared with team |
|---|---|---|
| Project root (`/CLAUDE.md`) | Every session, automatically | Yes (via git) |
| `.claude/CLAUDE.md` | Every session, automatically | Yes (via git) |
| `CLAUDE.local.md` in project root | Every session, automatically | No (git-ignored) |
| `~/.claude/CLAUDE.md` (home directory) | Every session, all projects | No |
| Subfolder `CLAUDE.md` | Only when Claude works in that folder | Yes (via git) |

> [!info] Added Context
> The `.claude/` folder is Claude Code's configuration directory — it also holds custom slash commands, skills, and subagents. Think of it as Claude Code's toolbox for a project. There is a project-level version (inside your repo) and a global version (in your home directory, applies to all projects).

---

## Best Practices

- Keep `CLAUDE.md` under 200 lines. Instruction-following quality degrades as the file grows. If a line's removal wouldn't cause Claude to make mistakes, remove it.
- Mark genuinely critical lines with `IMPORTANT:` — but use it sparingly. If everything is marked important, nothing is.
- Use the `rules/` subfolder inside `.claude/` to split a large `CLAUDE.md` into topic-specific files (`code-style.md`, `security.md`, `api-conventions.md`). These load lazily — only when Claude needs them — which keeps the upfront context lean.
- You can also use `@import` syntax inside `CLAUDE.md` to reference separate files, similar to imports in code.
- Treat `CLAUDE.md` as a living document. Update it after every significant feature — add new patterns, remove outdated ones, commit the change.
- When Claude repeats the same mistake across sessions, codify the fix: tell Claude the correction, then ask it to add the rule to `CLAUDE.md`.
- Audit `CLAUDE.md` periodically (weekly or monthly). Instructions drift — what was relevant at project start may contradict current patterns.

---

## Common Mistakes

> [!warning] Common Mistake
> Writing `CLAUDE.md` once at project start and never touching it again. The file should evolve with the project. Stale instructions are worse than no instructions — they actively mislead Claude.

> [!warning] Common Mistake
> Overusing `IMPORTANT:`. Marking ten things as important signals nothing. Reserve it for true constraints like "never auto-generate IDs" or "do not touch the auth middleware."

> [!warning] Common Mistake
> Putting feature-specific or one-off instructions in `CLAUDE.md`. It should contain only what is universally true for the project. Temporary or scoped instructions belong in the session prompt, not the persistent file.

---

## To Explore Later

- Auto Memory (`memory.md`) — Claude Code's counterpart to `CLAUDE.md`. While `CLAUDE.md` is written by you, `memory.md` is written by Claude as it observes patterns in your sessions. Both are loaded at session start. See [[11 - Subagents (Built-in)]] for context on how Claude manages state across tasks.

---

*Related: [[07 - Spec-Driven Development]] · [[05 - Context Window Management]]*
