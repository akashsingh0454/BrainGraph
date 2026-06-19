# Shared Brain: Multi-Agent Handoff System

This repository provides a unified handoff system ("Shared Brain") to enable seamless project state and task resumption across multiple AI coding agents, including **Claude Code**, **Windsurf (Cascade)**, **Cursor**, **Antigravity**, **GitHub Copilot**, **Aider**, **Roo Code/Cline**, and more.

It is particularly useful for switching between different AI tools or across multiple devices without losing context or leaving work half-done.

---

## Quick Start

### 1. How It Works
The system uses:
1. **Startup Rules Configuration**: Agent rule files (`CLAUDE.md`, `.cursorrules`, etc.) are placed in the root directory to automatically instruct any active agent to read the current task and handoff state before starting.
2. **Central State Folder (`.shared-brain/`)**: Houses the active task description (`active_task.md`), the latest handoff details (`handoff.md`), and the live, cross-device synced chat history (`temp_chat_history.md`).
3. **CLI Sync Utility (`.shared-brain/scripts/brain.py`)**: A standalone, zero-dependency Python script to manage tasks and automatically reconstruct context from git changes, WIP commits, local agent logs (e.g. Antigravity transcripts), and files modified on the filesystem.

For detailed setup and instructions, see the [.shared-brain README](file:///.shared-brain/README.md).

---

## Commands Reference

Run the control CLI inside your project:

```bash
# Initialize Shared Brain rules and folder structures in any repository
python .shared-brain/scripts/brain.py init

# Start a new task
python .shared-brain/scripts/brain.py start "Your Task Description"

# Resume active task, scanning filesystem changes, git history, and harvesting chats
python .shared-brain/scripts/brain.py resume

# End session, archive active task/chat states, and generate a handoff file
python .shared-brain/scripts/brain.py handoff
```
