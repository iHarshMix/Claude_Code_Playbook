# 09 - Custom Slash Commands

> Saved prompts that trigger as slash commands — the right way to stop repeating yourself across any repeatable workflow.

---

## What It Is

Custom slash commands are user-defined prompts stored as Markdown files inside your project. When you type `/command-name` in Claude Code, it loads and executes that prompt automatically — exactly like built-in slash commands, but built by you.

The file name becomes the command name. The file contents are the instructions.

### Storage location determines scope

| Scope | Location | Available |
|-------|----------|-----------|
| Project | `.claude/commands/your-command.md` | Current project only |
| User (global) | `~/.claude/commands/your-command.md` | All projects |

> [!note] From the Video
> Commands and Skills have since been merged by Anthropic. Going forward, what were called "commands" are now created as Skills (with `disable_model_invocation: true` in the YAML front matter to prevent auto-triggering). The concept and workflow remain identical — only the folder changes from `commands/` to `skills/`.

---

## Why It Matters

Every project has repeatable workflows — things you do after every code change, before every commit, after every feature build. ==Without custom commands, you either retype the same long prompt each time (error-prone) or forget the steps entirely.==

Custom slash commands turn those repeatable workflows into one-keystroke actions that Claude executes consistently every time.

---

## How to Use It

### Creating a command

1. Navigate to `.claude/commands/` inside your project (create the folder if it doesn't exist).
2. Create a Markdown file. The filename = the command name. Example: `review.md` → `/review`.
3. Write the command file with three parts:
   - A `description:` line at the top ==(this shows up in the slash menu autocomplete).==
   - An `allowed-tools:` section listing what tools the command can use (e.g. `Bash(python3*)` to restrict bash to Python only).
   - A detailed [^1]==prose== body explaining exactly what should happen when the command runs.
1. Restart Claude Code — new commands only appear after a restart.
![[09 command description part example.png]]

### Accepting arguments

A command can accept user input at invocation time via the `$ARGUMENTS` variable. ==Whatever the user types after the command name gets captured there.==

```markdown
##discription

discritption: ...
argument-hint: "<used_id> <count> <months>"   <-- format hint

## Arguments
User input: $ARGUMENTS

## Steps
Extract from $ARGUMENTS:
- user_id (integer)
- count (integer)
- months (integer)

If any are missing, tell the user the correct format.
```

Invoking it: `/seed-expenses 2 5 3` — Claude receives `2 5 3` as `$ARGUMENTS` and extracts the three values.

> [!tip] Best Practice
> Always include a format hint in the command body so Claude can prompt the user with the correct syntax if arguments are missing or malformed.

### Automating spec creation

A `/create-spec` command is a high-value pattern: the user passes a ==step number== and ==feature name==, and the command reads the codebase, checks existing specs, creates a new branch, and writes a structured spec document — all in one invocation. See [[07 - Spec-Driven Development]] for the spec format.

> [!tip] Best Practice
> Chain branch creation into your `/create-spec` command. Add steps to check for uncommitted changes, pull latest from main, create a feature branch, and switch to it — before writing the spec. This turns a 4-step manual routine into zero overhead.

---

## Best Practices

- Name commands after the action, not the tool: `/review`, `/commit`, `/test`, `/security-scan` — not `/run-pylint`.
- Be explicit about allowed tools. Restrict bash access to only the commands the workflow actually needs.
- Write the command body as if you were briefing a junior developer: step-by-step, nothing assumed.
- Use `$ARGUMENTS` for anything that changes per invocation (user IDs, feature names, counts). Hard-code what never changes.
- Commit your `.claude/commands/` (or `.claude/skills/`) folder to version control so the whole team benefits.

> [!tip] Best Practice
> After building several commands, audit them for overlap. If two commands share 80% of the same steps, extract the common logic into a shared instruction block that both reference.

---

## Common Mistakes

> [!warning] Common Mistake
> Forgetting to restart Claude Code after creating or editing a command. New commands are only registered on startup — changes mid-session won't show up.

> [!warning] Common Mistake
> Writing vague command bodies like "review the code and give feedback." Claude needs to know: which files, what criteria, what format the output should take, what counts as a pass or fail. The more specific, the more consistent the output.

> [!warning] Common Mistake
> Putting commands that should be project-specific into the global `~/.claude/` folder. A seed-database command only makes sense in one project — keep it project-scoped.

---

## To Explore Later #note_commands_skills_Merge

- Commands vs Skills merge: explore migrating existing `.claude/commands/` files into `.claude/skills/` with  `disable_model_invocation: true` — see [[10 - Claude Code Skills]] for the Skills structure. 
- Multi-step commands that invoke other commands or skills in sequence.

---

*Related: [[07 - Spec-Driven Development]], [[10 - Claude Code Skills]]*

[^1]: **Prose** is ==the ordinary, everyday language people use when speaking or writing==
