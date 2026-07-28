# Changelog

Every release of the Nilux AI CLI. The same list, formatted for reading, lives at
https://nilux.dev/changelog

Releases before 1.0.10 went straight to testers rather than to a registry, which is why they are
dated here but not on npm. `@nilux-ai/code` starts at 1.0.10.

## Changelog 25.07.2026 (v1.0.10)

**Long sessions keep their context — and their price**
- A dropped connection, a sleeping laptop or a server update no longer costs you your context: the session comes back with everything it had, and the model keeps working from the same understanding instead of quietly losing part of it.
- Reconnecting is now near-free. Where a rejoin used to make the provider re-read the whole conversation at full price, it now reuses the cached context almost entirely — the difference on a long session is cents per message versus fractions of a cent.
- `/compact` got the same treatment: summarising a long conversation no longer re-processes it from scratch, so compacting is both faster and dramatically cheaper.
- Resuming a session (`/resume`) and rewinding to an earlier point keep the same benefit — the conversation is restored exactly as it was, not rebuilt approximately.

**Faster web lookups**
- When the assistant looks several things up at once, the requests now go out together instead of one after another — a batch of lookups takes about as long as the slowest one, not the sum of all of them.
- Web lookups no longer hold up the rest of the turn either: files it reads in the same step appear straight away instead of waiting behind the network. Anything you still have to approve is untouched — it runs in order, exactly as before.

**Cleaner terminal**
- `/rewind` now lists only your own messages. Internal bookkeeping entries no longer appear as things you can roll back to, and the "restore code" marker now lands on the right message.
- Fetching a page shows the address instead of the long instruction that goes with it, and reports how much was actually downloaded and how the site answered, instead of a bare "done".

**Picking up where you left off**
- Fixed: resuming a session immediately after launching the CLI could leave the assistant with none of your history — the terminal showed the conversation while the assistant had nothing, which was worst right after a `/compact`, where the summary is the entire conversation. The history is now held and delivered as soon as the connection is up.
- `/resume` no longer offers conversations whose transcript is gone — those opened as a blank session with no explanation. The list now shows only what can actually be restored, and cleans itself up.
- A session appears in the list from its very first message. Previously, starting a conversation and closing the terminal within a few seconds could leave it off the list entirely, even though it was saved.
- Resuming a conversation no longer shrinks it in the list: it keeps its real message count and its original first line instead of being relabelled after your next message.

**Dashboard**
- Cached usage is now shown as a percentage, and the usage chart's tooltip includes what you spent that day.

## Changelog 20.07.2026 (v1.0.9)

**Memory lifecycle now works end-to-end**
- Fixed: closing or replacing a memory (marking work `resolved`/`superseded` via `memory_update_status`) could hang for two minutes and fail — it now completes instantly. Recalling and saving were never affected.

**No more long hangs on unsupported actions**
- Fixed: if the assistant attempted an action this version couldn't handle, it used to sit on "Running…" for ~2 minutes before timing out — now it fails fast with a clear result, so the model adapts immediately instead of retrying blindly.

**Sharper external (MCP) tool details**
- External tools whose parameters reused a shared shape sometimes showed up as untyped ("any"), making the model guess arguments — parameter types are now always resolved and shown correctly, so third-party MCP tools are more reliable.

## Changelog 18.07.2026

**Recall your past sessions**
- The assistant can now search and read its OWN past chat sessions for the current project — ask "what did I do last session", "where did I leave off", or "find where we discussed X", and it answers straight from your real conversation history.
- Four ways to look back: read a previous session, search across all your sessions, list recent sessions, or pull the compact summaries of what was decided.
- It shows when and who (timestamps + whether it was you or the assistant), reports how far back your history goes, and pages through results — so recall is precise, not a wall of noise.
- Different from project memory: memory is your curated notes and decisions; this searches the actual verbatim chat history for when memory doesn't have the answer.
- Stays in the current project and reads only your own sessions.

