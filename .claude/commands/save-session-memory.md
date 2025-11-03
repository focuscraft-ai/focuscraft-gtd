**ACTION REQUIRED**: Use the Task tool to invoke the session-memory agent immediately.

Do NOT wait for automatic execution. Invoke the agent now.

**Agent**: session-memory
**Subagent type**: session-memory
**Purpose**: Proactively capture and organize important information from the current session for cross-session persistence.

Execute the "Session Memory Capture" workflow.

The agent will:
1. Review the current conversation session
2. Extract key information:
   - Workflow changes or new workflows created
   - Lessons learned and mistakes corrected
   - Important person insights and context
   - Project decisions and milestones
   - Reference knowledge worth preserving
   - System improvements (agents, commands, processes)
3. Categorize by type and determine save location:
   - Workflow changes → CLAUDE.md updates
   - Lessons learned → CLAUDE.md "Important Lessons Learned"
   - Person insights → People/[username].md Notes sections
   - Project decisions → Project Log sections
   - Reference material → Reference/ appropriate subfolders
4. Check for duplicates (avoid re-saving existing information)
5. Present summary of items to save for your approval
6. After confirmation, save to appropriate files
7. Report what was saved and where

**When to use**:
- End of work sessions (before vacation, end of day)
- After significant work (new workflows, major decisions)
- When you want to preserve session insights

**Benefits**:
- Automatic capture (not manual documentation)
- Organized by type and purpose
- Prevents loss of important insights
- Keeps CLAUDE.md focused (details go to Reference/)
- Makes knowledge discoverable for future sessions

This complements `/export-session` - raw conversation export + organized memory capture.
