# 13 - MCP (Model Context Protocol)

> MCP is the standard that lets Claude Code talk to external tools and services — turning a capable coding agent into one that can also query your database, read your Figma designs, or manage your GitHub repos directly from the terminal.

---

## What It Is

MCP (Model Context Protocol) is an open standard created by Anthropic for connecting LLMs to external tools, services, and data sources. Before MCP, each integration required custom code that broke whenever the service's API changed. MCP standardizes that connection layer so any tool with an MCP server can plug into any MCP-compatible agent.

In Claude Code's context, adding an MCP server extends the tools Claude can use beyond its defaults (Read, Write, Bash). Each server you add gives Claude new abilities — querying a database in plain English, pulling a Figma design by URL, interrogating your GitHub repos without leaving the terminal.

> [!info] Added Context
> Think of MCP servers as power adapters. Claude Code is the device; MCP is the universal socket standard. Without it, every integration needs a custom cable. With it, you just plug in.

---

## Why It Matters

Claude Code's default toolset covers your local filesystem and shell. That's enough for isolated coding tasks, but real development workflows touch many systems — databases, design tools, project trackers, CI/CD platforms, communication channels. MCP closes that gap.

The practical benefit is reduced context-switching. Instead of opening a database client, a GitHub tab, a Jira board, and a Slack window alongside your terminal, you pull that context directly into Claude Code. Claude can then act on it — not just read it.

> [!note] From the Video
> "With MCP, you can tell Claude: read this Jira ticket and implement the feature. All the details from the ticket are automatically pulled into context and coding starts."

---

## How to Use It

### Adding an MCP server

```bash
# Add a local (stdio) server — for local databases, files
claude mcp add <server-name> -- <command> <args>

# Add a remote (HTTP/SSE) server — for cloud services like GitHub
claude mcp add --transport http <server-name> <url>
```

After adding, restart Claude Code and run `/mcp` to verify the server shows as connected.

### Checking available servers and their tools

```
/mcp
```

Selecting a server in the `/mcp` menu lets you view its tools and their descriptions — useful for understanding what each server can do before using it.

### Removing a server

```bash
claude mcp remove <server-name>
```

### Key MCP servers worth knowing

| Server | What it adds |
|--------|-------------|
| Database (SQLite / PostgreSQL / MySQL) | Query any table in plain English — schema, relationships, aggregations |
| Figma | Read a design by URL and convert it directly to HTML/CSS/component code |
| GitHub | Query repos, issues, PRs; create and merge PRs; delete branches — all from Claude |
| Context7 | Pulls live, up-to-date docs for any library or framework into Claude's context |
| Jira | Read tickets assigned to you; implement features directly from ticket specs |
| Notion | Read requirement docs, API design specs, and team knowledge bases |
| Slack | Post PR links to review channels; check incident channels for production errors |
| AWS | Deploy to EC2, check CloudWatch logs, optimize infrastructure |
| Docker | Generate and optimize Dockerfiles; manage container images |

### Authenticating GitHub (example setup)

1. Go to GitHub → Settings → Developer Settings → Personal Access Tokens → Fine-grained tokens
2. Generate a token with permissions for: Contents (read/write), Pull requests (read/write), Issues (read/write)
3. Pass the token when adding the MCP server

> [!warning] Common Mistake
> Not granting enough permissions when generating the GitHub token. If Claude can push but can't create pull requests, check that the PR permission is set to Read and Write — not just Read.

---

## Best Practices

- Keep your active MCP servers minimal. Every connected server loads its tool descriptions into your context window at session start. Too many servers means unnecessary token overhead before you've typed a single prompt.
- Add servers that match your current project's needs. Use `/mcp remove` to clean up servers from projects you've wrapped up.
- Treat the GitHub MCP server as a replacement for the manual git push → PR → merge → cleanup workflow. Pair it with a custom slash command (see [[09 - Custom Slash Commands]]) that commits, pushes, creates a PR, merges, and deletes the branch in one step.
- Use the database MCP server whenever you need to understand schema relationships in a new codebase. It removes the need to open a separate SQL client.

> [!tip] Best Practice
> For the Figma integration: always right-click the design frame in Figma and copy the direct link to that specific frame — not the file URL. Claude needs the frame-level URL to accurately read component details.

---

## Common Mistakes

> [!warning] Common Mistake
> Connecting every available MCP server "just in case." Each server's tool descriptions consume tokens on every session start. Five unnecessary servers can silently degrade response quality by filling early context with irrelevant tool metadata.

> [!warning] Common Mistake
> Using a local-path database server (like db-hub) with a local SQLite file. Many database MCP servers require a remotely accessible database. For SQLite files sitting on your local machine, use the `mcp-database-server` package which explicitly supports local SQLite paths.

---

## To Explore Later

- Transport mechanisms: `stdio` (local process communication) vs `SSE/HTTP` (remote server communication) — relevant if you build your own MCP server.
- Building a custom MCP server for internal tools (company-specific APIs, internal databases, custom data sources).
- Combining GitHub MCP with Slack MCP to post deployment summaries automatically after a PR is merged.

---

*Related: [[15 - Plugins & Extensions]]*