**Leaner external (MCP) tools**
- Connecting lots of MCP servers no longer floods the model's context: it now sees a compact menu of every connected tool (name + what it does) and loads a tool's full details only when it actually needs one.
- Faster and cheaper sessions when you have many external tools connected — and the model picks the right tool by name instead of guessing, so external integrations are more reliable.

## Changelog 13.07.2026

**Auto-Context — your project memory loads itself**
- New sessions now start primed: the model automatically receives your project's memory (key decisions, conventions, hard-won lessons and the latest session summary) with your first message — no more re-explaining the project every morning.
- Foundational records first: tag a memory with `core` and it is always included ahead of everything else and never cleaned up.
- Injected once per session and refreshed after `/compact` or `/clear`, so the model always works from the current state — never duplicated on `/resume` or reconnect.
- Invisible in the terminal: your chat shows only your own messages.
- On by default; toggle it anytime in `/config` → Auto-Context (uses up to ~4k input tokens per session, cache-priced after the first turn).

**Memory that stays clean**
- New `memory_update_status` tool — the model can now close finished work: a fixed bug becomes `resolved`, a replaced decision becomes `superseded`, instead of everything piling up forever.
- Replacing a memory is now one step: saving with `supersedes` automatically retires the old record — and the old one stays readable on demand, nothing is ever lost.
- Saving a near-duplicate now returns a hint pointing at the existing record and how to update it, instead of silently doing nothing.
- The model keeps exactly one rolling session summary per project instead of accumulating dated copies.

**Smarter recall**
- Replaced (superseded) records no longer clutter search results — ask for them explicitly when you need history.
- Live knowledge ranks first: open records now appear above resolved history regardless of match score.
- Following memory links still reveals a replaced predecessor — chains stay explorable.

**Sync & reliability**
- Fixed: syncing a large batch of memory changes could crash the memory engine (out of memory) — bulk sync is now applied atomically and is dramatically faster.
- Fixed: after `/clear`, resuming that conversation could replay the pre-clear history — a cleared session now starts a genuinely fresh conversation file.

## Changelog 03.07.2026

**Permission modes**
- Four approval modes — default, accept edits, plan and auto. Cycle them instantly with Shift+Tab, or via `/mode` (`/mode auto` jumps straight to one).
- Choose how much Nilux confirms with you — review every action, wave routine edits through, or run hands-free.
- Even on full-auto, genuinely dangerous commands like `rm -rf` always stop for your confirmation.

**Plan mode**
- Ask for a plan first — Nilux researches read-only and proposes a step-by-step plan before changing anything.
- Approve the plan to start work, or send notes to revise it.
- Your approved plan is saved and survives `/clear`, so a long task keeps its thread.

**Plan model**
- Optionally run planning on a stronger reasoning model while your everyday work stays on your usual one — set once in `/config`.

**In-app notifications**
- A notification bell in your dashboard with an unread badge and history — top-ups, low balance, referrals, refunds and more.

**Referral program**
- Invite friends; when they top up, you both earn a discount on your usage.
- New accounts also get a starter promo.

**Email verification & password reset**
- Confirm your email at sign-up, reset a forgotten password from the login page, and set or change your password in settings.

**Connected accounts**
- Link your Google and GitHub accounts from settings.

**Usage insights**
- The dashboard usage chart now shows your actual spend over time, with calendar-scoped stats.

**Interface & reliability**
- Inline command hints — typing a command like `/mode ` shows the available options; a partially typed command highlights the best match.
- More reliable mode switching with Shift+Tab in Windows terminals.
- Resource-heavy MCP tools now get more time before timing out.
- Steadier terminal output — removed a periodic idle flicker and corrected the approval-dialog timer.

## Changelog 07.06.2026

**Low balance heads-up**
- If your balance drops below $2, the CLI now shows a low-balance notice in the welcome banner when you start a session — so you can top up before a task gets interrupted mid-way.

## Changelog 01.06.2026

**Sign in with GitHub & Google**
- New "Continue with GitHub" and "Continue with Google" buttons on the login and register pages — one-click sign-up and sign-in, no password to create
- Your session lives in a secure HttpOnly cookie (same as email login); the social provider's token never touches the browser
- If an account with the same verified email already exists, signing in with GitHub/Google links to it instead of creating a duplicate

