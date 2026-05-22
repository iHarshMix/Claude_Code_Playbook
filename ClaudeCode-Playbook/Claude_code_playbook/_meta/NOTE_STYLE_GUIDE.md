# NOTE STYLE GUIDE — Claude Code Playbook

> Formatting contract for all theme notes.
> Claude reads this every session before creating or editing any note.

---

## Note Skeleton (fixed — every note follows this exactly)

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
| `##` H2 | The 6 fixed sections |
| `###` H3 | Sub-sections within a section only |
| `####` H4 | Never. Rethink structure instead. |

---

## Callout Types (three only)

```markdown
> [!tip] Best Practice
> Claude-added insight. Not from the video.

> [!warning] Common Mistake
> What typically goes wrong.

> [!note] From the Video
> Use sparingly — only when exact source framing matters.
```

`[!tip]` always = Claude addition. Clear separation of source vs added knowledge.

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

*Upload to Claude Project source files each session.*
