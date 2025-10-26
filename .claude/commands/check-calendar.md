Execute the "Check Calendar Workflow" as defined in CLAUDE.md.

**IMPORTANT**: Always run this workflow using the dedicated **meeting-prep** agent.

The agent will:

1. **Get today's events**:
   - Try MS Graph MCP to list today's calendar events
   - Fall back to Daily/YYYY-MM-DD.md if MCP unavailable

2. **Skip non-meeting events**:
   - All-day events, "Free" time, "Lunch", "Break", "Out of office"

3. **Process each meeting**:
   - **1:1 Meetings** (2 attendees):
     - Check/create person page in People/
     - Prepare agenda based on person context
     - Start with "Go Through TODOs"
   - **Group Meetings** (3+ attendees):
     - Summarize meeting context
     - Extract preparation needs

4. **Write agendas** to Daily/YYYY-MM-DD.md under "## Meeting Agendas for Today"

**When to run**:
- Morning before meetings start
- When meeting schedule changes
- Before important 1:1s to refresh context

**Purpose**: Be prepared for every meeting with relevant context and clear agendas.

**Time saved**: ~3-5 minutes per meeting × 3-4 meetings/day = 10-20 minutes/day
