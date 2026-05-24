# 04 - Making Code Changes & Adding Context

> How to give Claude Code precise file targets and use images as design references — the mechanics of actually changing your codebase.

---

## What It Is

Making code changes in Claude Code means directing the agent at specific files, giving it precise instructions, and iterating on the output — all within a session. The two key mechanisms this note covers are:

- **File mentions (`@`)** — telling Claude exactly which file to read or edit
- **Image context** — pasting a design reference image so Claude can generate matching code

---

## Why It Matters

Without these targeting mechanisms, Claude reads your entire project and may edit the wrong file, or produce generic output disconnected from your actual design. Both `@` mentions and images make the instruction deterministic and grounded — the difference between Claude guessing what you want and Claude seeing exactly what you want.

---

## How to Use It

### Prompts as the primary input

Write your prompt outside Claude Code first — in a plain text file or any chat interface — then paste the polished version in. Typing directly in the terminal increases the chance of missing details or making typos that cost you tokens and context.

> [!note] From the Video
> "I always plan what I need to prompt first, refine it in a chat tool, then paste the polished prompt into Claude Code. You're less likely to miss an aspect or make a mistake."

### Targeting a file with @

Use `@` followed by the file path to tell Claude which file to operate on.

```
Add a footer with two links (Terms and Conditions, Privacy Policy) to @templates/base.html
Do not change any other part of the page.
```

Without `@`, Claude has to infer the right file from context. With `@`, it goes directly there. Reduces ambiguity, reduces wasted tokens.

### Adding an image as design reference

Copy an image to your clipboard (from Figma, a screenshot, or any design tool), then paste it directly into the Claude Code input with `Ctrl+V`. The image appears inline as a reference.

Combine it with a targeted prompt:

```
Modify only the hero section in @templates/landing.html and @static/css/landing.css
to match this image exactly. Do not touch any other part of the page.
```

Claude's multimodal capability means it reads the image as visual input and generates code that reproduces the layout, structure, and style it sees.

### The change-approve-verify loop

Claude shows proposed edits as a diff before applying them:
- Green lines = additions
- Red lines = deletions

Review the diff, approve with `y`, then verify in the browser or output. This is the core loop for every code change.

### Committing after each meaningful change

After every distinct, working change — commit. Even small ones.

```bash
git add .
git commit -m "Add footer links to base template"
```

This is not optional. If a later change breaks something, you need a clean rollback point.

---

## Best Practices

- Always scope your prompts: tell Claude what to change AND what not to touch. Unbounded instructions produce unbounded edits.
- Use `@` even on small projects. It costs nothing and prevents wrong-file edits.
- Keep a prompts file alongside your project. One prompt per planned change, written in advance.
- Commit after every meaningful milestone — not just at the end of a session.

> [!tip] Best Practice
> End every prompt with an explicit constraint: "Do not modify any other part of the page." Claude defaults to being helpful — which sometimes means touching things you didn't intend.

> [!tip] Best Practice
> When using image context, paste the image first, then type the prompt below it. This gives Claude the visual before the instruction, which mirrors how you'd hand a design to a developer.

> [!info] Added Context
> The `@` syntax is similar to how IDEs reference symbols. Think of it as a direct pointer — you're saying "operate on this node in the file tree," not "find something relevant." The more precise the pointer, the more deterministic the output.

---

## Common Mistakes

> [!warning] Common Mistake
> Prompting without constraints. "Make the hero section look better" is an invitation for Claude to rewrite the whole page. Always define the boundary of the change explicitly.

> [!warning] Common Mistake
> Skipping commits between changes. If you batch three changes before committing and the third one breaks the UI, you can't isolate what went wrong. Commit often — it's cheap.

> [!warning] Common Mistake
> Typing prompts directly into Claude Code without pre-writing them. Hasty prompts miss details, which means follow-up turns to correct Claude — consuming more context than a clean first prompt would have.

---

## To Explore Later

- Plan Mode and spec-driven development for complex changes — rather than prompting directly, structure the work first: [[07 - Spec-Driven Development]], [[08 - Plan Mode & Ultraplan]]
- Branch-per-feature workflow with PRs — how to structure Git around Claude Code sessions

---

*Related: [[05 - Context Window Management]], [[07 - Spec-Driven Development]]*
