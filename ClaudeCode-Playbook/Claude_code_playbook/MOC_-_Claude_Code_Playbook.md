# 🗺️ MOC — Claude Code Playbook

> A generalized, project-agnostic playbook for using Claude Code effectively.
> Built from CampusX's *Agentic Coding using Claude Code* playlist.
> **Last updated:** 2026-05-24
> **Videos covered:** 15 / 15 ✅ Complete

---

## What This Playbook Is

This is not a tutorial on how to build a specific project.
It is a **system of best practices** for using Claude Code on *any* real project — with structure, control, and production-level intent.

---

## 🗂️ Theme Notes Index

### 🟢 Foundations
- [x] [[01 - Agentic Coding Mindset]]
- [x] [[02 - Setup & Configuration]]

### 🔵 Core Workflow
- [x] [[03 - Slash Commands]]
- [x] [[04 - Making Code Changes & Adding Context]]
- [x] [[05 - Context Window Management]]

### 🟠 Project Structure & Planning
- [x] [[06 - CLAUDE.md - Instructing the Agent]]
- [x] [[07 - Spec-Driven Development]]
- [x] [[08 - Plan Mode & Ultraplan]]

### 🟣 Reusability & Automation
- [x] [[09 - Custom Slash Commands]]
- [x] [[10 - Claude Code Skills]]

### 🔴 Advanced — Agents & Integrations
- [x] [[11 - Subagents (Built-in)]]
- [x] [[12 - Custom Subagents]]
- [x] [[13 - MCP (Model Context Protocol)]]
- [x] [[14 - Hooks in Claude Code]]
- [x] [[15 - Plugins & Extensions]]

---

## 📺 Source Videos → Theme Map

| # | Video Title | Theme Note | Status |
|---|-------------|------------|--------|
| 1 | Learn AI Coding the Right Way | [[01 - Agentic Coding Mindset]] | ✅ |
| 2 | How to Setup Claude Code | [[02 - Setup & Configuration]] | ✅ |
| 3 | Slash Commands | [[03 - Slash Commands]] | ✅ |
| 4 | Making Code Changes + Image as Context | [[04 - Making Code Changes & Adding Context]] | ✅ |
| 5 | Context Window Management | [[05 - Context Window Management]] | ✅ |
| 6 | Claude.md — The Most Important File | [[06 - CLAUDE.md - Instructing the Agent]] | ✅ |
| 7 | Spec-Driven Development | [[07 - Spec-Driven Development]] | ✅ |
| 8 | Plan Mode + Ultraplan Mode | [[08 - Plan Mode & Ultraplan]] | ✅ |
| 9 | Custom Slash Commands | [[09 - Custom Slash Commands]] | ✅ |
| 10 | Claude Code Skills: Full Guide | [[10 - Claude Code Skills]] | ✅ |
| 11 | SubAgents — Context & Token Problems | [[11 - Subagents (Built-in)]] | ✅ |
| 12 | Claude Custom Subagents | [[12 - Custom Subagents]] | ✅ |
| 13 | Claude + MCP Explained | [[13 - MCP (Model Context Protocol)]] | ✅ |
| 14 | Hooks — Full Theory + Practical | [[14 - Hooks in Claude Code]] | ✅ |
| 15 | Plugins + Claude Code Notes | [[15 - Plugins & Extensions]] | ✅ |

---

## 🔑 Key Concepts Quick Reference

