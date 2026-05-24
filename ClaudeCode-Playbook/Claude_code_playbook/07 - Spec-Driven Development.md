# 07 - Spec-Driven Development

> Writing a detailed specification before any code is written — the practice that separates structured agentic coding from uncontrolled vibe coding.

---

## What It Is

Spec-Driven Development (SDD) is an approach where you produce a written specification document before asking Claude Code to write a single line of code. The spec acts as the single source of truth for what the feature must do — Claude codes from it, not from an open-ended prompt.

> [!note] From the Video
> "Spec-Driven Development is a software development approach where a detailed specification document is written before any code is written. The spec acts as a single source of truth for what the system should do, and all development flows from it."

The spec constrains Claude to your decisions. It does not make decisions for Claude.

---

## Why It Matters

In vibe coding, you hand Claude a loose prompt ("build me a login system") and Claude fills in every unanswered question itself — which framework, which auth method, which password rules, what happens on three failed attempts. The answers it picks may not match what you want. You then iterate through corrections, which is slow and produces inconsistent code.

Spec-Driven Development inverts this. You answer the critical questions upfront, in writing. Claude's job becomes execution, not design. The result is more predictable code with fewer correction loops — especially important on production-grade projects.

> [!info] Added Context
> Vibe coding and SDD represent opposite ends of a control spectrum. Vibe coding trades control for speed. SDD trades speed (at planning time) for control and consistency. Neither is universally right — vibe coding suits prototypes; SDD suits anything you'll maintain.

---

## How to Use It

### The full SDD workflow

```
Spec Document → Review → Technical Design Plan → Review → Tasks → Code → Validate
```

Each stage feeds the next. Skipping stages is possible on small features; never skip on anything that touches core architecture.

### Stage 1 — Spec Document

A non-technical document answering what and why. It should contain:

- **Problem statement** — why this feature is needed.
- **Functional requirements** — the exact behaviours the system must have.
- **Input/output behaviour** — what triggers the feature and what it returns.
- **Constraints** — performance, compatibility, size, or rule-based limits.
- **Edge cases** — what can go wrong and how each case should be handled.
- **Acceptance criteria** — the checklist that defines "done." Used for validation later.

### Stage 2 — Technical Design Plan

A technical document answering how. Written after the spec, it adds:

- Tech stack selection with rationale.
- High-level architecture diagram (even just described in text).
- Data models and schemas.
- API endpoints or function signatures.
- Core design decisions.
- Functional flows (e.g. "on load: call `/api/chats`, render sidebar, on click: call `/api/chats/{id}`").

> [!info] Added Context
> Keeping spec and tech plan as separate documents is intentional. If you later migrate to a different tech stack, your spec stays valid and reusable. Only the tech plan needs rewriting.

### Stage 3 — Tasks

Extract a concrete task list from the tech plan. Typically ordered: data layer → backend → frontend → integration. These are the units Claude Code will execute, one at a time or in parallel via subagents.

### Stage 4 — Code

Claude Code implements each task. In plan mode (see [[08 - Plan Mode & Ultraplan]]), it reads the spec and tech plan, then produces its own implementation plan before writing any code.

### Stage 5 — Validate

Check the output against your spec's acceptance criteria. If criteria are not met, iterate with targeted corrections — not new open-ended prompts.

### Where to store spec documents

Keep specs inside `.claude/specs/` in your project. One file per feature, named clearly (`database-setup.md`, `auth-login.md`). This keeps specs version-controlled alongside code and accessible to Claude when you reference them.

### Constraint patterns

> [!tip] Best Practice
> The "do not touch X" constraint pattern belongs in your spec, not just in your session prompt. Constraints stated only in the prompt disappear after a `/clear`. Constraints in the spec survive every session. See also [[06 - CLAUDE.md - Instructing the Agent]] for project-wide constraints.

---

## Best Practices

- Write the spec before opening Claude Code. The planning phase is human work — Claude executes it, not designs it.
- Use Claude to generate a first-draft spec from a brief description, then review and correct it. This is faster than writing from scratch, but the review step is non-negotiable.
- Acceptance criteria should be testable statements, not vague goals. "Sidebar loads within one second" is testable. "Sidebar feels fast" is not.
- After validation, if Claude missed any criteria, add a constraint to `CLAUDE.md` so the same miss doesn't recur in future features.
- For small, isolated features you understand completely, the spec can be brief. For anything touching auth, data models, or shared infrastructure — be thorough.

---

## Common Mistakes

> [!warning] Common Mistake
> Treating the spec as optional for "simple" features. Small features grow. A spec written in five minutes now prevents a debugging session later.

> [!warning] Common Mistake
> Writing functional requirements that are ambiguous or incomplete, then being surprised when Claude interprets them differently. Every unresolved question in the spec is a decision Claude will make for you.

> [!warning] Common Mistake
> Skipping the acceptance criteria section. Without it, you have no principled way to validate whether Claude's output is correct. You end up eyeballing it, which misses edge cases.

---

## To Explore Later

- Automating spec creation via a custom slash command — the video mentions building a `/spec` command that generates a spec document from a brief feature description. Covered in [[09 - Custom Slash Commands]].
- Using subagents to execute tasks from the tech plan in parallel — covered in [[11 - Subagents (Built-in)]].

---

*Related: [[06 - CLAUDE.md - Instructing the Agent]] · [[08 - Plan Mode & Ultraplan]]*
