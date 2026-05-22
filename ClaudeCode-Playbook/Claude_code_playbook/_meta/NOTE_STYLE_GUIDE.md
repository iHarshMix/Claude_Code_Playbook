# NOTE STYLE GUIDE — Claude Code Playbook

> Formatting contract for all theme notes.
> Claude reads this every session before creating or editing any note.
> This guide evolves — update it when a better pattern is found, not before.

---

## Note Skeleton (stable — every note follows this structure)

```
# [Note Title]

> [One line — what this note is about and why it matters]

---

## What It Is
## Why It Matters
## How to Use It
## Best Practices
## Common Mistakes
## To Explore Later
```

- All 6 sections present in every note, even if brief.
- `## To Explore Later` uses `*(nothing parked yet)*` when empty — never delete it.
- No section should be a wall of text.

---

## Headings

| Level | Use For |
|-------|---------|
| `#` H1 | Note title only. One per note. |
| `##` H2 | The 6 standard sections |
| `###` H3 | Sub-sections within a section only |
| `####` H4 | Never. Rethink structure instead. |

---

## Callout Types (four — purpose-driven)

Each callout has a distinct job. Don't use one in place of another.

```markdown
> [!note] From the Video
> Exact framing from the source worth preserving as-is.
> Use sparingly — only when the original phrasing genuinely matters.
```

```markdown
> [!tip] Best Practice
> An actionable recommendation — something you should do.
> Always a Claude addition, never from the video.
```

```markdown
> [!info] Added Context
> Background, analogy, or explanation that helps understanding.
> Claude-added — not in the video, but useful to know.
```

```markdown
> [!warning] Common Mistake
> What typically goes wrong and why.
> Claude-added — pattern observed beyond the video.
```

### Source vs Claude — at a glance

| Callout | From Video | From Claude | Type of content |
|---------|-----------|-------------|-----------------|
| `[!note]` | ✅ | — | Exact source framing |
| `[!tip]` | — | ✅ | Actionable best practice |
| `[!info]` | — | ✅ | Context, analogy, background |
| `[!warning]` | — | ✅ | Mistake or failure pattern |

**Rule:** If you're reading a `[!note]`, it came from the video. Everything else came from Claude.

---

## Bullets vs Prose

- **Bullets:** steps, options, best practices, mistakes.
- **Prose:** explanations, definitions, "why it matters."
- Never mix in the same paragraph.
- Bullet max: 1-2 lines. If longer, make it a sub-section.

---

## Code

Always specify language on code blocks.
Use inline code for: command names, filenames, flags — e.g. `/compact`, `CLAUDE.md`.

---

## Internal Links

- Format: `[[note name]]`
- Link only when useful for navigation — not on every mention.
- Never link back to MOC from within a note.

---

## Naming

| Type | Format |
|------|--------|
| Theme notes | `NN - Title.md` |
| MOC | `MOC - Claude Code Playbook.md` |
| Meta files | plain name inside `_meta/` |
| Template | plain name inside `_templates/` |

---

## Avoid

- ❌ Bold for decoration
- ❌ Text walls in any section
- ❌ Same point repeated across sections
- ❌ Vague bullets ("use it wisely")
- ❌ Empty headers
- ❌ Emoji in body text — MOC only

---

## Done When

✅ Readable without the video.
✅ No section longer than ~10 bullets or ~8 lines of prose.
✅ Doesn't try to be a transcript.

---

## Changelog

- 2026-05-18 — Initial version. Skeleton and callout rules established.
- 2026-05-18 — "fixed" replaced with "stable/standard" to reflect that this guide evolves. Changelog added.
- 2026-05-18 — Added `[!info] Added Context` as fourth callout type. Added source vs Claude reference table for callouts.

---

*Upload to Claude Project source files each session.*
