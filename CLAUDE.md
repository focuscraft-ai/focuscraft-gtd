# FocusCraft GTD System - Claude AI Guide

**Version**: 0.9.1
**Last Updated**: 2025-10-26

A comprehensive GTD (Getting Things Done) system powered by Claude AI agents. This system provides complete automation for task collection, preparation, prioritization, and execution.

## Quick Reference

### Slash Commands
- **`/check-calendar`** → [Check Calendar Workflow](#check-calendar-workflow) - Prepare today's meeting agendas
- **`/update-meetings [date]`** → [Meeting Update Workflow](#meeting-update-workflow) - Update meeting agendas (optional: yesterday, YYYY-MM-DD)
- **`/execute-task [task]`** → [Execute Task Workflow](#execute-task-workflow) - Autonomously execute task from Next.md
- **`/archive-tasks`** → [Task Archival Workflow](#task-archival-workflow) - Move completed tasks to archive
- **`/scan-inboxes`** → [GTD Daily Workflow - Phase 1](#phase-1-collect-scan-all-inboxes) - Scan all inboxes and collect tasks
- **`/scan-emails`** → Scan email inbox only
- **`/scan-meetings`** → Scan Inbox/meetings/ folder only
- **`/prepare-tasks`** → [GTD Daily Workflow - Phase 2](#phase-2-clarify-prepare-tasks) - Clarify and improve task quality
- **`/prioritize-tasks`** → [GTD Daily Workflow - Phase 3](#phase-3-organize--prioritize) - Get priority recommendations

### Common Workflows
- **Daily workflow**: `/scan-inboxes` → `/prepare-tasks` → `/prioritize-tasks` → [GTD Daily Workflow](#gtd-daily-workflow) - Complete task management from inbox to execution
- **Morning routine**: Check calendar → Scan inboxes → Prioritize tasks
- **After meeting**: Say "meeting with [person] done" → [Meeting Update Workflow](#meeting-update-workflow) - Auto-update next agenda
- **Archive tasks**: `/archive-tasks` → [Task Archival Workflow](#task-archival-workflow) - Move completed tasks to archive

### Key File Locations
- **Person pages**: `People/[username].md` - Meeting agendas and context for individuals
- **Project files**: `Projects/[Project Name]/` - Each project has dedicated folder
- **Daily notes**: `Daily/YYYY-MM-DD.md` - Daily journal with meeting agendas
- **Drafts**: `Drafts/YYYY-MM-DD - [Title].md` - Work-in-progress deliverables
- **Tasks**: `Tasks/Next.md` - All active tasks organized by context
- **Projects index**: `Projects/Projects.md` - Central list of all active projects

### Important Rules
- **Person pages** go in `People/` folder
- **All deliverables** start in `Drafts/` folder with date prefix
- **Tasks** organized by context: @office (work) and @home (personal)
- **Meeting agendas**: Default = Operational Focus (2 weeks)

---

## Core Principle

**CLAUDE.md serves as a shared knowledge base for all Claude sessions and subagents.** All workflows, processes, and work-in-progress states must be documented clearly enough for any agent to understand and continue the work.

## System Architecture

### Two Modes of Operation

**File-Based Mode** (Works out of the box):
- Inboxes are folders with markdown files
- Agents scan files and extract tasks
- No external integrations needed
- Perfect for getting started

**MCP-Enhanced Mode** (Optional):
- Connect Microsoft 365 (calendar, email)
- Connect Atlassian (Confluence, Jira)
- Connect macOS Reminders
- Enhanced automation and live data

**IMPORTANT**: All agents are designed to work in BOTH modes. They try MCP tools first, fall back to file scanning if MCP unavailable.

## Slash Commands

Custom slash commands are defined in `.claude/commands/` directory. Each command is a markdown file that references workflows documented in CLAUDE.md.

**How Slash Commands Work**:
- Slash command files contain prompts that execute workflows
- Commands reference workflows by name (e.g., "Meeting Update Workflow")
- All workflow logic stays in CLAUDE.md (single source of truth)
- Slash commands are just convenient triggers

**Available Commands**:
- `/check-calendar` - Prepare agendas for today's upcoming meetings
- `/update-meetings [date]` - Update meeting agendas for specific date
- `/scan-inboxes` - Run all inbox scanners sequentially
- `/scan-emails` - Scan email inbox only
- `/scan-meetings` - Scan meetings folder only
- `/prepare-tasks` - Review task quality and clarity
- `/prioritize-tasks` - Get priority recommendations for today
- `/archive-tasks` - Move completed tasks to archive

## Specialized Agents

Specialized agents handle specific types of tasks independently, preserving main session context.

### Available Agents

**inbox-scanner** - File-based inbox processor (Hybrid mode)
- **Purpose**: Scan file-based inboxes or Reminders app
- **Capabilities**: Extract tasks from Inbox/ folder markdown files or macOS Reminders
- **Mode**: Hybrid - tries Reminders MCP, falls back to Inbox/tasks/ files

**email-scanner** - Email inbox processor (Hybrid mode)
- **Purpose**: Extract actionable tasks from email
- **Capabilities**: MS Graph email reading or Inbox/emails/ file scanning
- **Mode**: Hybrid - tries MS Graph MCP, falls back to Inbox/emails/ files

**meeting-scanner** - Meeting notes processor (Hybrid mode)
- **Purpose**: Extract TODOs from meeting notes
- **Capabilities**: Scan Inbox/meetings/ folder, extract action items, move to Reference
- **Mode**: Hybrid - tries MCP meeting tools, falls back to Inbox/meetings/ files
- **Agent file**: `.claude/agents/meeting-scanner.md`

**task-preparer** - Task quality reviewer
- **Purpose**: Review tasks for clarity and completeness
- **Capabilities**: Analyze Tasks/Next.md, identify improvements, suggest project promotions
- **Used by**: `/prepare-tasks` command
- **Agent file**: `.claude/agents/task-preparer.md`

**prioritizer** - Priority recommender
- **Purpose**: Suggest daily priorities based on context
- **Capabilities**: Analyze calendar, energy, urgency, duration; generate daily focus lists
- **Used by**: `/prioritize-tasks` command
- **Agent file**: `.claude/agents/prioritizer.md`

**meeting-prep** - Meeting agenda preparer (Hybrid mode)
- **Purpose**: Prepare meeting agendas for today's meetings
- **Capabilities**: Calendar reading (MCP or file), person page management, agenda preparation
- **Mode**: Hybrid - tries MS Graph calendar, falls back to Daily/ note structure

**execute-task** - Autonomous task executor (Hybrid mode)
- **Purpose**: Execute tasks end-to-end from Tasks/Next.md
- **Capabilities**: Context gathering, deliverable creation, task status updates
- **Mode**: Hybrid - uses MCP tools when available (emails, calendar, Confluence), falls back to file-based context
- **Agent file**: `.claude/agents/execute-task.md`

## Vault Structure

### Core Directories

- **`Inbox/`** - File-based inboxes for task collection
  - `Inbox/emails/` - Email-like messages as markdown files
  - `Inbox/meetings/` - Meeting notes awaiting processing
  - `Inbox/tasks/` - Miscellaneous tasks from various sources
  - `Inbox/other/` - Other items needing processing
- **`Tasks/`** - Task management
  - `Tasks/Next.md` - All active tasks organized by context
  - `Tasks/Archive/` - Completed tasks archive
- **`Projects/`** - Project management
  - `Projects/Projects.md` - Central project index
  - `Projects/[Project Name]/` - Individual project folders
  - `Projects/Archive/` - Archived completed projects
- **`People/`** - Person pages for 1:1 relationships
  - `People/[username].md` - Individual person pages
- **`Daily/`** - Daily notes and logs
  - `Daily/YYYY-MM-DD.md` - Daily journal entries
- **`Drafts/`** - Work-in-progress deliverables
  - Format: `YYYY-MM-DD - [Title].md`
- **`Reference/`** - Permanent reference material
  - `Reference/Concepts/` - Frameworks, methods, workflows
  - `Reference/Templates/` - Reusable templates
- **`Archive/`** - Historical content
  - `Archive/Tasks/` - Old completed tasks
  - `Archive/Projects/` - Old completed projects
  - `Archive/Meetings/` - Old meeting notes
- **`Templates/`** - Note templates

### Configuration Directories

- **`.claude/`** - Claude Code configuration
  - `.claude/commands/` - Custom slash commands
  - `.claude/agents/` - Specialized agent definitions

## Task Management

### Task Contexts

Tasks in `Tasks/Next.md` are organized by context:

- **`@office`** - Work tasks that require office resources or work hours
- **`@home`** - Personal tasks that can be done at home
- **`@anywhere`** - Tasks that can be done anywhere (phone calls, quick decisions)

### Task Metadata Format

```markdown
- [ ] Clear, actionable task description
  - Due: YYYY-MM-DD or "None"
  - Duration: 10min, 30min, 1hr, 2hr (estimate)
  - Energy: high/medium/low
  - Source: [Where this task came from]
  - Person: [[People/username]] (if related to someone)
  - Note: Additional context
```

### Project vs Task Decision

**Use simple task when:**
- Single action item
- Can be done in one session
- No dependencies
- Clear outcome

**Create project when:**
- Multiple steps required
- Needs research or planning
- Has dependencies
- Deliverables need drafting

## Project File Structure

Each project should include these sections:

- **Tasks** - Organized by category with checkboxes and completion dates
- **Log** - Chronological updates and decisions
- **Information** - Project context, requirements, and key details
- **Related Links** - Relevant resources and references

## Person Pages Workflow

Person pages are stored in the `People/` folder as `username.md` files.

### Recommended Person Page Structure

```markdown
---
tags:
  - "#person"
---
# [Full Name]
**Username**: username
**Role**: [Title/Position]
**Department**: [Department]

## Links
- [External profile or work page](URL)
- [1-on-1 Notes](link if recurring)

## Meeting Agenda
**Next meeting**: YYYY-MM-DD

1. **Go Through TODOs** from last meeting
2. [Topic from recent email or discussion]
3. [Follow-up on ongoing project]
4. [New item to discuss]

## Notes
[Key information, observations, relationship context]
```

## Automated Workflows

### GTD Daily Workflow

**Workflow Name**: "GTD Daily Workflow"
**Purpose**: Complete task management system from inbox collection to execution

This is the **recommended daily workflow** for managing all tasks using the GTD (Getting Things Done) methodology.

#### Phase 1: Collect (Scan All Inboxes)

**Command**: `/scan-inboxes`
**When**: Morning (start of workday) or whenever inboxes need processing

**What it does**: Runs scanner agents sequentially to collect all tasks from:

1. **File-Based Inboxes** (or Reminders app if MCP available)
   - Scan `Inbox/tasks/` folder for markdown files
   - Each file represents a task or reminder
   - Extract task details and context
   - Write to Tasks/Next.md
   - Archive processed files to Inbox/tasks/processed/

2. **Email Inbox** (file-based or MS Graph if MCP available)
   - Scan `Inbox/emails/` folder for email-like markdown files
   - OR: Read unread emails from MS Graph API
   - Filter automated notifications
   - Extract actionable tasks
   - Write tasks to Tasks/Next.md
   - Move processed files to Inbox/emails/processed/

3. **Meetings Folder** (meeting-scanner agent)
   - Try MCP meeting tools first, fall back to `Inbox/meetings/` files
   - Scan meeting notes for TODOs and action items
   - Create tasks with meeting context
   - Move processed files to Reference/Meetings/

**Result**: All tasks collected in `Tasks/Next.md`, complete scan reports in Daily page

**Key Feature**: Inbox folders are completely cleared after processing

---

#### Phase 2: Clarify (Prepare Tasks)

**Command**: `/prepare-tasks`
**When**: After scanning inboxes, before prioritizing

**What it does**: Reviews all tasks for:
- **Clarity**: Are tasks specific and actionable?
- **Completeness**: Is metadata present (Duration, Energy, Due date)?
- **Complexity**: Should any tasks be projects instead?
- **Dependencies**: Are tasks blocked or need prerequisites?

**Result**: Report identifying:
- Well-formed tasks (ready to execute)
- Tasks needing improvement (with specific suggestions)
- Potential projects (too complex for single task)
- Questions needing user input

**Time**: ~5-10 minutes to review report and clarify vague tasks

**Daily File Integration**:
- Report is automatically written to `Daily/YYYY-MM-DD.md` under "## Task Preparation Report"
- When `/prepare-tasks` is rerun, the existing section is **updated** (not duplicated)

---

#### Phase 3: Organize & Prioritize

**Command**: `/prioritize-tasks`
**When**: After preparing tasks, to plan your day

**Best times**:
- Morning (8-9am) to plan full day
- After lunch (1-2pm) to plan afternoon

**What it does**: Analyzes tasks and suggests priorities based on:
- **Current time/energy** - Morning vs afternoon vs evening
- **Calendar** - Available time blocks between meetings
- **Urgency** - Due dates and deadlines
- **Energy match** - High/medium/low energy tasks vs time of day
- **Duration fit** - Tasks that fit in available time
- **Strategic value** - Project work vs administrative tasks

**Result**: Daily Priority Report with:
- **Today's Focus** (3-5 top tasks with suggested timing)
- **Quick wins** (< 15min tasks for gaps)
- **Urgent tasks** (due today/overdue)
- **Tasks due this week**
- **Tasks to consider for tomorrow**

**Time**: ~2-3 minutes to review and decide on priorities

---

#### Phase 4: Execute (Do the Work)

**Approach**: Work through Today's Focus list
- Start with highest priority task
- Match task energy to current energy level
- Use Quick Wins during gaps between meetings
- Re-prioritize if interruptions occur (run `/prioritize-tasks` again)

**Tips**:
- Block time for high-priority tasks in calendar (prevents interruptions)
- Take breaks between tasks (energy management)
- Mark tasks as complete in Tasks/Next.md as you finish them
- If stuck on a task, note the blocker and move to next task

---

#### Complete Daily Workflow Example

**Morning (8:00 AM)**:
```
1. /scan-inboxes        → Collect all tasks (10-15min)
2. /prepare-tasks       → Review clarity report (5min)
3. /prioritize-tasks    → Get today's focus (2min)
4. Work on priorities   → Execute top 3-5 tasks
```

**Mid-day (if needed)**:
```
5. /prioritize-tasks    → Re-evaluate afternoon priorities
6. Continue execution   → Work on remaining tasks
```

**End of day**:
- Review completed tasks
- Note any blockers or open questions
- Quick look at tomorrow's calendar

---

### Execute Task Workflow

**Workflow Name**: "Execute Task Workflow"
**Slash Command**: `/execute-task [task]`
**Agent**: execute-task (autonomous execution)

**Trigger**: When you want to autonomously execute a task from Tasks/Next.md

**Purpose**: Take a task from your Next.md list and execute it end-to-end: gather context, create deliverables, update task status.

**Usage**:
- `/execute-task Draft email to John about project update` - Execute by description
- `/execute-task 5` - Execute task #5 from Tasks/Next.md
- `/execute-task Prepare meeting agenda for Sarah` - Execute by task name

**Sequence** (executed by execute-task agent):

1. **Identify Task**
   - Find task in Tasks/Next.md based on description or number
   - Confirm task details with you
   - Ask: "Do you have any specific links, files, or additional context I should use?"

2. **Gather Context** (HYBRID mode)

   **Always available**:
   - Search vault for related notes, projects, people
   - Check Reference/ for templates, frameworks, examples
   - Read person pages if task involves specific people
   - Review project files if task is #project tagged

   **When MCP available**:
   - Search emails using MS Graph
   - Check calendar for meeting context
   - Read Confluence pages (Atlassian MCP)
   - Search OneDrive/SharePoint documents

   **Fallback**: If MCP unavailable, check Inbox/ folders for exported data

3. **Determine Deliverable Type**
   - Email draft → `Drafts/YYYY-MM-DD - [Subject].md`
   - Document/proposal → `Drafts/YYYY-MM-DD - [Title].md` or project folder
   - Analysis/research → Project folder or vault root
   - Meeting prep → Person page or Daily page

4. **Create Draft**
   - Use templates from Reference/ if available
   - Include: Context, Draft Content, Questions/Decisions Needed
   - Mark as DRAFT

5. **Update Task Status**

   **Complete**:
   ```markdown
   - [x] [Task name] ✅ YYYY-MM-DD
     - Note:: Deliverable → [[path/to/deliverable]]
   ```

   **Review Needed**:
   ```markdown
   - [ ] REVIEW: [Task name]
     - Status:: **Draft ready for review** → [[path/to/deliverable]]
     - Note:: [What's ready, what questions remain]
   ```

   **Blocked**:
   ```markdown
   - [ ] BLOCKED: [Task name]
     - Status:: **[Specific blocker]** - [What's needed to continue]
     - Note:: [Context, what was attempted]
   ```

   **Waiting**:
   ```markdown
   - [ ] WAITING: [Task name]
     - Status:: **Waiting for [person/event]** - Expected [date]
     - Note:: [What was sent/done, what we're waiting for]
   ```

6. **Report Results**
   - List created deliverables with file paths
   - Report task status (Complete/Review/Blocked/Waiting)
   - Highlight questions or decisions needed
   - State clear next steps

**When to Use**:
- After `/prioritize-tasks` identifies high-priority tasks
- When you want to delegate task execution to AI
- For tasks requiring context gathering from multiple sources
- When you want deliverables created autonomously

**Examples**:

**Email Draft**:
```
/execute-task Draft email to Sarah about Q review meeting
→ Searches vault, emails, person page
→ Creates Drafts/2025-10-26 - Sarah Johnson - Q Review.md
→ Marks task as "REVIEW: Draft ready for review"
```

**Meeting Prep**:
```
/execute-task Prepare agenda for 1:1 with Mike
→ Reads People/mike.md, recent meetings, emails
→ Updates "Meeting Agenda" section in person page
→ Marks task as complete
```

**Analysis**:
```
/execute-task Analyze project X resource needs
→ Searches project files, emails, documents
→ Creates Drafts/2025-10-26 - Staffing Analysis - Project X.md
→ Marks task as "REVIEW: Analysis complete, need validation"
```

**Time saved**: 15-30 minutes per task (context gathering + draft creation)

---

### Check Calendar Workflow

**Workflow Name**: "Check Calendar Workflow"
**Slash Command**: `/check-calendar`

**Trigger**: When you explicitly call `/check-calendar` or say "check calendar"

**IMPORTANT**: **Always run this workflow using the dedicated `meeting-prep` agent.**

**Agent**: Use Task tool with `meeting-prep` subagent_type

**Sequence** (executed by meeting-prep agent):

1. **Get Today's Events**:
   - **MCP mode**: Use MS Graph calendar tools to list today's events
   - **File mode**: Read today's Daily note for scheduled meetings

2. **Skip Events**: Ignore all-day events, "Free" time, "Lunch", "Break", "Out of office"

3. **Process Each Event**:
   - **For 1:1 Meetings** (2 attendees):
     - Identify the other person
     - Check if person page exists in `People/` folder
     - If doesn't exist: Create person page with basic info
     - Prepare agenda:
       - Check person page for existing "Meeting Agenda" section
       - If exists: Review and update with recent topics
       - If doesn't exist: Create new agenda starting with "Go Through TODOs"
     - Write agenda to "## Meeting Agendas for Today" section in Daily page

   - **For Group Meetings** (3+ attendees):
     - Check event description for relevant links
     - Summarize meeting context
     - Write summary to "## Meeting Agendas for Today" section in Daily page

4. **Update Daily Page**: Create or update `Daily/YYYY-MM-DD.md`
   - If "## Meeting Agendas for Today" section exists: Replace it
   - If doesn't exist: Create it
   - Format each event with time, attendees, and agenda

5. **Output**: Point to the Daily page file location

**Purpose**: Prepare for all meetings in one go, create single source of truth for meeting agendas.

**Time saved**: ~3-5 minutes per meeting × average 3-4 meetings/day = 10-20 minutes/day

---

### Meeting Update Workflow

**Workflow Name**: "Meeting Update Workflow"
**Slash Command**: `/update-meetings [date]` (optional date parameter)

**Usage**:
- `/update-meetings` - Process today's meetings
- `/update-meetings yesterday` - Process yesterday's meetings
- `/update-meetings 2025-10-22` - Process meetings from specific date

**Trigger phrases** - When you say any of these:
- "just had meeting with [person]"
- "meeting with [person] done"
- "update agenda for [person]"

**Automatic actions**:

1. Identify the person (username format: first initial + last name, e.g., jsmith, schen)
2. Read `People/[username].md` file
3. Find today's meeting notes (from person page or Daily/ note)
4. **Extract and Process TODOs**:
   - Identify action items from meeting notes
   - Check if TODO already exists in Tasks/Next.md
   - If TODO doesn't exist:
     - Write task to Tasks/Next.md
     - Use standard task metadata format
     - Source: "Meeting - [Person Name] 1:1 (YYYY-MM-DD)"
5. Update the "Meeting Agenda" section in `People/[username].md` for next meeting
   - Remove/update completed items from current agenda
   - Add new action items from today's meeting
   - Keep pending items that weren't discussed
6. **Update Daily Page**: Mark meeting as "[COMPLETED]" in Daily note
7. Confirm what was updated

**Expected outcome**: Person page updated with next meeting agenda, tasks added to Next.md, Daily page marked complete

**Time saved**: ~2-3 minutes per meeting × 4-5 meetings/week = 10-15 minutes/week

---

### Task Archival Workflow

**Workflow Name**: "Task Archival Workflow"
**Slash Command**: `/archive-tasks`

**Trigger**: When you explicitly call `/archive-tasks`

**Purpose**: Move completed tasks from Tasks/Next.md to Archive/Tasks/Next.md to keep the active task list focused.

**Sequence**:

1. **Read Tasks/Next.md** and identify all completed tasks (marked [x])
2. **Count and report**: "Found X completed tasks ready to archive"
3. **Read or create Archive/Tasks/Next.md**
4. **Move completed tasks** to archive:
   - Preserve @office/@home context structure
   - Add at top (newest first by completion date)
   - Keep full metadata
   - Extract completion date from ✅ YYYY-MM-DD marker
5. **Remove from Next.md** - Delete archived tasks from active list
6. **Update archive metadata** - Update "Last archived" date and total count
7. **Report summary**: X tasks archived, archive location, Next.md cleaned up

**When to use**:
- After significant work sessions
- When completed tasks accumulate (10+ suggested threshold)
- Before starting new work cycles

**Time saved**: ~2-3 minutes per cleanup session vs manual cut/paste

---

## File-Based Inbox System

### How It Works

The vault includes an `Inbox/` folder with subfolders for different types of inputs. This allows the system to work **without any external integrations**.

### Inbox Structure

```
Inbox/
├── emails/           # Email-like messages
├── meetings/         # Meeting notes awaiting processing
├── tasks/           # Miscellaneous tasks
└── other/           # Other items
```

### Email Inbox Format

Create files in `Inbox/emails/` with this structure:

```markdown
---
from: sender@example.com
subject: Email subject line
date: 2025-10-26
---

# Email Subject

**From**: Sender Name <sender@example.com>
**Date**: 2025-10-26 09:30
**To**: you@example.com

Email body content goes here.

Action items or questions that need response.
```

### Meeting Notes Format

Create files in `Inbox/meetings/` with this structure:

```markdown
---
date: 2025-10-26
attendees: [John Smith, Sarah Chen]
---

# Meeting: Q1 Planning Review

**Date**: 2025-10-26 10:00-11:00
**Attendees**: John Smith, Sarah Chen, Alex Rivera

## Agenda
1. Review Q1 goals
2. Discuss resource allocation
3. Timeline planning

## Notes
- Discussed budget approval process
- Need to finalize team assignments by Friday

## Action Items
- [ ] John: Draft Q1 budget proposal (Due: Friday)
- [ ] Sarah: Schedule team kickoff meeting
- [ ] Alex: Review technical requirements document
```

### Task Inbox Format

Create files in `Inbox/tasks/` with this structure:

```markdown
---
created: 2025-10-26
priority: high
---

# Review proposal from client

**Context**: Client sent updated proposal document for Q1 project

**Action needed**: Review and provide feedback by end of week

**Related**: [[People/jsmith]] - John Smith is the client contact
```

### Processing Workflow

1. **Add items** to appropriate inbox folder as markdown files
2. **Run `/scan-inboxes`** to process all inboxes
3. **Scanner agents**:
   - Read each file
   - Extract actionable tasks
   - Write to Tasks/Next.md
   - Move processed files to respective /processed/ subfolders
4. **Review** scan report in Daily note

---

## Optional: MCP Integration

### What is MCP?

MCP (Model Context Protocol) allows Claude Code to connect to external services like:
- Microsoft 365 (Calendar, Email, Teams, OneDrive, SharePoint)
- Atlassian (Confluence, Jira)
- macOS Reminders

### Why Add MCP?

**File-based mode is fully functional**, but MCP adds:
- Live calendar integration (no manual Daily note updating)
- Automatic email scanning (no manual file creation)
- Direct Reminders app integration
- Confluence/Jira task reading
- Real-time data instead of manual file updates

### How to Add MCP

See README.md for detailed MCP setup instructions.

**Key point**: All agents work in both modes. They try MCP first, fall back to files automatically.

---

## Tips for Success

### Start Simple

1. Use file-based inboxes initially
2. Learn the daily workflow
3. Add MCP integrations gradually
4. Customize to your needs

### Daily Habits

- Morning: `/scan-inboxes` → `/prepare-tasks` → `/prioritize-tasks`
- Before meetings: `/check-calendar`
- After meetings: `/update-meetings`
- End of day: Review Daily note, check off completed tasks

### Folder Organization

- Keep Inbox/ clean (process regularly)
- Archive completed tasks weekly
- Review person pages before 1:1s
- Move completed projects to Archive/

### Energy Management

- High energy tasks (morning): Strategic work, complex problems
- Medium energy tasks (mid-day): Meetings, collaboration
- Low energy tasks (afternoon): Email, admin, routine items

---

## Customization

### Adding New Contexts

Edit `Tasks/Next.md` to add contexts like:
- `@errands` - Things to do while out
- `@phone` - Phone calls to make
- `@waiting` - Waiting for others

### Creating Templates

Add templates to `Templates/` folder for:
- Project structures
- Person pages
- Meeting notes
- Decision documents

### Adapting Workflows

All workflows are documented in this file. Modify them to match your:
- Work style
- Team structure
- Industry needs
- Personal preferences

---

## Troubleshooting

### Agents Not Finding Files

- Check file paths are absolute, not relative
- Verify folder structure matches documentation
- Look at agent logs in Daily notes

### Tasks Not Being Extracted

- Check task format matches metadata requirements
- Review scanner agent rules in `.claude/agents/`
- Ensure files are in correct inbox folders

### MCP Tools Not Working

- Agents automatically fall back to file mode
- Check MCP server configuration in Claude settings
- Verify authentication/permissions

---

## Getting Help

### Documentation Hierarchy

1. **This file (CLAUDE.md)** - Complete system guide
2. **README.md** - Quick start and setup
3. **Agent files** (`.claude/agents/`) - Specific agent behaviors
4. **Command files** (`.claude/commands/`) - Slash command prompts

### Learning Path

1. Read README.md (5 minutes)
2. Try file-based inbox system (1 day)
3. Run daily workflow for 1 week
4. Add MCP integrations (optional)
5. Customize to your needs

---

*This system is designed to grow with you. Start simple, add complexity as needed.*