| Concept | Lives In |
|---------|----------|
| What is agentic coding | [[01 - Agentic Coding Mindset]] |
| Vibe coding vs. agentic coding | [[01 - Agentic Coding Mindset]] |
| Developer-to-director mindset shift | [[01 - Agentic Coding Mindset]] |
| Free / API setup | [[02 - Setup & Configuration]] |
| Bash mode inside Claude sessions | [[02 - Setup & Configuration]] |
| Orienting Claude to a new codebase | [[02 - Setup & Configuration]] |
| `/clear`, `/compact`, `/memory` | [[03 - Slash Commands]] |
| Feeding images as context | [[04 - Making Code Changes & Adding Context]] |
| When to `/compact` vs `/clear` | [[05 - Context Window Management]] |
| CLAUDE.md structure and content | [[06 - CLAUDE.md - Instructing the Agent]] |
| `.claude/` folder — project vs global | [[06 - CLAUDE.md - Instructing the Agent]] |
| Auto Memory (`memory.md`) | [[06 - CLAUDE.md - Instructing the Agent]] |
| Spec document — what and why | [[07 - Spec-Driven Development]] |
| Technical Design Plan — how | [[07 - Spec-Driven Development]] |
| Acceptance criteria and validation | [[07 - Spec-Driven Development]] |
| Vibe coding vs. spec-driven | [[07 - Spec-Driven Development]] |
| Plan Mode — read-only planning | [[08 - Plan Mode & Ultraplan]] |
| Extended Thinking in planning | [[08 - Plan Mode & Ultraplan]] |
| Effort Level for reasoning budget | [[08 - Plan Mode & Ultraplan]] |
| Ultraplan — cloud-based planning | [[08 - Plan Mode & Ultraplan]] |
| Saved prompts as slash commands | [[09 - Custom Slash Commands]] |
| Project vs user scope for commands | [[09 - Custom Slash Commands]] |
| `$ARGUMENTS` for parameterized commands | [[09 - Custom Slash Commands]] |
| Commands → Skills merge | [[09 - Custom Slash Commands]] |
| What a Skill is and how it loads | [[10 - Claude Code Skills]] |
| Progressive Disclosure (on-demand loading) | [[10 - Claude Code Skills]] |
| `skill.md` — YAML front matter + body | [[10 - Claude Code Skills]] |
| Personal vs project skills | [[10 - Claude Code Skills]] |
| `disable_model_invocation: true` | [[10 - Claude Code Skills]] |
| Context explosion + lost-in-the-middle | [[11 - Subagents (Built-in)]] |
| Explore / Plan / General Purpose subagents | [[11 - Subagents (Built-in)]] |
| Implicit vs explicit subagent triggering | [[11 - Subagents (Built-in)]] |
| Parallel subagents — when and how | [[11 - Subagents (Built-in)]] |
| Custom subagent file structure | [[12 - Custom Subagents]] |
| Tool and model assignment per agent | [[12 - Custom Subagents]] |
| Sequential multi-agent pipeline | [[12 - Custom Subagents]] |
| Parallel code review (security + quality) | [[12 - Custom Subagents]] |
| What MCP is and why it exists | [[13 - MCP (Model Context Protocol)]] |
| Adding / removing MCP servers | [[13 - MCP (Model Context Protocol)]] |
| Database MCP — natural language queries | [[13 - MCP (Model Context Protocol)]] |
| Figma MCP — design to code | [[13 - MCP (Model Context Protocol)]] |
| GitHub MCP — full PR workflow automation | [[13 - MCP (Model Context Protocol)]] |
| Too many MCP servers degrades context | [[13 - MCP (Model Context Protocol)]] |
| Coding harness concept | [[14 - Hooks in Claude Code]] |
| Agent loop and session lifecycle | [[14 - Hooks in Claude Code]] |
| Hook structure (event, matcher, action) | [[14 - Hooks in Claude Code]] |
| Exit codes — 0 proceed, 2 block | [[14 - Hooks in Claude Code]] |
| Auto-formatting hook (post_tool_use) | [[14 - Hooks in Claude Code]] |
| File protection hook (pre_tool_use) | [[14 - Hooks in Claude Code]] |
| Hooks vs CLAUDE.md instructions | [[14 - Hooks in Claude Code]] |
| What a plugin is and why it exists | [[15 - Plugins & Extensions]] |
| Plugin folder structure + plugin.json | [[15 - Plugins & Extensions]] |
| Official vs third-party marketplaces | [[15 - Plugins & Extensions]] |
| Installing plugins and marketplaces | [[15 - Plugins & Extensions]] |
| Plugins include agents too | [[15 - Plugins & Extensions]] |

---

## 🔮 To Explore Later

- [ ] Claude Code in CI/CD pipelines
- [ ] Multi-repo agentic workflows
- [ ] Cost optimization at scale
- [ ] Skill evaluation and benchmarking
- [ ] Building custom MCP servers for internal tools
- [ ] Private team marketplaces and plugin composition

---

## 📌 Notes on This MOC

- Theme notes are organized by **concept**, not by video number.
- Each note is self-contained and readable independently.
- When new videos are added, check if they extend an existing note or need a new one. Update the table above.
- Checkboxes track which notes have been written.
