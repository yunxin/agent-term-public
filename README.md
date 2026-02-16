# AgentTerm

**Click any file:line, symbol, or traceback in your terminal to jump straight to your IDE.**

A purpose-built terminal for AI-assisted development. AgentTerm watches output in real time and turns every reference into a clickable link — no copy-paste, no manual navigation.

Built for workflows with Claude Code, Cursor, and similar AI coding tools that produce dense file references.

## Why

AI coding assistants dump dozens of file paths per response. Copying, switching windows, and manually navigating is slow. AgentTerm makes every reference instantly clickable — file paths, symbols, tracebacks, and more.

## Performance

Zero perceptible overhead. The decoration engine is append-only and single-pass — each row is processed exactly once as it streams in, with no re-scanning or viewport traversal. GPU-accelerated rendering keeps the terminal native-fast even with thousands of active links on screen.

## Architecture

- **Append-only stream processing** — pattern detection runs incrementally on new output, O(new rows) not O(total rows)
- **IPC over contextBridge** — sandboxed renderer communicates with the host process through a minimal typed API
- **IDE integration via local TCP socket** — two companion plugins: a backend plugin
  resolves files/symbols and moves the caret (port 8765), a frontend plugin scrolls
  the editor to the target line (port 8766)
- **Cross-platform shell management** — WSL on Windows, native PTY on macOS

## Download

Get the latest release from the [Releases page](https://github.com/yunxin/agent-term-public/releases).

| Asset | Description |
|-------|-------------|
| `AgentTerm-x.x.x-setup.exe` | Windows installer |
| `intellij-navigator-1.0.0.zip` | IntelliJ backend plugin (file/symbol resolution, port 8765) |
| `intellij-navigator-frontend-1.0.0.zip` | IntelliJ frontend plugin (editor scroll, port 8766) |

**Currently available for Windows (WSL) only.** Support for macOS, native Windows (non-WSL), and Linux can be added on request.

## Setup

Install both IntelliJ plugins via **Settings → Plugins → ⚙ → Install Plugin from Disk**.

| Environment | Where to install |
|-------------|-----------------|
| **Local** | Install both plugins in your IDE |
| **Remote dev** | Install backend plugin on the host IDE, frontend plugin on the client IDE |

## Stack

Electron · xterm.js (WebGL) · node-pty · esbuild
