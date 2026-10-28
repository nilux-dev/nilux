# Nilux AI

An AI engineer that lives in your terminal. Nilux reads, writes, runs, and remembers — across
sessions — so you can stay on the command line and let it do the work.

```bash
npm install -g @nilux-ai/code
nilux
```

Requires Node.js 20 or newer. Works on macOS, Linux, and Windows.

**[Docs](https://nilux.dev/docs)** · **[Quickstart](https://nilux.dev/docs/quickstart)** ·
**[Pricing](https://nilux.dev/pricing)** · **[Changelog](https://nilux.dev/changelog)**

## About this repository

The source is not published here. This repository is where the project is tracked publicly:
releases, documentation links, and **[issues](../../issues)** — the place to report a bug or ask
for something. The agent itself runs on our servers; the CLI you install is the client.

## What it does

Describe a task in plain language. Nilux finds the relevant files itself, proposes a change, shows
you the diff, and applies it once you approve. It runs commands, reads their output, and keeps
going — the same loop you would run by hand, without the typing.

- **Works across the whole project.** It searches and reads before it edits, so a rename reaches
  every call site rather than the one file you had open.
- **Asks before it acts.** Every file edit and every command is shown first. Four approval modes,
  from confirm-everything to hands-free — `Shift+Tab` cycles between them mid-session.
- **Remembers your project.** Conventions, decisions and the shape of the codebase survive between
  sessions, so you stop re-explaining the same context every morning.
- **Delegates.** For wide work it spawns subagents that explore in their own context and report
  back, instead of filling yours with search results.
- **Connects to your tools.** Any Model Context Protocol server — databases, APIs, cloud consoles —
  becomes available inside the session from one config entry.

## What it costs

Pay only for the tokens you use. No seat, no subscription, no minimum.

| Model | Input | Output | Context |
|-------|-------|--------|---------|
| Nilux Standard | $0.28 / 1M tokens | $0.56 / 1M tokens | 1M |
| Nilux Pro | $0.87 / 1M tokens | $1.74 / 1M tokens | 1M |

Repeated context is billed at a small fraction of the input rate, which is most of a long coding
session. Check your balance any time with `/balance`, or see live rates and a cost calculator at
[nilux.dev/pricing](https://nilux.dev/pricing).

## Handy commands

| Command | What it does |
|---------|--------------|
| `/resume` | Continue an earlier conversation |
| `/rewind` | Roll back to an earlier point in the session |
| `/compact` | Summarise a long conversation to keep it fast and cheap |
| `/model` | Switch between Standard and Pro mid-session |
| `/mcp` | Manage Model Context Protocol servers |
| `/skills` | List reusable prompts available as slash commands |
| `/init` | Generate a `nilux.md` with project context for the team |
| `/balance` | Show your remaining balance |
| `/help` | List everything |

## Reporting something

- **A bug or a feature request** — [open an issue](../../issues/new/choose).
- **A security vulnerability** — please do not open an issue. See [SECURITY.md](SECURITY.md).

## License

The `@nilux-ai/code` package is distributed under [Apache-2.0](LICENSE). Its source is not
published, and the server that runs the agent is proprietary.
