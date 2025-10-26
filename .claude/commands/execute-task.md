Execute the "Execute Task Workflow" using the execute-task agent as defined in CLAUDE.md.

**Usage**: `/execute-task [task description or number]`

**Examples**:
- `/execute-task Draft email to John about project status`
- `/execute-task 5` (task #5 from Tasks/Next.md)
- `/execute-task Prepare Q review agenda for Sarah`

**What it does**:
1. Finds the task in Tasks/Next.md
2. Gathers context from vault, emails, meetings, documents
3. Creates deliverables (emails, documents, analysis)
4. Updates task status (COMPLETE, REVIEW, BLOCKED, WAITING)
5. Reports what was created and next steps

**Agent**: execute-task (autonomous execution)
