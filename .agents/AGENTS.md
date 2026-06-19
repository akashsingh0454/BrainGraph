# Antigravity Rules & Handoff Instructions

Before doing any work, you MUST check if `.shared-brain/` contains active task details.

## Startup Protocol
1. Read `.shared-brain/active_task.md` and `.shared-brain/handoff.md` to see the current active task state.
2. Read `.shared-brain/resume_context.md` if it exists.

## During Work
1. Update `.shared-brain/active_task.md` as you complete tasks.
2. Log key updates (1-2 sentences) of your progress to the bottom of `.shared-brain/temp_chat_history.md` with:
   `- **[Timestamp] [Antigravity]**: Summary of what you just did.`
   This is critical for multi-device sync and crash recovery!

## Handoff Protocol
When you are finishing or if your limits are running low:
- Run `python .shared-brain/scripts/brain.py handoff` or ask the user to run it to archive the task and prepare a clean handoff.
