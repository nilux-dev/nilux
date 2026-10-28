# Nilux AI

An AI engineer for your terminal, and a desktop app for Mac. Nilux reads, writes, runs, and
remembers — across sessions — so you can hand it the work and stay in control.

```bash
npm install -g @nilux-ai/code
nilux
```

Requires Node.js 20 or newer. Works on macOS, Linux, and Windows; on Windows it also needs
[Git for Windows](https://git-scm.com/downloads/win), because it runs commands in the Git Bash that
comes with it.

Prefer an app? **[Download Nilux for Mac](https://nilux.dev/download)**.

**[Docs](https://nilux.dev/docs)** · **[Quickstart](https://nilux.dev/docs/quickstart)** ·
**[Pricing](https://nilux.dev/pricing)** · **[Changelog](https://nilux.dev/changelog)** ·
**[Download](https://nilux.dev/download)**

## About this repository

The source is not published here. This repository is where the project is tracked publicly:
documentation links and **[issues](../../issues)** — the place to report a bug or ask for
something. Release notes are on the site: [CLI](https://nilux.dev/changelog/terminal) and
[desktop app](https://nilux.dev/changelog/desktop). The agent itself runs on our servers; the CLI and the desktop app you install are
the clients.

## What it does

Describe a task in plain language. Nilux finds the relevant files itself, proposes a change, shows
you the diff, and in the default mode applies it once you approve. It runs commands, reads their output, and keeps
going — the same loop you would run by hand, without the typing.

- **Works across the whole project.** It searches and reads before it edits, so a rename reaches
  every call site rather than the one file you had open.
- **You decide what needs approval.** In the default mode every file edit and every command is
  shown first. Four approval modes, from confirm-everything to hands-free — `Shift+Tab` cycles
  between them mid-session.
- **Remembers your project.** Decisions, the corrections you give it and the context behind the
  work are kept as plain notes on your machine, per project, so you stop re-explaining the same
  context every morning.
- **Delegates.** For wide work it spawns subagents that explore in their own context and report
  back, instead of filling yours with search results.
- **Connects to your tools.** Any Model Context Protocol server — databases, APIs, cloud consoles —
  becomes available inside the session from one config entry.

## What it costs

Pay only for the tokens you use. No seat, no subscription, no monthly minimum, and new accounts
start with free credit.

Repeated context is billed at a small fraction of the input rate, which is most of a long coding
session. The current rates for both models, the peak hours and a cost calculator are at
[nilux.dev/pricing](https://nilux.dev/pricing). Check your balance any time with `/balance`.

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
