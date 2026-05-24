# SESSION CONTEXT — Claude Code Playbook

> One entry per session. Most recent session at the top.
> Upload to Claude Project source files at the start of every new session.
> Tells Claude what was covered, what was decided, and where to pick up.

---

## How to Use This File

**End of every session:** fill in the session summary block, push to GitHub, re-upload to Claude Project.
**Start of every new session:** Claude reads this + PLAYBOOK_CONTEXT + NOTE_STYLE_GUIDE before anything else.
**Rule:** most recent session always at the top. Older sessions stay for reference — never delete them.

---

## Batch Plan (permanent reference)

| Batch | Videos | Theme | Total Duration | Status |
|-------|--------|-------|----------------|--------|
| 1 | 1 + 2 | Foundations | ~44 min | ✅ |
| 2 | 3 + 4 + 5 | Core Interaction | ~89 min | ✅ |
| 3 | 6 + 7 + 8 | Project Structure | ~111 min | ✅ |
| 4 | 9 + 10 | Reusability | ~96 min | ✅ |
| 5 | 11 + 12 | Agents | ~96 min | ✅ |
| 6 | 13 + 14 + 15 | Integrations & Automation | ~156 min | ✅ |

**Playlist complete. All 15 notes written.**

---

## Session Log

---

### Session 6 — 2026-05-24
**Batch covered:** Batch 5 + Batch 6 (combined session)
**Videos covered:** Video 11 + Video 12 + Video 13 + Video 14 + Video 15
**Notes written/updated:** 11 - Subagents (Built-in), 12 - Custom Subagents, 13 - MCP (Model Context Protocol), 14 - Hooks in Claude Code, 15 - Plugins & Extensions

**What was done:**
- Read transcripts for Videos 11, 12, 13, 14, and 15
- Wrote note `11 - Subagents (Built-in)` — covers the context explosion problem (stateless LLMs + full history re-sent each turn), the "lost-in-the-middle" effect, how subagents solve it (isolated context, compact result returned), the three built-in types (Explore, Plan, General Purpose), implicit vs explicit triggering, parallel subagents pattern and the same-file conflict warning, and the function analogy as a `[!note]`
- Wrote note `12 - Custom Subagents` — covers why built-ins are insufficient for specialized tasks, the Markdown + YAML file structure, two creation methods (UI via `/agents` and manual), tool and model assignment strategy, sequential pipeline (test-writer → test-runner) and parallel review (security + quality) as documented workflow patterns, the "don't trust generated files blindly" tip, and wiring subagents to slash commands
- Wrote note `13 - MCP (Model Context Protocol)` — covers what MCP is and the pre-MCP integration problem, how it extends Claude Code's default toolset, add/remove/inspect workflow, a reference table of 9 key servers with their practical use cases, the GitHub token permissions gotcha, and the "too many servers degrades context" warning as the video's most counterintuitive lesson
- Wrote note `14 - Hooks in Claude Code` — covers the coding harness concept (required foundation for hooks), agent loop and session lifecycle as compressed scaffolding, the probabilistic LLM + deterministic harness tension that hooks resolve, the three-field hook structure (event, matcher, action), exit code table (0 = proceed, 2 = block), stdin JSON payload pattern, auto-formatting and file-protection hook examples, and the CLAUDE.md vs hooks distinction
- Wrote note `15 - Plugins & Extensions` — covers the sharing/distribution problem plugins solve, the plugin folder structure and mandatory `plugin.json` manifest, the app store analogy for marketplaces, official vs third-party marketplace distinction with marketplace.json format, install workflow, scope selection (user vs project), and the "plugins include agents too" correction from the video

