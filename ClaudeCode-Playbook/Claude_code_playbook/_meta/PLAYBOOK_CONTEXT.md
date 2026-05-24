# PLAYBOOK_CONTEXT

## Goal
Build a generalized, project-agnostic playbook of best practices for using Claude Code on any real project.
Source: CampusX — *Agentic Coding using Claude Code* (15 videos, ongoing playlist).

---

## Ground Rules (read before every session)

- Notes are **thematic**, not per-video. One note per concept cluster.
- Content from videos is **generalized** — no CampusX-specific project references.
- Claude adds best practices beyond the video where useful, marked as `[!tip]` or `[!info]` callouts.
- Advanced/optional topics go in `## To Explore Later` — never in the main body.
- Essentials first. Don't overcrowd notes.

---

## Playlist Progress

| # | Video Title | Duration | Theme Note | Status |
|---|-------------|----------|------------|--------|
| 1 | Learn AI Coding the Right Way | 16:54 | [[01 - Agentic Coding Mindset]] | ✅ |
| 2 | How to Setup Claude Code | 26:36 | [[02 - Setup & Configuration]] | ✅ |
| 3 | Slash Commands | 31:28 | [[03 - Slash Commands]] | ✅ |
| 4 | Making Code Changes + Image as Context | 22:02 | [[04 - Making Code Changes & Adding Context]] | ✅ |
| 5 | Context Window Management | 35:07 | [[05 - Context Window Management]] | ✅ |
| 6 | Claude.md — The Most Important File | 46:28 | [[06 - CLAUDE.md - Instructing the Agent]] | ✅ |
| 7 | Spec-Driven Development | 28:07 | [[07 - Spec-Driven Development]] | ✅ |
| 8 | Plan Mode + Ultraplan Mode | 37:36 | [[08 - Plan Mode & Ultraplan]] | ✅ |
| 9 | Custom Slash Commands | 46:27 | [[09 - Custom Slash Commands]] | ✅ |
| 10 | Claude Code Skills: Full Guide | 49:46 | [[10 - Claude Code Skills]] | ✅ |
| 11 | SubAgents — Built-in | 48:24 | [[11 - Subagents (Built-in)]] | ✅ |
| 12 | Claude Custom Subagents | 47:23 | [[12 - Custom Subagents]] | ✅ |
| 13 | Claude + MCP Explained | 54:33 | [[13 - MCP (Model Context Protocol)]] | ✅ |
| 14 | Hooks — Full Theory + Practical | 1:04:58 | [[14 - Hooks in Claude Code]] | ✅ |
| 15 | Plugins + Claude Code Notes | 35:08 | [[15 - Plugins & Extensions]] | ✅ |

**Videos covered so far:** 15 / 15
**Theme notes created so far:** 15 / 15

---

## Theme Notes Status

| Note | Created | Last Updated |
|------|---------|--------------|
| 01 - Agentic Coding Mindset | ✅ | 2026-05-22 |
| 02 - Setup & Configuration | ✅ | 2026-05-22 |
| 03 - Slash Commands | ✅ | 2026-05-23 |
| 04 - Making Code Changes & Adding Context | ✅ | 2026-05-23 |
| 05 - Context Window Management | ✅ | 2026-05-23 |
| 06 - CLAUDE.md - Instructing the Agent | ✅ | 2026-05-23 |
| 07 - Spec-Driven Development | ✅ | 2026-05-23 |
| 08 - Plan Mode & Ultraplan | ✅ | 2026-05-23 |
| 09 - Custom Slash Commands | ✅ | 2026-05-23 |
| 10 - Claude Code Skills | ✅ | 2026-05-23 |
| 11 - Subagents (Built-in) | ✅ | 2026-05-24 |
| 12 - Custom Subagents | ✅ | 2026-05-24 |
| 13 - MCP (Model Context Protocol) | ✅ | 2026-05-24 |
| 14 - Hooks in Claude Code | ✅ | 2026-05-24 |
| 15 - Plugins & Extensions | ✅ | 2026-05-24 |

---

## Structural Decisions Made

- Flat folder — one folder, no subfolders for notes.
- `_meta/` holds PLAYBOOK_CONTEXT and NOTE_STYLE_GUIDE (not Obsidian notes).
- `_templates/` holds the note skeleton.
- `_concepts/` subfolder only if 3+ notes share a concept worth isolating — not created yet.
- Internal links use `[[note name]]` Obsidian format.
- `[!tip]` callouts = actionable best practices (Claude additions, always distinct from video content).
- `[!info]` callouts = added context, analogies, background (Claude additions).
- Note title uses em dash (—) except CLAUDE.md note which uses hyphen to avoid filename issues.
- Notes generalize fully — no project-specific references from the source videos.
- Three orientation questions from Video 2 preserved verbatim as reusable for any project.
- Spec and Technical Design Plan kept as separate concepts in Note 07 — the separation rationale (tech-stack independence) is documented there.
- Auto Memory (`memory.md`) parked in Note 06's To Explore Later — closely related to CLAUDE.md but distinct enough to not crowd the note.
- Plan Mode configuration options (model, Extended Thinking, Effort Level) each have their own sub-section in Note 08 — they are independent levers.
- Commands → Skills merge documented in both Notes 09 and 10. Note 09 carries the `[!note]` explaining the product change; Note 10 documents `disable_model_invocation: true` as the going-forward pattern for command-style behaviour.
- `$ARGUMENTS` variable for parameterized commands documented in Note 09.
- Progressive Disclosure (3-level on-demand loading) documented as the core mechanism in Note 10.
- Personal vs project skill scope table included in Note 10, mirroring the same pattern from Note 06 (CLAUDE.md locations).
- Context explosion problem and "lost-in-the-middle" effect documented as the two core problems subagents solve in Note 11.
- Implicit vs explicit subagent triggering documented in Note 11; parallel subagents' same-file conflict warning added as `[!warning]`.
- Custom subagent file structure (YAML front matter + body) and the two creation methods (UI vs manual) documented in Note 12.
- Sequential (test-writer → test-runner) and parallel (security + quality review) multi-subagent workflow patterns documented in Note 12 with example slash command wiring.
- MCP "too many servers degrades context" warning documented in Note 13 — the video's most counterintuitive practical lesson.
- Coding harness concept introduced in Note 14 as the foundation for understanding hooks — deterministic harness + probabilistic LLM = the problem hooks solve.
- Agent loop and session lifecycle documented in Note 14 as required conceptual scaffolding; exit code table (0 = proceed, 2 = block) included as the operational core.
- Plugin folder structure and mandatory `plugin.json` manifest documented in Note 15.
- Official vs third-party marketplace distinction documented in Note 15 with marketplace.json format.

---

## Open Questions / Parked Ideas

- `_concepts/` folder: revisit — playlist is now complete, assess whether any cross-cutting concepts warrant isolation.
- Skill evaluation and benchmarking: parked in Note 10's To Explore Later — may warrant its own note.
- Building custom MCP servers for internal tools: parked in Note 13's To Explore Later.
- Private team marketplaces and plugin composition conflicts: parked in Note 15's To Explore Later.
- CI/CD pipeline integration and multi-repo agentic workflows: remain open for future exploration.

---

## How to Update This File

**New note created:** mark ✅ in Theme Notes Status, add date, update count.
**Video covered:** mark ✅ in Playlist Progress, update count.
**New video added to playlist:** add row to Playlist Progress, decide if new theme note needed, update MOC.

---

*Upload this to Claude Project source files at the start of every session.*
