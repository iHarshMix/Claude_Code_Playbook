# 08 - Plan Mode & Ultraplan

> Plan Mode forces Claude Code to think before it codes — generating a detailed implementation plan that you review and approve before any files are changed.

---

## What It Is

Plan Mode is a ==read-only operating== mode in Claude Code. When active, Claude Code spins up ***internal agents to read and explore your codebase***, then produces a detailed implementation plan for a given task. It makes zero file changes during this phase. You review the plan, then explicitly approve execution.

> [!note] From the Video
> "During Plan Mode, you cannot perform any write operations. Claude will only and only read. And the main goal of reading is that it is creating a very elaborate plan for your given task."

Ultraplan is a cloud-based variant of Plan Mode. The planning runs remotely on an Opus instance inside an Anthropic container, with a web editing interface for the plan. The resulting plan can then be sent back to your local session for implementation.

---

## Why It Matters

Without a planning step, Claude Code jumps from prompt to code immediately. On simple tasks this is fine. On anything touching multiple files, shared modules, or architectural decisions, the result is often off-target — either structurally wrong or over-engineered.

Plan Mode inserts a deliberate review checkpoint between intent and execution. You see the full plan before a single file is touched. This catches structural misunderstandings early, when they cost only a revised prompt — not a debugging session after the code is written.

> [!info] Added Context
> Plan Mode fits directly into the Spec-Driven Development workflow. The spec document is the input; the implementation plan is the output. Plan Mode is how you go from "what and why" (spec) to "how exactly" (plan) without writing the technical design plan yourself.

---

## How to Use It

### Activating Plan Mode

Two ways:
- Press `Shift + Tab` twice in the Claude Code terminal.
- Type `/plan` and hit Enter.

The interface will confirm: `Plan Mode ON`.

### Running a planning session

Give Claude Code a ***prompt referencing*** your ==[1]spec document== and ==[2]relevant files==:

```
Read the spec at .claude/specs/feature-name.md and the existing codebase, 
then generate an implementation plan. Save the plan to .claude/plans/feature-name.md.
```

Claude Code will read all referenced files and produce a step-by-step plan. It will not write any code.

### Reviewing and approving

Read the plan carefully before approving. Look for:
- Steps that touch files you didn't expect.
- Missing steps (e.g. no migration, no tests).
- Wrong assumptions about your data model or API structure.

Once satisfied, approve execution. Claude Code switches to write mode and implements the plan.

### Activating Ultraplan

Type `/ultraplan` followed by your planning prompt. Claude Code will ask for confirmation, then open a web-based planning session at a provided URL. Review and edit the plan in the browser, then choose to teleport it back to your terminal for local implementation.

---

## Configuration Options

### Model selection

For complex planning tasks (large refactors, architectural decisions, many interdependent files), switch to Opus before entering Plan Mode:

```
/model
```

Select Opus for planning, then switch back to Sonnet for implementation. Opus produces higher-quality plans but consumes significantly more tokens.

### Extended Thinking

Extended Thinking gives Claude a reasoning phase before it writes its response — a scratchpad where it works through the problem before committing to a plan.

```
/config → Thinking Mode → true
```

> [!tip] Best Practice
> Always enable Extended Thinking when using Plan Mode. Plans produced with it are observably more thorough, especially when multiple files interact.

> [!info] Added Context
> Extended Thinking is analogous to writing on a whiteboard before speaking. Without it, Claude starts generating the plan token-by-token as soon as it sees the prompt — which works for simple tasks but can go wrong on complex ones because early tokens constrain later ones.

### Effort Level

Effort Level controls how many tokens Claude may use during its Extended Thinking scratchpad — i.e., how long it can reason before answering.

```
/effort [low | medium | high | max | auto]
```

| Level | When to use |
|---|---|
| `low` | Simple, isolated features |
| `medium` | Standard features, recommended default |
| `high` | Complex multi-file features |
| `max` | Major architectural work (Opus only) |
| `auto` | Let Claude infer — good general default |

Higher effort = better plan quality, more tokens consumed. Don't use `max` routinely.

---

## Best Practices

- Always read the plan before approving. The checkpoint is only useful if you actually use it.
- Save plans to `.claude/plans/` alongside specs. They serve as documentation of why the code was structured the way it was.
- For complex features, pair Opus model + Extended Thinking + high effort. For routine features, Sonnet + auto effort is sufficient.
- Use Ultraplan when your regular Plan Mode output is unsatisfactory — not as the default. It costs more and takes longer, but produces better plans for genuinely hard planning problems.
- If Claude's plan includes a step you disagree with, correct it before approving. Changing your mind mid-implementation is much more disruptive.

---

## Common Mistakes

> [!warning] Common Mistake
> Approving the plan without reading it. The entire value of Plan Mode is the review step. Rubber-stamping it turns Plan Mode into a slower version of just running Claude directly.

> [!warning] Common Mistake
> Using Opus and `max` effort for every planning task. Reserve heavy settings for genuinely complex work. Routine features don't need this level of compute — and the token cost adds up quickly.

> [!warning] Common Mistake
> Not saving the plan. Plans are useful references when validating output against your spec. A plan you can't review is a missed debugging tool.

---

## To Explore Later

- Ultraplan's web editing interface allows collaborative review of plans — potentially useful for team workflows.
- Using `/ultraplan` as part of a custom slash command that chains: spec generation → planning → task creation automatically. Connects to [[09 - Custom Slash Commands]].

---

*Related: [[07 - Spec-Driven Development]] · [[09 - Custom Slash Commands]]*
