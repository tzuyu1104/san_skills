# Ask — Code Q&A for OpenCode

Ask is a read-only Q&A agent for [OpenCode](https://opencode.ai). It answers questions about your codebase — explains how things work, finds relevant code, explores architecture, and provides deep insights — without ever editing your files.

Powered by your existing OpenCode model. No extra API keys. No subscriptions.

The original code is from github.com/MRZ07/ask under MIT license. Because the original github repository is broken, I backup it here.

---

## Quick Start

### Install

1. Clone this repo or download `ask.js`
2. Copy or symlink `ask.js` to your OpenCode config plugins:
   ```bash
   mkdir -p ~/.config/opencode/plugins
   cp ask.js ~/.config/opencode/plugins/ask.js
   ```
3. Add to `~/.config/opencode/opencode.json`:
   ```json
   {
     "plugin": ["./plugins/ask.js"]
   }
   ```
4. Restart OpenCode.

### Use

Ask is available both as a **general agent** (selectable in OpenCode's agent picker) and via `@ask` in any conversation:

- **General mode** — Select "Ask" from the agent list for a dedicated Q&A session
- **Subagent mode** — Type `@ask how does collision work?` mid-conversation

Ask will explore the codebase, gather context, and give you a thorough answer — complete with file paths, line numbers, and architectural context.

---

## How It Works

Ask is an OpenCode plugin that registers a `subagent` named `ask`. When invoked, the agent:

1. **Explores** — searches your codebase with grep, glob, and targeted file reads
2. **Analyzes** — traces code paths, understands architecture, identifies patterns
3. **Answers** — provides a clear, structured response with source citations
4. **Never edits** — the agent has `edit: deny` and `write: deny` baked in

---

## vs. GitHub Copilot `/ask`

| | GitHub Copilot `/ask` | OpenCode **Ask** |
|---|---|---|
| **Scope** | Current file + editor selection | Full workspace exploration |
| **Search tools** | None (inline context only) | grep, glob, read, bash, web |
| **Architecture awareness** | Limited to visible code | Deep — traces across files and layers |
| **Permission model** | Read-only by convention | Enforced: `edit: deny`, `write: deny` |
| **Invocation** | In-editor chat panel | `@ask` in any OpenCode conversation |
| **Model** | Copilot's model | Your configured OpenCode model |
| **Subagent dispatch** | No | Yes — can delegate parallel searches via `task` |
| **Custom prompt** | Fixed | Open source — fork and customize |
| **Offline** | No (cloud only) | Depends on your model provider |

### When to use which

**Use Copilot `/ask`** when you need a quick answer about the file or selection you're actively editing — minimal context switching.

**Use OpenCode Ask** when you need deep understanding — tracing logic across many files, understanding architecture, investigating bugs, or orienting yourself in an unfamiliar codebase.

---

## Permissions

| Tool | Access |
|------|--------|
| `read` | `allow` |
| `grep` | `allow` |
| `glob` | `allow` |
| `bash` | `git *: allow, *: ask` |
| `webfetch` | `allow` |
| `websearch` | `allow` |
| `task` | `allow` |
| `edit` | `deny` |
| `write` | `deny` |

---

## License

MIT