**Sign in to the CLI from your browser**
- Running `nilux` now opens your browser to sign in — the same login as the website, including Continue with Google and GitHub. No password is typed into the terminal.
- If you're already signed in on nilux.dev, pairing the CLI is a single click.
- If you created your account with Google or GitHub, you can now sign in to the CLI too — previously only email-and-password accounts could.

**Usage cost display**
- Small per-request and per-model costs are no longer rounded down to $0.00 on the Usage page — they now show enough precision to be readable (e.g. $0.0001)

**Interface polish**
- Smoother CLI rendering — no more flickering or screen jumps on long output and approval dialogs
- Refreshed loading spinner
- Clearer file diffs — line numbers are now colored by change (added / removed)

## Changelog 31.05.2026

**Faster & Cheaper Long Sessions**
- Session environment (project file tree, git state, project notes, date) is now captured once when you start nilux and reused for the whole session — the model's cached context stays valid far longer
- Reconnecting no longer rebuilds the model's context from scratch — near-instant resume with ~99% cached-context reuse
- Lower cost on long sessions — a stable cache means the provider bills the cheap cache-hit rate instead of reprocessing the entire conversation
- Connected skills and MCP tools are now listed in a consistent order, so enabling or disabling one mid-session no longer silently breaks cached-context reuse

**Awareness of Mid-Session Changes**
- When the date rolls over during a long session, the model now knows the current date without you having to mention it
- When you make a new git commit while chatting, the model becomes aware the repository changed and reflects the live HEAD — useful if you ask what changed — while never acting on it on its own
- Live repository state now supersedes the snapshot taken at the start of the session

**Editing & File Safety**
- Fixed: the Edit tool corrupted any text containing `$` sequences (shell scripts, regex, environment variables like `$1`/`$$`, template strings) — the replacement is now inserted exactly as written
- Edit now requires the target text to be unique, or an explicit "replace all" — so an edit can no longer silently land on the wrong occurrence
- "Replace all" now actually works (it was previously ignored and replaced only the first match)
- Writing or creating a file no longer silently produces an empty file when content is missing — it reports an error instead
- Fixed: rewind / checkpoint restore could lose your changes on case-sensitive filesystems (Linux) — now uses the real file path

**Reliability**
- Long, tool-heavy turns now compact automatically mid-turn instead of failing when the context fills up
- Sending a new message while a response is still streaming now queues it, instead of running two responses at once (which could scramble the conversation and double-count usage)
- After a reconnect, if any output produced while you were offline couldn't be fully recovered, you're now told — instead of a silent gap
- Fixed occasional duplicate-key glitches in the message list during fast streaming

**Account Security**
- Session tokens are no longer kept in browser localStorage — they now live in HttpOnly cookies (web dashboard and admin), so a script injected into a page can't read your session
- Changing your password now revokes your existing sessions and API keys everywhere, including the live chat connection
- A deactivated account is now disconnected immediately, mid-session, rather than only on next connect
- Registration now requires an 8-character minimum password (was 6)
- Hardened server-side URL fetching (web-page reader, image URLs) to block internal/private addresses

**Billing Accuracy**
- The per-turn cost shown after each response is now correct (it previously displayed $0.00 while your balance still decreased); image/vision cost is now priced correctly
- Top-up payments hardened: protection against double-crediting on payment-provider retries, correct USD handling, and a $5–$500 range
- The dashboard no longer shows placeholder/sample trend numbers as if they were real metrics

## Changelog 30.05.2026

**Connection Resilience — New Reconnect System**
- Transparent auto-reconnect — if your connection drops mid-task (Wi-Fi, router reboot, laptop sleep), the session reconnects on its own and the running task continues from where it stopped — no need to resend
- Live task resume — the in-progress request keeps executing on the server during the outage; you rejoin it seamlessly
- 10-minute reconnect window with smart backoff, replacing fixed retry attempts — survives sleep and long network drops
- No lost output — tokens, tool calls and results produced during the outage are replayed in order, exactly once
- Approvals survive disconnects — confirming an action while offline is preserved and applied on reconnect
- Parallel/batch tool calls no longer hang after a drop
- Duplicate-action protection — a tool never runs twice after reconnect
- Model context (KV cache) preserved across reconnects — no slow context rebuild

