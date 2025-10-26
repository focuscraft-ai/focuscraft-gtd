Execute the "GTD Daily Workflow - Phase 2: Clarify (Prepare Tasks)" as defined in CLAUDE.md.

Use the **task-preparer** agent to:

1. Read all tasks in Tasks/Next.md
2. Analyze each task for:
   - Clarity (is the action clear?)
   - Completeness (all metadata present?)
   - Complexity (single task or hidden project?)
   - Dependencies (any blockers?)

3. Generate Task Preparation Report with:
   - Well-formed tasks (ready to execute)
   - Tasks needing improvement (with specific suggestions)
   - Potential projects (too complex for single task)
   - Questions for user input

4. Write report to Daily/YYYY-MM-DD.md under "## Task Preparation Report"

**Purpose**: Ensure all tasks are actionable and ready for prioritization.

**Time**: ~5-10 minutes to review report and clarify vague tasks

**Next step**: Run `/prioritize-tasks` to get today's priorities
