Execute the "Task Archival Workflow" as defined in CLAUDE.md.

This workflow:

1. **Reads Tasks/Next.md** and identifies all completed tasks (marked [x])

2. **Counts completed tasks** and reports to user

3. **Moves completed tasks** to Archive/Tasks/Next.md:
   - Preserves @office/@home context structure
   - Adds at top (newest first by completion date)
   - Keeps full metadata
   - Extracts completion date from ✅ YYYY-MM-DD marker

4. **Removes from active list** - Deletes archived tasks from Tasks/Next.md

5. **Updates archive metadata** - "Last archived" date and total count

6. **Reports summary**:
   - X tasks archived
   - Archive location
   - Next.md cleaned up

**When to run**:
- After significant work sessions
- When completed tasks accumulate (10+ suggested threshold)
- Before starting new work cycles
- When Tasks/Next.md feels cluttered

**Purpose**: Keep active task list focused on actionable items, preserve history in archive.

**Time saved**: ~2-3 minutes per cleanup vs manual cut/paste
