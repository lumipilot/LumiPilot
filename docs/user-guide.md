# LumiPilot User Guide

**English** | [한국어](user-guide.ko.md)

This guide covers LumiPilot 1.0.23 for Windows. It walks through installation, first-time setup, conversations, approvals, settings, and troubleshooting. For an overview and downloads, see the [README](../README.md).

## Contents

1. [Installation and first run](#1-installation-and-first-run)
2. [First-time setup](#2-first-time-setup)
3. [Tour of the screen](#3-tour-of-the-screen)
4. [Having a conversation](#4-having-a-conversation)
5. [Approvals and safety](#5-approvals-and-safety)
6. [Managing conversations](#6-managing-conversations)
7. [What the AI can do](#7-what-the-ai-can-do)
8. [Lumi (the character)](#8-lumi-the-character)
9. [Settings reference](#9-settings-reference)
10. [Notifications and background work](#10-notifications-and-background-work)
11. [Security and privacy](#11-security-and-privacy)
12. [Troubleshooting](#12-troubleshooting)

---

## 1. Installation and first run

Download steps and SHA-256 verification are in the [README](../README.md#download).

- **Installer** — Run `LumiPilot-<version>-build<N>-windows-x64-setup.exe`. It needs no administrator rights and installs for the current user only. Remove it from Windows Settings → Apps.
- **Portable ZIP** — Extract it anywhere and run `LumiPilot.exe`. There is no install step.

On first run, a usage and safety notice appears. Choose your language (Korean or English) and read it. The AI connection setup window opens next (chapter 2).

### Where your data lives

The app creates these folders automatically. Uninstalling does not delete them.

| Item | Location |
|---|---|
| Data folder | `%APPDATA%\LumiPilot\LumiPilot` |
| Settings | `config\settings.ini` |
| Conversations, memories, schedules | `data\` |
| Log | `data\log\app.log` |
| Error records | `data\CrashLogs\` |

---

## 2. First-time setup

### 2-1. Choose a provider and model

On first run, the **AI connection** window opens. Pick the screen to use (coding session or character session), then the service, authentication, and model, and press **Start**. If you closed it with **Later**, reopen it from Settings → API → **AI connection**.

- **Provider** — The AI service to use.
  - With an API key: Anthropic, OpenAI, Google Gemini, xAI, NVIDIA, Z.ai, OpenRouter, OpenCode, Ollama (runs on your computer), and any OpenAI-compatible endpoint you add.
  - With a subscription sign-in: ChatGPT, Grok, GitHub Copilot. Whether this is allowed is governed by each provider's terms.
  - **Claude and Gemini subscription sign-in is disabled in this version.** Both can still be used with an API key.
- **Model** — Pick a model from the chosen provider. If the list is empty, press **↻** to fetch it. If you have not entered an API key yet, a prompt says so.
- **Helper model** (optional) — A cheaper model for light jobs such as titles and memory cleanup. If left empty, the model you chose above is used.

### 2-2. Enter API keys

Use the **Settings → API** tab. Enter only the keys for features you plan to use. Values save as you type; there is no Save button.

| Item | When you need it |
|---|---|
| API-key providers | When you chose an API-key provider |
| Subscription providers | To sign in with a subscription account (a button shows the steps) |
| Custom providers | To add an OpenAI-compatible address such as a company gateway |
| Image generation | To let the AI draw pictures |
| Google Workspace | For Gmail, Calendar, Drive, and Tasks (needs your own Google OAuth client) |
| Mail accounts | For work or internet mail (IMAP/SMTP) |
| Web search (Tavily) | To let the AI search the internet |
| LINE | To let the AI send LINE messages |
| Voice (ElevenLabs) | To speak with a voice model |
| git token | To let the AI clone or push remote repositories (enter it, or sign in with GitHub) |

**Move between devices** at the bottom of the same screen exports your keys to a file for another PC. The exported file is not encrypted, so delete it after you move it. Subscription sign-ins are not included; sign in again on the new PC.

### 2-3. Set a working folder

**Settings → General → Workspace → Working folder → Change.** This is the base folder for reading and editing files and running commands. Think of it as the AI's working area. It is not an isolation boundary, though (chapter 5).

### 2-4. Notifications and voice (optional)

- **Task completion notifications** (Settings → General) — Notifies you of finished background work while you are not looking at the app.
- **Voice output** (Settings → General) — Choose how replies are read aloud. **OS built-in TTS** uses voices installed on your PC with no key. **Voice model** needs a voice key (API tab) and is billed per character. **Read coding session replies** also reads the final answer of the conversation you are viewing. Tool output, reasoning, and code blocks are not read, and at most 4,000 characters per reply are spoken.

---

## 3. Tour of the screen

### Top bar

From the left:

- **☰** — Opens the sidebar.
- **Session name pill** — The name of the conversation you are viewing. **Click it to open the context usage window** (chapter 6). A dot on its left blinks while the AI is answering.
- **Split button** (wide windows) — Opens two or three conversation columns side by side.
- **Session list button** — Opens the conversation list and archive. It shows how many conversations are open, and a dot appears when another one is waiting for a response.
- **Changes badge** — Shows a count when the working folder has uncommitted changes. Click it to open the file manager's Changes tab.
- **Browser button** — Opens the in-app web browser.

On the character screen, a summary of **delegated sessions** takes the middle of the bar.

### Sidebar (☰)

- **Search** — Searches conversations. Results are grouped by conversation; clicking one jumps to that message and highlights it briefly.
- **Provider / Model / ↻** — See chapter 2. On the character screen, character model settings (conversation model, per-tier models, voice) appear here.
- **Helper model** — Sets a lightweight model separately (titles, memory, completion checks). Compaction summaries use the main model.
- **Triggers** — Turns the macro and trigger feature on or off.
- **Icon row at the bottom** — Search · Files · Character · Settings. The Character button switches between the coding screen and the character screen.
- The app version is shown at the very bottom.

### File manager (sidebar → Files)

It has three tabs.

- **Browse** — Browse the working folder. You can filter by name, sort (name, modified time, size), show hidden files, create folders, clone a repository from a remote address (＋Clone), switch drives, and jump back to the working folder. Right-click a file or folder for **Move · Run · Rename · Duplicate · Copy path · Set as working folder (folders) · Delete**. Click a file to open the viewer (word wrap, find in file, Markdown view, text size). Large files are read in parts; images and executables show only their size and type. HTML is first drawn as a static preview with scripts and network access blocked; **View** runs it with scripts in the in-app browser. Preview limits are 32 MiB for images and 8 MiB for HTML.
- **Changes** — See uncommitted changes. Select files to **stage/unstage** or **discard changes**, then write a message and commit. Buttons at the top **fetch, pull, and push**. Remote actions ask for confirmation, and a failure is reported with its reason. Conflicts and in-progress merges also appear here.
- **History** — The commit list. Click a commit to see its changed files and diffs. Commits that exist only on the remote can be fetched with **Get**.

### Browser

You and the AI share **the same tab**. The top has back, forward, reload, stop, new tab, and the address bar; the **More** menu has **Open in external browser** and **Hand this tab to the AI**. **When you hand a tab over, the AI operates the page** (click, type, read).

- At most 3 tabs are open. Beyond that, the least recently used tab is closed.
- Sites you are signed in to are also signed in for the AI. The app does not store site passwords; only the sign-in state (cookies) from your own sign-in is kept in the app's dedicated profile.
- On wide windows the browser opens to the right of the conversation. Drag the divider to resize it, or collapse it.
- Page dialogs, prompts, and notifications are answered inside the app.
- Browser features need the Microsoft Edge WebView2 Runtime.

---

## 4. Having a conversation

Type in the input box at the bottom and press **Send** (the paper plane). **Enter** sends and **Shift+Enter** adds a new line. A new conversation shows a "How can I help?" prompt until you send the first message.

### Input box buttons

- **Mode button (slider icon)** — Changes the permission level and plan mode (see below).
- **Attach (paperclip)** — Attaches an image. It appears only for models that accept images. You can also paste a screenshot.
- **Commands (/)** — Opens the `/` command list.
- **Stop reading** — Appears only while voice output is reading aloud.

### While the AI is answering

- **Stop (square)** — Stops the work.
- **Type and send to steer** — Slips "do it this way" into what the AI is doing right now.
- **Queue** — Messages you send while the AI is answering pile up below and are delivered automatically afterward (up to 5). Drag to reorder or click to edit.

### Mode button

The button's border color shows the current state. Changes here apply **only to this conversation**.

- **Plan mode** — The AI does not edit right away. It first shows a plan and asks for approval. You cannot toggle it while the AI is answering.
- **Permission level** — Three levels. New conversations start at **Ask before edits**.
  - **Ask before edits** (gray) — Edits and commands ask for approval according to rules and risk level.
  - **Auto-edit** (green) — File edits run automatically; other tools follow separate rules.
  - **Full auto** (red) — Runs without asking, except for actions you have explicitly denied.
- **Reasoning effort** — How deeply the AI thinks. Higher is smarter but slower. Only the levels the model supports are shown.
- **Compaction point** — When the conversation passes this ratio, older parts are summarized to free up space.
- **Eager delegation** — When on, the AI splits work across several helpers without being asked.

### Special commands

- `/goal <task>` — Sets a **goal** for the conversation. The AI keeps working on its own until the goal is met and checks that it is done. A goal chip appears above the input box showing status (running, done, paused, blocked, usage limit, budget reached) and tokens and time used. Click it to **view details · edit · pause/resume · clear**. If a goal was left unfinished, you are asked whether to resume when you reopen the app or the conversation.
- `/compact` — Summarizes older conversation now to free up space. Enter it alone, with no other text.

After turning on the goal flag, press **Esc** or the flag's ✕ to go back to normal input.

### Cards in the conversation

Cards appear while the AI works and after. Most expand when clicked, and right-clicking gives menus such as Copy. Long output can be shown in full with **▼ Expand**.

- **Work card** — Groups the tools the AI ran (reading, searching, commands, and so on) and shows how many failed. Shell commands are split into **Command** and **Result**.
- **File edit card** — Shows the change as a diff. Switch between **split** and **inline**.
- **HTML card** — Renders results such as charts and documents. Switch between preview and code, go full screen, save as HTML, or open in the browser.
- **Image card** — A picture the AI made. Click to enlarge; use **Copy path · Open in default app · Annotate region**. To annotate, drag over the part you want changed and add a note; it becomes an edit request.
- **Helper card** — A helper (sub-agent) the AI delegated work to. Expand it to see each step.
- **Task list card** — The AI's task list and progress.
- **Question, memory, and notice cards** — Questions the AI asked and your answers, things it remembered, and notices such as compaction or plan approval.
- **Review card** — Problems the AI found in code. Use **Put in input box** (fills in an edit request) or **Auto-fix**.
- **Error card** — Shows the reason and a **↺ Retry** button.
- **Completion card** — Appears when background work ends (chapter 10).

### When the AI asks you something

When the AI offers choices, a **choice panel** replaces the input box. Pick an item or write your own under **Other**, then **Submit**. **Cancel** skips the question. If several requests are waiting, "n more pending requests" appears above the input; handling the visible one brings up the next.

---

## 5. Approvals and safety

When the AI is about to change something (edit a file, run a command, send a message), an **approval window** appears just before it runs. It states what will happen and the risk, and for commands, **which shell** (PowerShell or bash) will run it.

- **Run** (**Apply** for file edits) — Allow it this once.
- **Deny** — Do not allow it.
- **Stop** — Cancel the whole task.

Remember-rules you can switch on together. Once chosen, the AI no longer asks about it:

- **Always allow this command pattern** — Remembers a frequently used command (manage it in Settings → General → Allowed shell commands).
- **Always allow edits in this folder** — Remembers file edits in that folder.
- **Allow for this session** — For broad actions such as viewing the screen, the browser, or mouse and keyboard control.

When you review a plan in **plan mode**, choose how to continue:

- **Approve · confirm each step** — Follow the plan, but ask again at every step.
- **Approve · auto-edit** — Run edits automatically for this plan.
- When you deny, say what to change and the AI revises the plan.

### Please keep in mind

- **This is not a sandbox.** Commands and tools you approve run with your user account's permissions. Setting a working folder and approval prompts are not OS-level isolation. Do not run the app as administrator, and try risky work on a copy first.
- **"Always allow" is reused.** It differs from approving one call with the same arguments. Check the target, content, and scope in the approval window. Use full auto only in a trusted test environment.
- **Do not trust outside content blindly.** Web pages, mail, repository instructions, and tool results may contain malicious instructions. If something asks to read secrets, widen permissions, or send data out, check the purpose and the target.
- **Denying or stopping does not undo finished work.** Completed file changes, commands, outgoing messages, and costs remain.

---

## 6. Managing conversations

### Conversation list

- **New conversation** — At the top of the list. You can keep up to 30 conversations open at once.
- **Rename** — Click the pencil (✎). With auto titles on, a title is added after the first reply.
- **Open beside (▥)** — Opens that conversation in the next column where splitting is available.
- **Close (✕)** — Choose **Cancel · Archive · Delete permanently**. Archived conversations stay in the archive and can be restored. Permanent deletion cannot be undone.
- **Archive** — Below the list. Click an item to restore it; click the trash can to delete it permanently.

### Split columns (wide windows)

The **split** button in the top bar opens two or three conversation columns side by side. Each has its own conversation and input box. In an empty column, pick a conversation to open or start a **new conversation**.

- When space runs short, the farthest columns fold into vertical rails; click a rail to expand it again.
- The ✕ on a column header **closes only the column** (the conversation stays).
- Drag a divider to resize; double-click to equalize. The layout is restored when you reopen the app.
- Shortcuts: **Ctrl+\\** split · **Ctrl+1/2/3** focus that column · **Ctrl+Shift+W** close the focused column.
- A column header shows its state (awaiting approval, question, failed) when something is waiting.

### Context usage

Click the session name pill to see how much of the AI's context window this conversation uses: usage by messages and tool definitions, the maximum window, when compaction happens, and what prompt reuse saved. With a subscription plan, the plan usage reported by the provider (per-window usage and reset time) is shown too. GitHub Copilot shows its monthly allowance usage. If space runs short, run `/compact` to summarize now.

### Rewinding messages

Right-click a message for a menu.

- **Copy / Copy selection**
- **Edit** — Edit a message you sent and send it again. Everything after it is removed and the conversation continues from there.
- **Expand / Collapse** — Fold or unfold long messages.
- **Restore files** — Restores files the AI changed after that message (checkpoints). A confirmation appears, and the result (restored, deleted, skipped) is reported.

Checkpoint limits:

- Only files changed through the app's supported edit paths are recorded. Changes made by shell commands, outside programs, databases, mail, or remote servers are not recovered.
- Originals larger than 4 MiB per file are not recorded. When a session's records pass 64 MiB, the oldest turns are discarded, and restoring to a discarded turn reports that the file cannot be restored.
- Restoring can overwrite current files or delete newly created ones. Changes made outside the app are not automatically protected, so review before restoring.
- Checkpoints do not replace a separate backup.

---

## 7. What the AI can do

The AI chooses suitable tools by itself; you do not need to memorize or call them. Most tools follow the approval rules in chapter 5.

- **Files and code** — Read, write, and edit files (including `apply_patch`), search by name and content, find code symbols, check errors.
- **Commands and Git** — Run terminal commands, run long jobs in the background, repeat until a condition is met, and use Git status, commit, merge, and push.
- **Planning and helpers** — Task lists, splitting long jobs across helpers (sub-agents), and asking you questions.
- **Memory and schedules** — Remember important facts, reminders, recurring schedules, and wake-ups for later.
- **Screen and web** — Screen capture, mouse and keyboard control, app window control (Windows), web search, reading web pages, driving the in-app browser, and opening the external browser. **Everything visible on screen is passed to the AI**, so read the warning in the approval window before allowing.
- **Pictures and documents** — Draw pictures (needs image generation set up) and build HTML results such as charts.
- **Google** — Calendar, Tasks, Drive, and Docs. Connect your account in Settings → API with your own Google OAuth client. Calendar, mail, and task tools work in character sessions only; Drive and Docs also work in coding sessions.
- **Mail** — Read mail, save drafts, send, move to and restore from trash, and clean up spam on connected accounts (Gmail, or IMAP/SMTP accounts you add in settings).
  - Sending, deleting, and marking spam always show the content and ask for approval; "Allow for this session" is not offered. Deleting moves mail to the trash, so it can be reversed.
  - Add work or internet mail in Settings → API → Mail accounts. Enter the address, port, and security mode for the incoming (IMAP) and outgoing (SMTP) servers, check each with **Test connection**, then save. Connections always use TLS, and login details are not sent if the certificate does not match. Some services, such as Naver and Daum, require an app password.
  - **Whether the AI may receive message bodies must be chosen per account; there is no default.** With "Do not allow", the AI sees only the subject, sender, and date.
  - For accounts that cannot hold drafts on the server, drafts are saved only on this PC. If the server does not support safe moves (MOVE or UIDPLUS), only cleanup is disabled; reading and sending still work.
- **Messaging** — Send LINE messages.

### Windows only: crash analysis and Visual Studio debugging

You can hand off finding the cause of a hang or crash. The AI only reads; it does not pause or modify your program.

- **Crash dump analysis** — Give the path to a `.dmp` file ("find the cause of this crash") and the AI reads functions, source lines, and GPU-related evidence. The analyzer (`LumiPilotDumpAnalyzer.exe`) is bundled, so **Visual Studio is not required.**
- **Live Visual Studio inspection** (optional) — When your program is stopped at a breakpoint or exception in Visual Studio, the AI reads threads, stacks, and variable values. This needs an extension. **Close all Visual Studio windows**, run `extras\LumiPilotDebugBridge.vsix` from the extracted folder (Visual Studio 2022 and 2026), then reopen Visual Studio. To confirm, check **Output → "LumiPilot Debug Bridge"** in Visual Studio. The extension is read-only: it does not add breakpoints, continue or step, change variables, or call functions. The VSIX is unsigned, so the installer may warn.

---

## 8. Lumi (the character)

Lumi is the app's built-in character and conversation partner. Lumi does not use coding tools directly; instead, **Lumi hands work to conversations.** You cannot import or choose other characters. Use the **Character** button in the sidebar to switch to the character screen.

- **Talking** — Say something in the input box and Lumi answers. The conversation so far is always visible; long-press a line for "Hear again / Send again".
- **Character settings** (the mode button in the input) — Whether delegated work starts with a plan, the approval level for sessions, how many to run at once, reasoning effort, and whether to report progress.
- **Delegating work** — Ask something like "fix the bug in this repository" and Lumi opens a coding session for it.
  - The top of the screen shows what was delegated and its state (working, waiting for approval, waiting for a reply, failed, stopped, done). Click it for a list where you can **view in chat · change tier · stop**.
  - Lumi picks a model to match the size of the job (big, normal, light). Set the per-tier models in ☰ → character model settings on the character screen.
  - When delegated work waits for approval, a single line appears above the input. **Expand** it to read the details, then answer with a button or in words. If you deny, that job stops.
- **Voice** — Turn it on in Settings → General → **Voice output** (2-4).
- **Next events card** — Shows up to 3 upcoming events in time order, combining character schedules and Google Calendar (default calendar), each labeled with its source. Click the card to open the schedule window. If the Google lookup fails, the last successful result is shown with a "lookup failed" note.
- **Tasks** — Click "N tasks left" under the events to open the Google Tasks popup. Ask Lumi to add, edit, complete, or delete; the usual approval rules apply. In Settings → API's Google connection, press **Add tasks permission**, choose the same account, and enable the Tasks API in Google Cloud.
- **Schedules** — Create one by asking ("brief me every morning at 8"), or add one in Settings → Character. Pick reminder / question / delegate work, and repeat once, daily, weekdays, weekly, or at an interval. Schedules missed while the app was closed are reported once at the next launch.
- **Morning briefing and speaking first** — Lumi can tell you today's events, unread mail, weather, and what finished overnight. Turn on "check in even without a reason" to have Lumi start conversations in the time window you set. These features work **only while the app is running**.

Lumi, the app icon, and some icons use AI-generated visual assets, and replies, generated images, and synthetic voice are labeled as AI-generated.

---

## 9. Settings reference

Open **Settings** at the bottom of the sidebar. There are ten tabs.

### General

- **Display** — Dark theme, language (Korean/English), app text size, file-change view (vertical/horizontal).
- **Model** — Provider and model used to draw pictures. With **Auto-select**, the "Current: …" line shows what is actually used.
- **Voice output** — Reading method (OS built-in TTS / voice model), turning voice output on, reading coding session replies.
- **Conversation** — Auto titles, task completion notifications, compaction ratio, context window basis (default/extended), and **auto-continue** (lets the AI keep answering when background work finishes; it costs money, so it is off by default).
- **System prompt** — An instruction added to every coding conversation (for example, "always be formal"). Characters are excluded.
- **Workspace** — Working folder, and the name and email used for git commits.
- **Allowed shell commands** — Commands the AI may run without asking again.

### API

See 2-2. If a notice at the top says **stored credentials could not be read**, the data was created on another account or PC. Enter the keys again or sign in again.

### Memory

- **Auto memory extraction** — Remembers important things from conversations. Turning it off keeps memories you saved yourself.
- **Kinds** — Work memory / character memory / character relationship.
- **Add** memories, and click an item to edit or delete it. Types are text, image, and document (a path). **Clear all** empties that kind.

### Skills

Collections of procedures the AI follows. You can ask the AI to write one, install one from a public GitHub repository, or register one yourself as a Markdown file. The Settings → Skills tab lists loaded skills with their source (built-in, user skill, workspace, plugin), an on/off switch per skill, its conditions (OS, provider), and any load warnings. After editing files, press **Reload skills**.

**Letting the AI do it**

The built-in skills `skill-creator` and `skill-installer` let you do this by asking, in a coding session (a conversation with a working folder open). You do not need to install Python or Git.

- **Creating a skill** — Ask, for example, "Make a skill for writing release notes." The AI first checks whether an existing skill already covers it, picks where to save it, writes the `SKILL.md`, and validates it. By default it goes in this project (`.agents\skills\`); to use it in every project, say so (the user skills folder). A new skill is available from the next turn.
- **Installing from GitHub** — Give the repository, for example, "Install a skill from github.com/owner/repo." The AI lists the skills in the repository, you pick one, and you choose whether it is for this project or for all projects. You are asked to **approve** just before it is installed.
  - Only public repositories work. The install is pinned to the commit (a 40-character hash) that was read when the list was made, so the same request always installs the same files.
  - Before downloading, the file list is checked, and bundles with symbolic links, submodules, executables (`.exe`, `.dll`, and similar), or more than 500 files or 20 MB are refused. If the `SKILL.md` cannot be loaded, nothing is installed, and if writing fails, the files already written are removed.
  - A skill with the same name is never overwritten. To get a newer version, delete the old folder yourself and install again.
  - If GitHub's unauthenticated request limit (60 per hour) is reached, the AI tells you when you can try again.
  - An installed skill is outside instructions. Read its `SKILL.md` and any scripts before relying on it. The caution under **Using skills** below applies as is.

**Registering one yourself**

1. **Pick a folder.** The app reads only the two locations below (plus built-in and plugin skills). Create the folder if it does not exist.

   | Scope | Location |
   |---|---|
   | User skills (all projects) | `%APPDATA%\LumiPilot\LumiPilot\config\skills\` |
   | Workspace skills (that project only) | `<working folder>\.agents\skills\` |

   If names collide, the earlier one wins in this order: workspace, user, plugin, built-in. Claude Code's `.claude\skills\` and a `skills\` folder in the working folder are not read, so copy skills you already use into one of the folders above.

2. **Create a skill folder with a `SKILL.md`.**

   ```text
   .agents\skills\
   └─ release-notes\          ← folder name = skill name
      ├─ SKILL.md             ← required
      ├─ references\          ← detail read only when needed (optional)
      ├─ scripts\             ← tools to run repeatedly (optional)
      └─ assets\              ← files to copy into results (optional)
   ```

   `SKILL.md` starts with a header fenced by `---`, followed by the instructions.

   ```markdown
   ---
   name: release-notes
   description: Use when writing release notes. Do not use for a plain summary of commits.
   ---

   # Writing release notes

   1. Read the commits since the last tag.
   2. Write one English sentence for each change a user would notice.
   ```

   - `name` (required) — Lowercase letters, digits, and hyphens, up to 64 bytes, and the same as the folder name.
   - `description` (required) — Up to 1,024 bytes. **The AI decides whether to use a skill from this description alone.** Say what it does, when to use it, and which similar requests it does not cover.
   - `when` (optional) — Write `platform: [windows]` or `provider: [openai]` to list the skill only under those conditions.
   - The body cannot be empty. Prefer outcomes, selection criteria, project-specific constraints, and how to verify over general knowledge the AI already has.

3. **Reload.** Press Settings → Skills → **Reload skills** and check that it appears in the list. If the header is not closed or `description` is missing, a warning card appears at the top.

**Using skills**

- The AI picks a skill by itself when the conversation and the skill's description match.
- To name one yourself, write `$skill-name` in the input box (for example, `Write the 1.0.23 notes with $release-notes`).
- Switch off skills you do not use. If there are so many that they exceed the list budget, some are hidden from the AI; turning off unused ones fixes that too.
- Skills that come from a plugin appear as `<plugin>:<name>`.
- Skills are instructions to the AI, so use **only ones from sources you trust**. A skill does not widen tool permissions; the approval rules (chapter 5) still apply.

### Triggers (macros)

- **Macros** — Save frequently used instructions by name. When a trigger fires, the instruction is delivered.
- **Triggers** — Run automatically at set times. Types are **interval** (every N seconds) and **when an AI reply completes**.
- The whole feature is switched on or off with **Triggers** in the sidebar.

### MCP

Attach tools from outside services. **Add server** with an address and headers, and it connects automatically at startup and its tools join in. For each server you can **reconnect · edit · delete**, set **enabled and trusted**, and sign in or out if authentication is needed. Tools that only look things up can be marked **read-only** so they run without approval. Do not mark tools that change or send anything.

### Plugins

Install skills, MCP servers, hooks, and agents as one bundle. Codex and Claude Code plugin folders (`.codex-plugin`, `.claude-plugin`) work as they are. **Install from folder**, or add a **marketplace** (a plugin list in a Git repository or folder) and pick items to install. Being in the list does not install anything. Git sources are installed pinned to a commit. Plugins can run code, so install only from sources you trust.

### Character

Set up speaking first and schedules (chapter 8).

### Browser

**Site sessions** — Shows sign-in sessions the app browser remembers through cookies. Look up a site address to view or clear its cookies; clear them here to sign out or switch accounts.

### About

The app version (copyable), open-source licenses, and the usage and safety notices.

---

## 10. Notifications and background work

- **Background work** — Long commands, watchers, and helper jobs run behind the scenes without making you wait. When one ends, a completion card (last output, exit code, elapsed time) appears in the conversation.
- **System notifications** — Turn them on in Settings → General to be notified while you are not looking at the app. Completion and approval requests for work Lumi delegated also arrive as notifications.
- **Scheduled runs** — Recurring schedules and wake-ups run **only while the app is running**. If a conversation has no AI connection yet, its automatic run is skipped and the reason is noted in the conversation.

---

## 11. Security and privacy

- **Data goes where you send it.** Conversations, attachments, screen contents, and tool results are sent to the AI provider and integrations you choose. The app does not send usage statistics, conversations, or crash data to the developer. Check each provider's retention, training, and billing policies yourself. Details are in the [Data Handling Notice](../legal/en/data.txt).
- **Approvals** — Actions that change things ask before they run (except in full auto). If you do not understand what an action does, do not allow it.
- **Key storage** — API keys are stored encrypted. If migrating them to encrypted storage fails, they are blocked rather than kept in plaintext. Files exported with **Move between devices** are plaintext; delete them after moving.
- **Site sign-in** — The app does not store site passwords. Only the sign-in state from your own sign-in in the built-in browser is kept, in the app's dedicated profile.
- **Location** — If you do not allow it when the AI asks for your location, the app reports that permission was denied. It does not estimate location from your IP address.
- **Cost** — The app is free, but external AI subscriptions, APIs, and integrations may cost money. The app's token and budget displays do not guarantee the provider's actual billing limits.
- **AI can be wrong.** Review changes before relying on them.

Legal documents: [License](../legal/en/license.txt) · [Usage & Safety](../legal/en/usage.txt) · [Data Handling](../legal/en/data.txt)

---

## 12. Troubleshooting

| Symptom | What to try |
|---|---|
| The app will not open | Check the log (`%APPDATA%\LumiPilot\LumiPilot\data\log\app.log`) and the error records (`data\CrashLogs`). If the last exit was abnormal, the app tells you why on the next launch. |
| The model list is empty | Check that you entered a key in Settings → API, then press **↻** in the sidebar. |
| Sending shows the connection setup window | No AI connection is set up yet. Choose the service, authentication, and model, then press **Start**. |
| Claude/Gemini subscription sign-in does not work | Subscription sign-in for both is disabled in this version. Connect with an API key instead. |
| Commands do not run | Git for Windows is required. It is detected automatically once installed. |
| The browser will not open | Check that the Microsoft Edge WebView2 Runtime is installed. |
| Windows shows a warning on first run | The release has no code signature, so SmartScreen may warn. Verify the download with the SHA-256 steps in the [README](../README.md#download). |
| Visual Studio inspection does not work | Check that `LumiPilotDebugBridge.vsix` was installed with all Visual Studio windows closed, and that "LumiPilot Debug Bridge" in the Output window shows a running line. Crash dump analysis works without the extension. |
| Google tools are missing | Connect a Google account in Settings → API. You must register the client ID, secret, and redirect address. |
| The AI cannot open a site that needs sign-in | Open the site in the in-app browser and sign in yourself. The AI uses your signed-in state. |
| Stored keys cannot be read | The data was created on another account or PC. Enter the keys again or sign in again. |
| A reply was cut off | It was too long. Ask again in smaller pieces. |
| The AI stopped after repeating the same action | It stopped itself after calling the same tool over and over. Change your instruction and try again. |
| No voice is heard | For OS TTS, check that the Windows voice language is installed. For a voice model, check the ElevenLabs key and credits. |
| Usage limit error | Wait and retry, or switch to another model or key. |

If that does not help, ask in the [official LumiPilot Discord](https://discord.gg/e3j5EnK3J) or email **lumipilothelp@gmail.com**. Include the version, time, permission mode, symptom, and steps to reproduce. Do not send API keys, passwords, entire conversations, or whole repositories.
