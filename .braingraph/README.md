# BrainGraph: Contextual Multi-Agent Handoff System

Welcome to **BrainGraph**! This system enables seamless task handoffs and state persistence across multiple AI coding agents, including **Claude Code**, **Windsurf (Cascade)**, **Cursor**, **Antigravity**, **GitHub Copilot**, **Aider**, **Roo Code/Cline**, and more, utilizing code dependency mapping for highly accurate handoffs.

## Core Structure
- `active_task.md`: The single source of truth for the active task, goals, subtasks, and blockers.
- `handoff.md`: The latest handoff documentation written by the outgoing agent or session.
- `temp_chat_history.md`: A live, append-only transcript of key decision points and history that syncs across devices.
- `active_graph.md`: Auto-generated Mermaid dependency flow mapping your active changes and their downstream impacts.
- `agents.json`: Persistent agent usage and availability states.
- `scripts/braingraph.py`: The control CLI for BrainGraph.

## How to Use

### 1. Starting a New Task
When you start a new task, run:
```bash
python .braingraph/scripts/braingraph.py start "Describe your task here"
```
This initializes `active_task.md` and starts the watchdog daemon.

### 2. When an Agent Runs (Startup)
Whenever any agent starts up in this repository, it reads its corresponding rules file (e.g. `CLAUDE.md`, `.cursorrules`, `.agents/AGENTS.md`) which instructs it to:
1. Read `.braingraph/active_task.md`, `.braingraph/handoff.md`, and `.braingraph/resume_context.md`.
2. Register its process: `python .braingraph/scripts/braingraph.py register`.
3. Keep `.braingraph/temp_chat_history.md` updated with key steps.

### 3. Resuming / Switching Agents
If you run out of limits on one agent or switch devices/IDEs, run:
```bash
python .braingraph/scripts/braingraph.py resume
```
This script will scan local modifications, git status, WIP commits, and **parse Graphify's call graph** (`graphify-out/graph.json`) to find all downstream symbols affected by your changes. It outputs:
- **Mermaid Callflow**: Generates a dependency visualizer in `.braingraph/active_graph.md`.
- **Context Summary**: Saves the consolidated resumption context to `.braingraph/resume_context.md`.

### 4. Completing a Session (Handoff)
Before switching or ending a session, run:
```bash
python .braingraph/scripts/braingraph.py handoff
```
This archives the current task state, stops the watchdog daemon, and prepares a clean handoff document.
