# PLAYBOOK_CONTEXT

## Goal
Build a generalized, project-agnostic playbook of best practices for using Claude Code on any real project.
Source: CampusX — *Agentic Coding using Claude Code* (15 videos, ongoing playlist).

---

## Ground Rules (read before every session)

- Notes are **thematic**, not per-video. One note per concept cluster.
- Content from videos is **generalized** — no CampusX-specific project references.
- Claude adds best practices beyond the video where useful, marked as `[!tip]` callouts.
- Advanced/optional topics go in `## To Explore Later` — never in the main body.
- Essentials first. Don't overcrowd notes.

---

## Playlist Progress

| # | Video Title | Duration | Theme Note | Status |
|---|-------------|----------|------------|--------|
| 1 | Learn AI Coding the Right Way | 16:54 | [[01 - Agentic Coding Mindset]] | ⬜ |
| 2 | How to Setup Claude Code | 26:36 | [[02 - Setup & Configuration]] | ⬜ |
| 3 | Slash Commands | 31:28 | [[03 - Slash Commands]] | ⬜ |
| 4 | Making Code Changes + Image as Context | 22:02 | [[04 - Making Code Changes & Adding Context]] | ⬜ |
| 5 | Context Window Management | 35:07 | [[05 - Context Window Management]] | ⬜ |
| 6 | Claude.md — The Most Important File | 46:28 | [[06 - CLAUDE.md - Instructing the Agent]] | ⬜ |
| 7 | Spec-Driven Development | 28:07 | [[07 - Spec-Driven Development]] | ⬜ |
| 8 | Plan Mode + Ultraplan Mode | 37:36 | [[08 - Plan Mode & Ultraplan]] | ⬜ |
| 9 | Custom Slash Commands | 46:27 | [[09 - Custom Slash Commands]] | ⬜ |
| 10 | Claude Code Skills: Full Guide | 49:46 | [[10 - Claude Code Skills]] | ⬜ |
| 11 | SubAgents — Built-in | 48:24 | [[11 - Subagents (Built-in)]] | ⬜ |
| 12 | Claude Custom Subagents | 47:23 | [[12 - Custom Subagents]] | ⬜ |
| 13 | Claude + MCP Explained | 54:33 | [[13 - MCP (Model Context Protocol)]] | ⬜ |
| 14 | Hooks — Full Theory + Practical | 1:04:58 | [[14 - Hooks in Claude Code]] | ⬜ |
| 15 | Plugins + Claude Code Notes | 35:08 | [[15 - Plugins & Extensions]] | ⬜ |

**Videos covered so far:** 0 / 15
**Theme notes created so far:** 0 / 15

---

## Theme Notes Status

| Note | Created | Last Updated |
|------|---------|--------------|
| 01 - Agentic Coding Mindset | ⬜ | — |
| 02 - Setup & Configuration | ⬜ | — |
| 03 - Slash Commands | ⬜ | — |
| 04 - Making Code Changes & Adding Context | ⬜ | — |
| 05 - Context Window Management | ⬜ | — |
| 06 - CLAUDE.md - Instructing the Agent | ⬜ | — |
| 07 - Spec-Driven Development | ⬜ | — |
| 08 - Plan Mode & Ultraplan | ⬜ | — |
| 09 - Custom Slash Commands | ⬜ | — |
| 10 - Claude Code Skills | ⬜ | — |
| 11 - Subagents (Built-in) | ⬜ | — |
| 12 - Custom Subagents | ⬜ | — |
| 13 - MCP (Model Context Protocol) | ⬜ | — |
| 14 - Hooks in Claude Code | ⬜ | — |
| 15 - Plugins & Extensions | ⬜ | — |

---

## Structural Decisions Made

- Flat folder — one folder, no subfolders for notes.
- `_meta/` holds PLAYBOOK_CONTEXT and NOTE_STYLE_GUIDE (not Obsidian notes).
- `_templates/` holds the note skeleton.
- `_concepts/` subfolder only if 3+ notes share a concept worth isolating — not created yet.
- Internal links use `[[note name]]` Obsidian format.
- `[!tip]` callouts = Claude additions, always distinct from video content.
- Note title uses em dash (—) except CLAUDE.md note which uses hyphen to avoid filename issues.

---

## Open Questions / Parked Ideas

- If a future video spans two theme notes, decide at that point: split or extend.
- `_concepts/` folder: revisit when playlist is complete.
- To Explore Later: CI/CD pipelines, multi-repo workflows, cost optimization.

---

## How to Update This File

**New note created:** mark ✅ in Theme Notes Status, add date, update count.
**Video covered:** mark ✅ in Playlist Progress, update count.
**New video added to playlist:** add row to Playlist Progress, decide if new theme note needed, update MOC.

---

*Upload this to Claude Project source files at the start of every session.*