## Changelog 21.05.2026

**Built-in Memory**
- Model remembers decisions, bugs, patterns, conventions and context across sessions
- 11 tools: remember, recall, forget, project_status, link_memories, goal_progress, compliance_trend, pattern_store, pattern_search, pattern_mature, pattern_mark_as_skill
- Memory search
- Data stored locally on user's machine
- Works on any Node.js version with no additional dependencies
- Enabled by default, toggle in /config

**Cloud Sync**
- Two-way memory synchronization between devices
- Automatic download on startup, upload after each write
- Conflicts resolved automatically
- Deleted records sync correctly between devices
- Configuration in `~/.nilux/config.json`

**MCP Fixes**
- Disable now persists to config file (not reset after restart)
- Disconnect no longer auto-reconnects

**Bug Fixes**
- Improved sync stability

## Changelog 18.05.2026

**Background Workflow (Ctrl+B)**
- Workflow can now be sent to background by pressing Ctrl+B during execution
- User continues working — workflow runs autonomously
- BottomBar shows live status: role · tool count · tokens · time
- `↓ to view` → Enter opens detailed overlay with each role's progress
- `x` in overlay stops the workflow
- Approval dialogs from background workflow arrive correctly, don't block input
- "Running in the background (↓ to manage)" — status like SubAgent

**Live Progress**
- File `~/.nilux/bg-tasks/<id>.output` updates in real time
- You can ask the agent to check workflow status at any time
- Shows current role, executed tools, handoffs between roles
- Shows when workflow is waiting for user confirmation

**Session Recovery**
- Each workflow step is saved in conversation history
- On terminal crash — `/resume` restores full workflow state
- Unfinished workflows are automatically marked as interrupted on recovery

**Smart Waiting**
- Agent no longer takes over while workflow is running
- Agent waits for notification instead of constantly polling status
- On stop shows what was done, what was interrupted, what wasn't started

**ESC after Background Workflow**
- ESC correctly stops the main agent after workflow completes/stops
- Approval from background workflow no longer shows "Generating..." for main agent

**Other Improvements**
- Navigation ↓: chat history first, then BottomBar
- All workflow data stored locally on user's machine
- Long tool arguments trimmed in WorkflowDisplay (Puppeteer scripts don't flood the terminal)
- Status color in BottomBar matches active role (planner/coder/reviewer)

## Changelog 17.05.2026

**Workflow System — Full Refactor**
- 3 roles instead of 4: Planner → Coder → Reviewer (Tester merged with Reviewer)
- Planner saves plan to `~/.nilux/plans/workflow-*.md`
- UI shows plan before execution — Approve or Reject
- After completion agent receives full info: file list, reviewer findings, plan path
- Generation progress: `↓ 1.2k tokens` instead of "Initializing..." while model thinks

**ESC in Workflow**
- ESC correctly stops workflow and returns control to main agent
- Fixed hang after ESC
- Fixed approval dialog hang after ESC

**Workflow Launch**
- Fixed 120-second delay on start
- Per-role model selection now works (planner=Pro, coder=Standard, etc.)

**Kill Protection**
- AI can no longer kill CLI via `taskkill`, `pkill`, `killall` and other variants
- TaskStop is used to stop background tasks

**WebSocket Stability**
- Deploy no longer drops active connections
- Workflow doesn't hang on connection loss

**Bug Fixes**
- Edit tool: empty `new_string` for text deletion now works
- Role timer doesn't hang on restart (coder↔reviewer cycle)
- Escalation no longer triggers prematurely

**Plan File**
- Saved to `~/.nilux/plans/` regardless of model
- Plan path visible in WorkflowDisplay
