Execute the "Email Inbox Scanning Workflow" using the email-scanner specialized agent.

The agent will:
1. Try MS Graph MCP first to read unread emails
2. Fall back to scanning Inbox/emails/ folder if MCP unavailable
3. Filter out automated notifications (system emails, calendar, etc.)
4. Process each actionable email with deep understanding
5. Extract tasks, responses needed, decisions, and delegations
6. Assess complexity and detect hidden projects
7. Write tasks to Tasks/Next.md with full metadata
8. Mark emails as read (MCP) or move files (File mode)
9. Write complete report to Daily/YYYY-MM-DD.md

**Hybrid Mode**: Works with or without MCP setup (file-based by default).

This is part of the GTD inbox collection workflow.
