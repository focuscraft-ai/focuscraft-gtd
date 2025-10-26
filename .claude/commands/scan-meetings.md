Execute the "Meeting Notes Scanning Workflow" using the meeting-scanner specialized agent.

The agent will:
1. Try MCP meeting tools first (if available)
2. Fall back to scanning Inbox/meetings/ folder for meeting note files
3. Extract TODOs and action items
4. Create tasks in Tasks/Next.md with full metadata
5. Move processed meeting files to Reference/Meetings/
6. Write detailed report to Daily file

**Hybrid Mode**: Works with or without MCP setup (file-based by default).

This is part of the GTD inbox collection workflow.
