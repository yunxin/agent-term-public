# AgentTerm

**Click any file path, traceback, or symbol in your terminal to jump straight to your IDE.**

A purpose-built terminal for AI-assisted development. AgentTerm watches output in real time and turns every reference into a clickable link — no copy-paste, no manual navigation.

Built for workflows with Claude Code, Cursor, and similar AI coding tools that produce dense file references.

## Why

AI coding assistants dump dozens of file paths per response. Copying, switching windows, and manually navigating is slow. AgentTerm makes every reference instantly clickable — file paths, tracebacks, symbols, and more.

## Performance

Zero perceptible overhead. The decoration engine is append-only and single-pass — each row is processed exactly once as it streams in, with no re-scanning or viewport traversal. GPU-accelerated rendering keeps the terminal native-fast even with thousands of active links on screen.

## Architecture

- **Append-only stream processing** — pattern detection runs incrementally on new output, O(new rows) not O(total rows)
- **IPC over contextBridge** — sandboxed renderer communicates with the host process through a minimal typed API
- **IDE integration via local TCP socket** — companion plugin turns the IDE into a navigation server; the terminal sends structured commands for file/line/symbol resolution
- **Cross-platform shell management** — WSL on Windows, native PTY on macOS

## Download

Get the latest release from the [Releases page](https://github.com/yunxin/agent-term-public/releases).

| Asset | Description |
|-------|-------------|
| `AgentTerm-x.x.x-setup.exe` | Windows installer |
| `intellij-navigator-1.0.0.zip` | IntelliJ plugin (IDE companion) |

## Stack

Electron · xterm.js (WebGL) · node-pty · esbuild
