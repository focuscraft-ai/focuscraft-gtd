Execute the "Weekly Planning Workflow" using the weekly-planner agent.

**ACTION REQUIRED**: Use the Task tool to invoke the weekly-planner agent immediately.

Do NOT wait for automatic execution. Invoke the agent now.

**Agent**: weekly-planner
**Subagent type**: weekly-planner
**Purpose**: Create comprehensive weekly plan from today through end of current week

**What it does**:
1. Analyzes calendar load (today through Sunday)
2. Identifies meeting-project connections (what to discuss in 1:1s)
3. Gathers tasks with deadlines and urgent items
4. Prioritizes projects by criteria (High/Medium/Lower with reasoning)
5. Creates daily schedule recommendations (detailed for critical days)
6. Generates success criteria (must/nice/defer based on cognitive load)
7. Saves weekly plan to `Weekly/YYYY-W##.md`

**Output**: Weekly plan file showing focus, priorities, meeting opportunities, and what to tackle first.
