# Shared Brain: Multi-Agent Handoff System

Welcome to the **Shared Brain**! This folder enables seamless task handoffs and state persistence across multiple AI coding agents, including **Claude Code**, **Windsurf (Cascade)**, **Cursor**, **Antigravity**, **GitHub Copilot**, **Aider**, **Roo Code/Cline**, and more.

## Core Structure
- `active_task.md`: The single source of truth for the active task, goals, subtasks, and blockers.
- `handoff.md`: The latest handoff documentation written by the outgoing agent or session.
- `temp_chat_history.md`: A live, append-only transcript of key decision points and history that syncs across devices.
- `scripts/brain.py`: The control CLI for the Shared Brain.

## How to Use

### 1. Starting a New Task
When you start a new task, run:
```bash
python .shared-brain/scripts/brain.py start "Describe your task here"
```
This initializes `active_task.md` with your description.

### 2. When an Agent Runs (Startup)
Whenever any agent starts up in this repository, it reads its corresponding rules file (e.g. `CLAUDE.md`, `.cursorrules`, `.agents/AGENTS.md`) which instructs it to:
1. Read `.shared-brain/active_task.md` and `.shared-brain/handoff.md`.
2. Keep `.shared-brain/temp_chat_history.md` updated with key steps.

### 3. Resuming / Switching Agents
If you run out of limits on one agent or switch devices/IDEs, run:
```bash
python .shared-brain/scripts/brain.py resume
```
This script will scan:
- Uncommitted/local file changes (even autosaved files modified in the last 4 hours).
- Git diffs and recent `WIP` commits.
- Conversation logs and transcripts (both local agent logs and the synced `temp_chat_history.md`).

It compiles a comprehensive **Context Summary** tailored for the incoming agent, which you can paste directly into the new agent's chat, or which the agent will automatically read on startup.

### 4. Completing a Session (Handoff)
Before switching or ending a session, run:
```bash
python .shared-brain/scripts/brain.py handoff
```
This archives the current task state, prompts for progress details, and prepares a clean handoff for the next session.
