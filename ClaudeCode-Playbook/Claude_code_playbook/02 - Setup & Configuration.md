# 02 - Setup & Configuration

> Getting Claude Code running on your machine — paid, free via cloud models, or fully local — and wiring it to a real project from day one.

---

## What It Is

Claude Code is a terminal-based AI coding tool from Anthropic. Setup involves three things: installing the CLI, connecting it to a model (paid or free), and opening it from inside your project folder. Once running, you interact with it through a conversational interface in the terminal.

---

## Why It Matters

Where you launch Claude Code determines what it can see. Running it from your project root gives it access to your entire codebase as context — which is the foundation for everything else in the workflow. Setup done right means every session starts with Claude already oriented to your project.

---

## How to Use It

### Installing Claude Code

```bash
# Install via npm (from Claude Code homepage)
npm install -g @anthropic-ai/claude-code

# Launch from your project root
cd your-project/
claude
```

On first run, Claude Code will ask you to trust the folder and authorize your Anthropic account via browser. This is a one-time step.

### Paid setup (recommended)

- Create an account at `claude.ai`
- Upgrade to a paid plan (~$20/month)
- Run `claude` in your terminal — it uses Anthropic's models directly (Opus, Sonnet, Haiku)

### Free setup via Ollama (cloud models)

Ollama lets you run Claude Code backed by open-source or cloud models at no cost, with limitations.

```bash
# Install Ollama from ollama.com, then:
ollama launch claude
# Select a cloud model (e.g. Qwen 3.5) when prompted
```

Weekly usage limits apply. Good for exploration, not sustained work.

### Free setup via Ollama (local models — fully offline)

```bash
# Pull a local model first
ollama pull qwen2.5-coder:7b

# Then launch
ollama launch claude
# Select the local model from the "More" section
```

Response speed depends on your machine. 16GB RAM can run ~14B parameter models comfortably. Lower RAM → use smaller models.

> [!info] Added Context
> Local models are free with no usage limits, but coding quality drops noticeably compared to Claude's proprietary models. Use them to learn the workflow; switch to paid for real projects.

### Bash mode inside Claude Code

Inside a Claude session, press `Shift + 1` (`!`) to enter bash mode. Run shell commands directly — they become part of the conversation history.

```
> !
$ python3 -m venv venv
$ source venv/bin/activate
$ pip install -r requirements.txt
$ python3 app.py
```

This matters because Claude can then answer questions about commands it watched you run — error messages, installed packages, running processes all become context.

### Orienting Claude to a new project

When you first open Claude Code in a project, ask these three questions before doing anything else:

```
What does this project do?
What tech stack does this project use?
Explain the project structure to me.
```

Claude reads your files and builds its understanding from them. This onboarding step is what makes all subsequent work coherent.

> [!tip] Best Practice
> Always launch Claude Code from your project root directory, not from your home folder or some other location. Claude's awareness of your codebase is scoped to where you launch it.

---

## Best Practices

- Run bash commands inside the Claude session (bash mode), not in a separate terminal — this keeps them in Claude's context
- Set up version control (`git init`, push to GitHub) before starting work — not after
- Use a virtual environment for Python projects; activate it inside Claude's bash mode so Claude sees the same environment you do
- Treat the three orientation questions as a standard checklist every time you onboard to a new codebase

> [!tip] Best Practice
> Starting a project mid-state (with some existing code already in place) is normal and closer to real-world conditions than starting from scratch. Claude Code handles this well — just orient it first.

---

## Common Mistakes

> [!warning] Common Mistake
> Running bash commands in a separate terminal window. Claude has no visibility into those commands or their output, so you lose all the context-building benefit of bash mode.

> [!warning] Common Mistake
> Launching `claude` from the wrong directory. If you're not in your project root, Claude Code won't see your files and will operate essentially blind.

- Skipping the orientation questions and jumping straight into asking Claude to write code
- Not setting up Git before starting — makes it harder to track what Claude changed and roll back if needed
- Choosing a local model for serious work — quality difference is significant

---

## To Explore Later

- OpenRouter as an alternative to Ollama for free/cheap model access
- Open Code (open-source Claude Code alternative) for fully free setups
- API key configuration for direct Anthropic API access without a subscription

---

*Related: [[01 - Agentic Coding Mindset]] | [[03 - Slash Commands]] | [[05 - Context Window Management]]*
