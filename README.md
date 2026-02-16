# AgentTerm

**Click any file path, traceback, or symbol in your terminal to jump straight to your IDE.**

A purpose-built terminal for AI-assisted development. AgentTerm watches output in real time and turns every reference into a clickable link — no copy-paste, no manual navigation.

Built for workflows with Claude Code, Cursor, and similar AI coding tools that produce dense file references.

## Why

AI coding assistants dump dozens of file paths per response. Copying, switching windows, and manually navigating is slow. AgentTerm watches terminal output in real time and makes every reference instantly clickable.

## Features

**Intelligent Click Targets**
- File paths with line numbers (`src/main.js:42`, `file.py:10:5`, `File "path.py", line 42`)
- GitHub-style references (`file.js#L42-L50`)
- Qualified symbols (`ClassName.method`, `module.function`)
- Underscore identifiers (`my_var`, `_private`) with context-aware filtering
- All patterns detected proactively as output streams — no hover required

**IDE Integration**
- One-click navigation to file:line in PyCharm (via companion plugin)
- Symbol lookup with file-context hints — the terminal remembers which file was last referenced and passes it to the IDE for disambiguation
- Visual feedback: green (navigated), yellow (multiple matches), red (not found)

**Color-Matched Decorations**
- Underlines match the ANSI color of the decorated text (RGB, 256-palette, bold-bright)
- Respects SGR inverse video — reads the visually correct foreground color
- Subtle dotted underline at rest, solid + highlight on hover

**Terminal UX**
- WebGL-accelerated rendering (xterm.js)
- Windows Terminal-style copy: Enter copies selection, Ctrl+C copies or sends SIGINT depending on selection state
- Dark theme with 4px thin scrollbar (expands on hover)
- WSL shell on Windows, native shell on macOS

## Technical Approach

- **Append-only decoration engine** — only processes new rows above the cursor; never re-scans unless content drifts (handles progress spinners gracefully)
- **Overlap resolution** — longer/earlier matches win; patterns ordered by specificity
- **IPC architecture** — Electron main ↔ renderer via contextBridge; IDE communication over local TCP socket
- **Build-time trial system** — timestamp injected at build, expiration checked at launch (packaged builds only)

## Download

Get the latest release from the [Releases page](https://github.com/yunxin/agent-term-public/releases).

| Asset | Description |
|-------|-------------|
| `AgentTerm-x.x.x-setup.exe` | Windows installer |

## Stack

Electron · xterm.js (WebGL) · node-pty · esbuild
