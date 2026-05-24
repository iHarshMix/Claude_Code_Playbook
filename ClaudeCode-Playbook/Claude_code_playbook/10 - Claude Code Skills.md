# 10 - Claude Code Skills

> Reusable, file-based knowledge packages that teach Claude how to do a specialized task — loaded automatically only when needed.

---

## What It Is
![[10- What are Skills.png|479]]
A Skill is a folder inside your project that contains a `skill.md` file and any supporting resources. When Claude detects that a task matches a skill's description, it loads the skill's instructions from disk and uses them — without you having to provide them in the prompt.

> [!info] Added Context
> Think of skills as the difference between telling a contractor "build something" every time vs. handing them a company standards manual they reference whenever the job calls for it. The manual stays on the shelf until needed — it doesn't occupy the room.

### Skill folder structure

```
.claude/
  skills/
    your-skill-name/
      skill.md          ← required: trigger logic + instructions
      scripts/          ← optional: supporting code files
      templates/        ← optional: reference files, design assets
```

### Inside `skill.md`

Every `skill.md` has two parts:

**YAML front matter** (top of file):
```yaml
---
name: frontend-design
description: >
  Load this skill whenever the user asks to build, redesign,
  or improve any UI component or page.
---
```

The description is the trigger. Claude reads all skill descriptions at session start and uses them to decide which skill to load when a relevant task appears.

**Markdown body** (below the front matter): detailed instructions — layout rules, typography choices, code patterns, validation steps, links to supporting files in subfolders.

### Commands are now Skills

> [!note] From the Video
> Anthropic has merged Commands and Skills into one structure. Everything lives in `.claude/skills/`. To create a skill that behaves like a command (user-triggered only, never auto-loaded), add `disable_model_invocation: true` to the YAML front matter.

---

## Why It Matters

![[10 Why Skills.png]]

General-purpose LLMs are good at general tasks. They struggle with specialized, repeatable work that requires your specific standards — your design conventions, your code review criteria, your document format. A system prompt can hold these instructions, but it burns context window even when irrelevant.

Skills solve this with **==progressive disclosure==**: *only load what's needed, only when it's needed.*

### The five prompt limitations that Skills fix

| Problem with prompts | How Skills fix it |
|----------------------|-------------------|
| Must retype every session | Loaded automatically from file |
| Burns context window if always-on | Loaded on demand only |
| Can't bundle reference files | Supporting folders included in skill |
| Can't version, share, or improve | Lives in Git — team can collaborate |
| Can't compose multiple instruction sets | Skills can link to other skills |

---

## How to Use It

### Creating a skill (recommended path)

![[10 Asking Claude to make skills.png]]

Use the **Skill Creator** built into Claude.ai (click the `+` icon → Skills → Skill Creator). It will ask:
1. What does the skill do?
2. When should it trigger?
3. What does success look like?

Answer in detail. It will generate the `skill.md` content. Copy it into your project's `.claude/skills/your-skill-name/skill.md`.

> [!tip] Best Practice
> Let the Skill Creator interview you rather than writing `skill.md` from scratch, especially for your first skill. The generated description and trigger language are usually better calibrated than manual attempts.

### Personal vs project skills

| Type     | Location                       | Scope                                       |
| -------- | ------------------------------ | ------------------------------------------- |
| Personal | `~/.claude/skills/your-skill/` | All projects on your machine                |
| Project  | `.claude/skills/your-skill/`   | Current project only; ==shareable via Git== |

Use personal skills for your coding style, writing voice, or design preferences that apply everywhere. Use project skills for domain-specific knowledge tied to one codebase.

### How loading works (Progressive Disclosure)

![[10 How skills loads.png]]

1. **Session start** — Claude loads all YAML front matter (name + description) for every skill. ==This is tiny and always present.==
2. **Task detected** — Claude matches the user's request against skill descriptions. If a match is found, it loads that skill's full `skill.md` body into context.
3. **Supporting resources** — If the `skill.md` body references files in subfolders (scripts, templates), those are fetched ==on demand as needed.==

Nothing enters context until it's actually relevant.

## ==Composing skills==

A skill's body can reference another skill by path. This allows building a ==multi-step workflow from modular pieces== — e.g. a "generate report" skill that links a "read PDF" skill and a "create PPTX" skill, each loaded in sequence as the workflow progresses.

> [!tip] Best Practice
> Build skills small and focused. One skill = one specialized capability. Compose them for complex workflows rather than writing one giant all-in-one skill. Smaller skills are easier to test, improve, and reuse.

---

## Best Practices

![[10 Skill example.png]]

- Write the `description` field as a trigger condition, not a title: "Load this skill whenever the user asks to create or modify a slide deck" — not "PowerPoint skill."
- Include failure patterns and validation steps in the body, not just the happy path.
- After creating a skill, restart Claude Code — skills only register on startup.
- Commit skills to version control. They are team infrastructure, not personal config.
- Iterate: test the skill on 3–5 real tasks, note where output drifts from expectations, refine the body. Expect 4–5 iterations before a skill is reliable.

> [!tip] Best Practice #note_relative_path
> When a skill references external scripts or templates, use relative paths from within the skill folder. Absolute paths break when the project is cloned to a different machine.

---

## Common Mistakes

> [!warning] Common Mistake
> Writing a skill description that is too broad — "Load this skill for any coding task." Claude will load it constantly, burning context. Make descriptions specific enough that the skill only triggers for the one task type it handles well.

> [!warning] Common Mistake
> Treating community-sourced skills as safe to use without review. Skills execute bash commands and read files. Always read a skill fully before adding it to your project, especially from unknown sources.

> [!warning] Common Mistake
> Building a skill and never iterating on it. First-draft skills almost always have gaps in edge case handling. Testing on real tasks and refining the body is what turns a draft into a reliable tool.

---

## To Explore Later

- Skill evaluation and benchmarking: how to formally measure whether a skill's output meets your quality bar across a test set.
- Anthropic's public skills repository: a safer starting point than community marketplaces for reference implementations.
- Skill composition patterns for multi-step agentic workflows.

---

*Related: [[09 - Custom Slash Commands]], [[11 - Subagents (Built-in)]]*
