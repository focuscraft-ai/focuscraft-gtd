Execute the "GTD Daily Workflow - Phase 1: Collect (Scan All Inboxes)" as defined in CLAUDE.md.

This workflow runs scanner agents sequentially:

## Scanner Sequence

1. **Email Inbox** (email-scanner agent):
   - Try MS Graph MCP first, fall back to `Inbox/emails/` files
   - Extract actionable tasks from emails
   - Write tasks to Tasks/Next.md
   - Mark emails as read (MCP) or move files (File mode)

2. **Meetings Folder** (meeting-scanner agent):
   - Try MCP meeting tools first, fall back to `Inbox/meetings/` files
   - Scan meeting notes for TODOs and action items
   - Create tasks with meeting context
   - Move processed files to Reference/Meetings/

**Final Report**: Summarize results from all scanners and write to Daily file.

**Note**: This is the core inbox processing workflow - designed to be run at the start of each day or whenever inboxes need clearing.