**Decisions made:**
- Note 14 required the most structural work: the video's 20-minute conceptual setup (coding harness → agent loop → session lifecycle → hooks) was compressed into three short paragraphs as required scaffolding — without it, the hook definition and exit code system have no foundation
- The session-start summary hook pattern (from the video's personal anecdote) became a `[!tip]` in Note 14 — the most generalizable creative use case mentioned
- The "plugins include agents too" point was flagged as a correction the video itself made mid-stream; it's documented in Note 15's What It Is section rather than buried
- All three meta files (PLAYBOOK_CONTEXT, MOC, SESSION_CONTEXT) updated to reflect 15/15 completion
- MOC Key Concepts Quick Reference expanded significantly for Notes 11–15, going from 2 placeholder entries to 20+ specific concepts
- PLAYBOOK_CONTEXT Structural Decisions updated with decisions from Sessions 5 and 6
- To Explore Later in MOC updated with two new items from Notes 13 and 15

**Style guide updated:** No

**Open threads (carry to next session):**
- Playlist is complete. No open threads.
- Future work: assess whether any cross-cutting concepts warrant a `_concepts/` note (skill evaluation, harness engineering, MCP server building).

**Next session:** Playlist complete. No scheduled next session.

---

### Session 5 — 2026-05-24
**Batch covered:** Batch 5 — Agents
**Videos covered:** Video 11 + Video 12
**Notes written/updated:** 11 - Subagents (Built-in), 12 - Custom Subagents

*(Absorbed into Session 6 above — both batches were completed in the same conversation.)*

---

### Session 4 — 2026-05-23
**Batch covered:** Batch 4 — Reusability
**Videos covered:** Video 9 + Video 10
**Notes written/updated:** 09 - Custom Slash Commands, 10 - Claude Code Skills

**What was done:**
- Read transcripts for Videos 9 and 10
- Wrote note `09 - Custom Slash Commands` — covers the definition (saved prompts as Markdown files), project vs user scope as a table, three-part file structure (description, allowed-tools, body), `$ARGUMENTS` for parameterized commands with format-hint best practice, the `/create-spec` command as a high-value pattern, branch creation chained into spec command, and the Commands → Skills merge documented as a `[!note]`
- Wrote note `10 - Claude Code Skills` — covers the core problem (general LLMs vs specialized tasks), why prompts fail for repeated workflows (5 limitations as a table), skill folder structure with code block, `skill.md` anatomy (YAML front matter + Markdown body), Progressive Disclosure as the 3-level loading mechanism, personal vs project skills scope table, skill creation via Skill Creator (recommended path), skill composability, and `disable_model_invocation: true` for command-style skills

**Decisions made:**
- Commands → Skills merge documented in both notes. Note 09 carries the `[!note]` as the primary flag; Note 10 documents the going-forward structure and the `disable_model_invocation` flag
- Progressive Disclosure named and explained as the core loading mechanism
- Personal vs project skills table mirrors the same pattern used in Note 06 for CLAUDE.md locations
- Skill evaluation and benchmarking parked in Note 10's To Explore Later and added to MOC's To Explore Later

**Style guide updated:** No

**Open threads:** None

**Next session:** Batch 5 — Agents (Videos 11 + 12)

---

### Session 3 — 2026-05-23
**Batch covered:** Batch 3 — Project Structure
**Videos covered:** Video 6 + Video 7 + Video 8
**Notes written/updated:** 06 - CLAUDE.md - Instructing the Agent, 07 - Spec-Driven Development, 08 - Plan Mode & Ultraplan

**What was done:**
- Read transcripts for Videos 6, 7, and 8
- Wrote note `06 - CLAUDE.md - Instructing the Agent` — covers the no-memory problem, what CLAUDE.md is, both creation methods (`/init` vs manual), structured breakdown of what to include (6 content sections), full location taxonomy as a table (5 possible locations), the `.claude/` folder concept (project-level vs global), the `rules/` subfolder for splitting large files, and Auto Memory (`memory.md`) in To Explore Later
- Wrote note `07 - Spec-Driven Development` — covers vibe coding vs SDD as the conceptual framing, the full 5-stage workflow (Spec → Review → Tech Design Plan → Tasks → Code → Validate), spec document anatomy with all 6 required sections, tech design plan anatomy, why the two documents are kept separate (tech-stack independence), where to store spec files, and the constraint pattern connection to Note 06
- Wrote note `08 - Plan Mode & Ultraplan` — covers Plan Mode activation, the planning prompt pattern, review/approve loop, Ultraplan as cloud-based escalation option, and three configuration levers (model selection, Extended Thinking, Effort Level) each as their own sub-section with a table for Effort Level

**Decisions made:**
- Auto Memory (`memory.md`) placed in Note 06's To Explore Later
- Spec and Technical Design Plan kept as clearly separate sub-sections in Note 07
- Open thread from Session 2 resolved: the "do not touch X" constraint pattern is addressed in Note 07's Best Practices

**Style guide updated:** No

**Open threads:** None

**Next session:** Batch 4 — Reusability (Videos 9 + 10)

---

### Session 2 — 2026-05-23
**Batch covered:** Batch 2 — Core Interaction
**Videos covered:** Video 3 + Video 4 + Video 5
**Notes written/updated:** 03 - Slash Commands, 04 - Making Code Changes & Adding Context, 05 - Context Window Management

**What was done:**
- Read transcripts for Videos 3, 4, and 5
- Wrote note `03 - Slash Commands` — covers built-in command reference table, sessions concept, /btw for side questions, /permissions scopes, model switching pattern (Opus for planning, Sonnet for implementation)
- Wrote note `04 - Making Code Changes & Adding Context` — covers pre-writing prompts, @ file mentions, image paste as design reference, the change-approve-verify loop, commit discipline
- Wrote note `05 - Context Window Management` — covers context window concept, ~150K usable token reality, pre-loaded components table, quadratic history growth, /context and /compact usage, auto-compaction vs manual compaction, /clear vs new session

**Decisions made:**
- Constraint pattern in prompts ("do not touch X") captured in Note 04 as [!tip] — worth revisiting in Note 07
- Sub-agents forward-linked from Note 05 to Notes 11/12

**Style guide updated:** No

**Open threads:**
- The "do not touch X" constraint pattern connects to spec writing — mention the link when writing Note 07

**Next session:** Batch 3 — Project Structure (Videos 6 + 7 + 8)

---

### Session 1 — 2026-05-22
**Batch covered:** Batch 1 — Foundations
**Videos covered:** Video 1 + Video 2
**Notes written/updated:** 01 - Agentic Coding Mindset, 02 - Setup & Configuration

**What was done:**
- Read transcripts for Video 1 (Agentic Coding Mindset) and Video 2 (Setup & Configuration)
- Wrote note `01 - Agentic Coding Mindset` — covers vibe coding vs. agentic coding, the developer-to-director shift, why vibe coding fails at scale, and what structured AI collaboration looks like in practice
- Wrote note `02 - Setup & Configuration` — covers three setup paths (paid, Ollama cloud, Ollama local), bash mode and why to use it inside Claude sessions, Git/project setup workflow, and the three orientation questions for onboarding to any codebase

**Decisions made:**
- Notes generalize fully — no CampusX project references, no expense tracker mentions
- The three orientation questions from Video 2 preserved verbatim as they are genuinely reusable for any project
- `[!info]` callout used for analogies and added context (beyond video content), distinct from `[!tip]` which is for actionable best practices

**Style guide updated:** No

**Open threads:** None

**Next session:** Batch 2 — Core Interaction (Videos 3 + 4 + 5)

---

## Session Template (copy this for each new session)

```
### Session [N] — [Date]
**Batch covered:** Batch [N] — [Batch Name]
**Videos covered:** Video [X] + Video [Y]
**Notes written/updated:** [note names]

**What was done:**
- 

**Decisions made:**
- 

**Style guide updated:** Yes / No
> If yes — what changed:

**Open threads (carry to next session):**
- 

**Next session:** Batch [N+1] — [Batch Name] (Videos [X + Y])
```

---

*Upload to Claude Project source files at the start of every session.*
