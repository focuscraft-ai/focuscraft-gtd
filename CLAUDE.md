# Obsidian Vault Overview for Claude AI

## Quick Reference

### Slash Commands
- **`/check-calendar`** → [Check Calendar Workflow](#check-calendar-workflow) - Prepare today's meeting agendas (uses meeting-prep agent)
- **`/update-meetings [date]`** → [Meeting Update Workflow](#meeting-update-workflow) - Update meeting agendas (optional: yesterday, YYYY-MM-DD)
- **`/plan-week`** → [Weekly Planning Workflow](#weekly-planning-workflow) - Create weekly plan from today through Sunday (uses weekly-planner agent)
- **`/next-item [low|mid|high]`** → [Next Item Workflow](#next-item-workflow) - Get single highest-priority task at chosen energy level (default: low)
- **`/execute-task [task]`** → Execute task from Next.md autonomously - gather context, create deliverables, update status
- **`/export-session`** → Export conversation history to Sessions/ folder before compacting
- **`/save-session-memory`** → Capture and organize session insights into memory files (CLAUDE.md, person pages, Reference/)
- **`/archive-tasks`** → [Task Archival Workflow](#task-archival-workflow) - Move completed tasks from Next.md to archive
- **`/improvement`** → [Improvement Documentation Workflow](#improvement-documentation-workflow) - Document GTD system improvements with consistent format

### Common Workflows

**Quick Automation Commands:**
- **Morning automation**: Say "good morning" → [Good Morning Workflow](#good-morning-workflow) - Runs essential morning prep (scan inboxes + check calendar) in one sequence
- **Weekly planning**: `/plan-week` → [Weekly Planning Workflow](#weekly-planning-workflow) - Plan remaining days of current week (on-demand)
- **Next item**: `/next-item [low|mid|high]` → [Next Item Workflow](#next-item-workflow) - Get single highest-priority task at chosen energy level
- **Create task**: Say "create task" → [Quick Task Creation](#quick-task-creation) - Fast task creation with minimal questions
- **List tasks**: Say "list tasks" → [Task List Command](#task-list-command) - Show all #agent reminders categorized by control status

**GTD Methodology:**
- **Full GTD process**: [GTD Daily Workflow](#gtd-daily-workflow) - Complete 4-phase methodology (Collect → Clarify → Organize → Execute)
  - Phase 1: `/scan-inboxes` - Collect from all sources
  - Phase 2: `/prepare-tasks` - Clarify what needs doing
  - Phase 3: `/prioritize-tasks` - Organize by priority
  - Phase 4: Execute using `/next-item` or manual selection
  - **Note**: "Good morning" automates Phase 1 (Collect) and calendar prep

**Project & Meeting Workflows:**
- **New project**: Reminder with #project tag → [Standard Project Workflow](#standard-project-workflow) - Create project structure
- **After meeting**: Say "meeting with [person] done" → [Meeting Update Workflow](#meeting-update-workflow) - Auto-update next agenda
- **Archive projects**: Say "archive projects" → [Project Archival Workflow](#project-archival-workflow) - Archive completed projects and preserve deliverables
- **Archive tasks**: Say `/archive-tasks` → [Task Archival Workflow](#task-archival-workflow) - Move completed tasks to archive
- **Evaluate proposal**: After `/check-calendar`, use skill → [Career Evaluation Workflow](#career-evaluation-workflow) - Evaluate promotion/hiring proposals

**System Maintenance:**
- **Document improvement**: Say `/improvement` → [Improvement Documentation Workflow](#improvement-documentation-workflow) - Capture system improvements with standard format

### Key File Locations
- **Person pages**: `People/[username].md` - Meeting agendas and context for individuals
- **Project files**: `Projects/[Project Name]/` - Each project has dedicated folder
- **Project tags**: `Projects/PROJECT-TAGS.md` - Master list of all project tags
- **Daily notes**: `Daily/YYYY-MM-DD.md` - Daily journal with meeting agendas (see `Daily/CLAUDE.md` for Daily file update standards)
- **Weekly plans**: `Weekly/YYYY-W##.md` - Weekly plans from today through Sunday with priorities and focus
- **Drafts**: `Drafts/YYYY-MM-DD - [Title].md` - Work-in-progress deliverables (emails, documents)
- **Projects index**: `Projects/Projects.md` - Central list of all active projects
- **GTD system docs**: `Reference/Concepts/GTD/` - System architecture, improvements, and future plans

### Important Rules
- **Person pages** go in `People/` folder (check `People/CLAUDE.md` for special cases)
- **All deliverables** start in `Drafts/` folder with date prefix
- **Projects** use #project tag in reminders, short tasks use #agent tag only
- **Meeting agendas**: Default = Operational Focus (2 weeks), unless "Q" or "FY plan" in title
- **Prioritize recent**: Last 2-3 meetings > old agenda items when preparing agendas

### Monthly Recurring Tasks
- **Time tracking review** - Flag project work in OH/EDU/MNG tickets (see `Maintenance/`)
- **Documentation audit** - Prevent documentation drift and duplication creep (see `Maintenance/`)
- **GTD system review** - Use `gtd-system` skill to review workflows, analyze improvements, suggest optimizations (see `Reference/Concepts/GTD/`)

### Project Task Integration
- **All project tasks** must appear in `Tasks/Next.md` with project tag for visibility
- **Project tags** use snake_case format (e.g., #focuscraft_ai, #gasper_hyi)
- **Master tag list**: See `Projects/PROJECT-TAGS.md` for all active project tags
- **Tag placement**: Inline in task title (e.g., "Task description #project_tag #other_tags")
- **Purpose**: Single source of truth (Next.md) with project filtering capability
- **Search**: Use Grep or Obsidian search to find all tasks for a project by tag

---

## Core Principle

**CLAUDE.md serves as a shared knowledge base for all Claude sessions and subagents.** All workflows, processes, and work-in-progress states must be documented clearly enough for any agent to understand and continue the work. Everything saved here should be accessible to future sessions - agents should know the workflows and the current state of any in-progress work.

## Information Architecture

The GTD system follows a **single source of truth principle** with clear rules for what information lives where.

**Quick Reference**:
- **Next.md** = All actionable tasks (single source of truth)
- **macOS Reminders** = Notifications only (not working list)
- **Person Pages** = Display agenda items (don't store them)
- **Project Files** = Project context (tasks in Next.md)
- **Daily Pages** = Journal + reports (reference tasks, don't duplicate)

**For complete architecture**: See `Reference/Concepts/GTD/Architecture/Information Architecture.md`

**For verification workflows**: See `Reference/Concepts/GTD/Architecture/Data Quality Verification Workflows.md`

## Slash Commands

Custom slash commands are defined in `.claude/commands/` directory. Each command is a markdown file that references workflows documented in CLAUDE.md.

**How Slash Commands Work**:
- Slash command files contain prompts that execute workflows
- Commands reference workflows by name (e.g., "Meeting Update Workflow")
- All workflow logic stays in CLAUDE.md (single source of truth)
- Slash commands are just convenient triggers

**Available Commands**:
- `/check-calendar` - Executes "Check Calendar Workflow" to prepare agendas for today's upcoming meetings
- `/update-meetings [date]` - Executes "Meeting Update Workflow" for meetings on specified date (today, yesterday, or YYYY-MM-DD)
- `/execute-task [task]` - Executes task from Next.md autonomously using execute-task agent
- `/export-session` - Exports conversation history to Sessions/ folder
- `/save-session-memory` - Captures session insights and saves to memory files (session-memory agent)
- `/archive-tasks` - Executes "Task Archival Workflow" to move completed tasks to archive

**Creating New Slash Commands**:
1. Create `.md` file in `.claude/commands/` (e.g., `new-command.md`)
2. Add prompt that references a workflow name in CLAUDE.md:
   ```markdown
   Execute the "[Workflow Name]" as defined in CLAUDE.md.
   ```
3. Document the slash command in the workflow's section in CLAUDE.md

**Important**: Never duplicate workflow logic in slash commands. Always reference CLAUDE.md workflows by name.

**Standards**: See `Reference/Concepts/GTD/Architecture/Agent and Command Creation Standards.md` for complete DRY principles and templates.

### How Slash Commands Invoke Agents

**IMPORTANT**: When a slash command references an agent:
1. The command expands to show a prompt/description (what you're reading)
2. **YOU must invoke the agent** using the Task tool immediately
3. **Do NOT wait** for automatic execution - commands don't auto-invoke agents
4. **Pattern**: Command says "using the [agent-name] agent" or "invoke the [agent-name] agent" → Use Task tool with that subagent_type NOW

**Recognition Pattern**:
- Look for: "**ACTION REQUIRED**: Use the Task tool to invoke the [agent-name] agent immediately"
- This is your signal to invoke the agent, not wait

**Example Flow**:
```
User types: /scan-reminders
Command expands to: "ACTION REQUIRED: Use the Task tool to invoke the reminders-scanner agent..."
Your action: Immediately use Task tool with subagent_type="reminders-scanner"
DON'T: Wait, assume it's running, or ask if you should invoke
DO: Invoke the agent right away
```

**Why This Matters**:
- Slash commands are just prompts - they don't execute anything themselves
- Agent invocation requires explicit Tool use by Claude
- Without immediate invocation, workflow stalls and user waits
- This pattern was added 2025-10-29 to prevent confusion and delays

**For Command Authors**:
When creating slash commands that invoke agents, always include:
```markdown
**ACTION REQUIRED**: Use the Task tool to invoke the [agent-name] agent immediately.

Do NOT wait for automatic execution. Invoke the agent now.

**Agent**: [agent-name]
**Subagent type**: [subagent-type]
**Purpose**: [brief description]
```

This makes Claude's required action crystal clear.

## Specialized Agents

Claude Code has access to specialized agents that handle specific types of tasks. These agents preserve main session context by running workflows independently.

### Available Agents

**meeting-prep** - Meeting preparation specialist
- **Purpose**: Calendar checking and meeting agenda preparation
- **Used by**: Check Calendar Workflow (`/check-calendar`)
- **Capabilities**:
  - Calendar event processing and filtering
  - Person page creation and management
  - Confluence 1:1 page reading
  - Email context gathering (MS Graph)
  - Agenda preparation following Meeting Agenda Preparation Rules
  - Daily page updates with meeting agendas
- **When to use**: Any time meeting agendas need to be prepared
- **Agent file**: `.claude/agents/meeting-prep.md`

### Creating New Specialized Agents

When a workflow becomes:
- Highly repetitive
- Well-defined with clear inputs/outputs
- Resource-intensive (many tool calls)
- Better run independently to preserve main context

Consider creating a dedicated agent:
1. Create `.md` file in `.claude/agents/` directory
2. Define agent name, description, model, and color
3. Document agent's responsibilities and capabilities
4. Update workflows in CLAUDE.md to reference the agent
5. Test agent with the workflow

**Standards**: See `Reference/Concepts/GTD/Architecture/Agent and Command Creation Standards.md` for complete agent creation patterns and DRY principles.

## Workflow Templates

Workflows in this document follow common patterns. Understanding these patterns helps you execute workflows consistently.

### Standard Workflow Structure

All workflows include these elements:
- **Workflow Name**: Unique identifier for reference
- **Trigger**: How the workflow is invoked (slash command, phrase, or intent)
- **Purpose**: What the workflow achieves and when to use it
- **Sequence**: Numbered steps to execute

### Agent-Based Workflow Pattern

Workflows that use specialized agents follow this pattern:
1. **IMPORTANT**: Always invoke using Task tool with specified subagent_type
2. **Don't wait** for automatic execution - commands don't auto-invoke agents
3. **Agent executes** the sequence independently
4. **Results returned** to main session when complete

When you see "**Always run this workflow using the dedicated [agent-name] agent**":
- Immediately use Task tool with that subagent_type
- Don't announce each step - let agent work
- Present results when complete

### Slash Command Pattern

Slash commands are triggers, not executors:
- Command file contains prompt referencing workflow by name
- All workflow logic stays in CLAUDE.md (single source of truth)
- Commands never duplicate workflow steps
- See "How Slash Commands Invoke Agents" section for agent invocation pattern

## Skills

Skills are interactive capabilities that guide you through complex processes requiring back-and-forth conversation and decision-making.

### Available Skills

**career-evaluation** - Promotion and hiring proposal evaluation
- **Purpose**: Evaluate proposals against Salary Policy Handbook and grade expectations
- **Used by**: Career Evaluation Workflow (after `/check-calendar` detects promotion meetings)
- **Capabilities**: Read proposals, analyze against policy, generate 1-page evaluation reports
- **When to use**: Promotion or hiring proposal evaluation needed
- **Skill file**: `.claude/skills/career-evaluation/skill.md`

**feedback-writer** - Performance feedback specialist
- **Purpose**: Write high-quality performance feedback with guided conversation
- **Used for**: Grill feedback (TL/GL/DH), HYI colleague feedback, promotion feedback
- **Capabilities**:
  - Context gathering (asks main session to read files, emails, Confluence)
  - Targeted question generation based on gaps
  - Tone matching from previous feedback examples
  - Interactive draft refinement (one suggestion at a time)
  - Saves draft and marks task complete
- **When to use**: Any time performance feedback needs to be written
- **Invocation**: `Skill: feedback-writer [person] [type]`
- **Example**: `Skill: feedback-writer username grill`
- **Skill file**: `.claude/skills/feedback-writer/skill.md`

**gtd-system** - GTD system improvement and optimization
- **Purpose**: Maintain, improve, and evolve the GTD task management system
- **Used for**: System improvements, workflow optimization, new feature design, FocusCraft product sync
- **Capabilities**:
  - Track system improvements and analyze impact
  - Review workflows and suggest optimizations
  - Design new features interactively
  - Monitor system state (Reference/Concepts/GTD/) and future plans (@claude tasks)
  - Identify improvements for FocusCraft product
  - Help with sanitization and sync decisions
- **When to use**: Monthly reviews, when noticing friction, before major changes, FocusCraft updates
- **Invocation**: `Skill: gtd-system [command]`
- **Common commands**: `review workflows`, `design [feature]`, `suggest optimizations`, `sync to focuscraft`
- **Knowledge base**: `Reference/Concepts/GTD/` (Architecture, Improvements, Future)
- **Skill file**: `.claude/skills/gtd-system/skill.md`

### Skills vs Agents

**Use Skill when**:
- Requires back-and-forth conversation
- Iterative decision-making needed
- User guidance throughout process
- Maintains conversational state

**Use Agent when**:
- Autonomous execution preferred
- Clear inputs → outputs workflow
- Many file/tool operations
- Preserves main session context

## you Persona

When writing emails or documents for you, follow this communication style:

### Overall Style
- **Tone**: Professional, direct, collaborative. Warm but efficient.
- **Language**: Slovenian for internal (default), English for external/international
- **Core traits**: Pragmatic, context-rich, transparent, structured thinker, analytical

### Email Structure
**Opening**: "Živjo" (Slovenian), "Hej", "Dear all," (English)
**Body**: Direct answer first, then context in bullets (•) or numbered lists
**Closing**: "Lp, you" (Slovenian), "Regards, you" (English)

### Communication Patterns
**DO:**
- Lead with direct answer or acknowledgment
- Use bullet points (•) for complex ideas
- Provide reasoning and context
- Ask clarifying questions when needed
- Be transparent about concerns ("Me pa skrbi, da...")
- Use collaborative language ("se strinjam", "lahko razumem")
- Reference specific numbers, documents, facts
- Think through implications and alternatives

**DON'T:**
- Use emojis (maintain professional tone)
- Be overly formal or use corporate jargon
- Apologize unnecessarily
- Give vague answers
- Use excessive punctuation (!!!, ???)

### Tone by Recipient
- **Leadership**: More structured, strategic framing, still direct
- **Peers (GLs, DHs)**: Natural, collaborative, problem-solving mode
- **Direct reports**: Supportive, clear, provides rationale
- **External**: Professional but warm, more concise

### Common Phrases
- "Glede na..." (given that), "Se pravi..." (meaning), "Mislim, da..." (I think)
- "Me pa skrbi, da..." (I'm concerned), "Smiselno je..." (it makes sense)
- "Se strinjam" (I agree), "Lahko razumem" (I can understand)
- "Predlagam..." (I propose), "Potrebno je..." (it's necessary)

## Vault Structure

This is you Dezman's Obsidian vault at `[vault path]`. Comprehensive knowledge base for work management, project planning, meetings, and personal development.

**For complete directory details**: See [[Reference/Concepts/Vault Structure]]

### Essential File Locations

**Active Work**:
- `Tasks/Next.md` - All actionable tasks with metadata
- `Daily/YYYY-MM-DD.md` - Daily journal with meeting agendas
- `Projects/Projects.md` - Central project index
- `Notes.md` - Running notes and thoughts

**Deliverables**:
- `Drafts/` - Work-in-progress deliverables (emails, documents, invitations)
- `Projects/[Project Name]/` - Project-specific deliverables and files

**Knowledge Base**:
- `Reference/Concepts/` - Frameworks, workflows, GTD system docs
- `Reference/Meetings/` - Archived meeting notes (always check with Meetings/)
- `Reference/People/` - Performance frameworks, promotion examples
- `Reference/Business/` - Strategy, domains, planning

**People & Meetings**:
- `People/username.md` - Person pages with meeting agendas
- `Meetings/` - Active 2025 meeting notes (temporary before Confluence)

**Archives**:
- `Archive/` - Historical content no longer actively referenced

### Key Organization Rules

- **Vault root**: Only 8-10 active working files
- **Deliverables**: Start in Drafts/, move to project folder if project created
- **Reference/**: Permanent, reusable knowledge (check first for "how we did X")
- **Meeting notes**: Check BOTH Meetings/ (active) AND Reference/Meetings/ (archived)
- **Person pages**: Format is username.md (e.g., username.md, username.md)

### Search Strategy Quick Reference

| Looking for | Check here first |
|-------------|------------------|
| Recent work | Daily/, Notes.md |
| Project status | Projects/Projects.md, project folders |
| Frameworks/processes | Reference/Concepts/ |
| Meeting context | Meetings/ AND Reference/Meetings/ |
| Past examples | Reference/People/, Reference/Business/ |
| Objectives | objectives.md, FY planning files |
- all projects I am working on are in the @Projects/ folder. @Projects/Projects.md is the starting file where I have a summary of all projects I am working on. Whenever I ask you something about projects you go and look inside this folder.
- whenever Tasks or Information is updated on project pages, please update Log. You can see the example of how this is done in Everyday AI.md
- create a dedicated folder for each project inside Projects/ folder to keep related files organized
- within each project folder, use descriptive file names without project prefix since the folder provides context

## Standard Project Workflow

**IMPORTANT**: Only use this workflow for tasks that have **#project tag** in the reminder title.

If a task has **#agent tag only** (no #project tag), it's a small item to solve right away - do NOT create a full project structure. Work on it directly.

**For tasks with #project tag:**
1. **Check task in reminders** - Find outstanding tasks/reminders that need to become projects
2. **Create project** - Set up project file with structure (Tasks, Log, Information, Confluence Links)
3. **Create project tag** - Generate snake_case tag from project name (see `Projects/PROJECT-TAGS.md`)
   - Add tag to PROJECT-TAGS.md master list
   - Add tag to all related tasks in Tasks/Next.md
   - Format: #project_name (e.g., #focuscraft_ai, #gasper_hyi)
4. **Gather information** - Research from multiple sources:
   - Vault content (meeting notes, previous work)
   - Emails (recent communications, context)
   - Confluence (company pages, documentation)
5. **Prepare drafts** - Create deliverables based on task description and gathered info

**Note**: A simpler workflow for small #agent tasks may be developed in the future.

### Putting Work On Hold

When working on a task needs to be paused to start something else, use this decision tree:

```
Is this a #project task?
├─ YES → Save in Projects/[Project Name]/ folder
│         - Update Log section with current status
│         - Add "ON HOLD" status and next steps
│
└─ NO (it's a #agent task)
    │
    ├─ Does it create a deliverable? (email, document, invitation, etc.)
    │  │
    │  YES → Save in Drafts/ folder
    │         - File naming: YYYY-MM-DD - [Title].md
    │         - Include: Context, Questions/Decisions Needed, Draft content, Next Steps
    │         - Tags: #draft, #agent, type tag (e.g., #email, #meeting-invitation)
    │
    └─ NO (research, analysis, administrative work)
       │
       └─ Save in vault root
          - File naming: [Task description].md (e.g., "Alex - time tracking categories.md")
          - Include: Work Done So Far, Context Analysis, Next Steps
          - Tags: #agent, relevant person/project tags
          - Status: in-progress
```

**Quick Reference Table:**

| Task Type | Location | File Naming | Required Sections |
|-----------|----------|-------------|-------------------|
| **#project task** | `Projects/[Project Name]/` | Descriptive name (folder provides context) | Log (with status), Information, Tasks |
| **#agent deliverable** | `Drafts/` | `YYYY-MM-DD - [Title].md` | Context, Questions/Decisions Needed, Draft content, Next Steps |
| **#agent research/analysis** | Vault root | `[Task description].md` | Work Done So Far, Context Analysis, Next Steps |

**Key Rule**: ALL deliverables → Drafts/. Non-deliverable #agent work → Vault root. Projects → Projects/ folder.

### Task Contexts in Next.md

Tasks in `Tasks/Next.md` are organized by context to indicate where and when they can be done:

- **`@office`** - Work tasks that require office resources, work computer, or collaboration
- **`@home`** - Personal tasks that can be done at home
- **@claude** - Meta-tasks about improving Claude Code workflows, vault structure, and automation

**`@claude` Context**:
This special context is for tasks that improve the system itself:
- Enhancing agents and workflows
- Fixing bugs in automation
- Updating CLAUDE.md documentation
- Vault structure improvements
- Adding new features to the GTD system

Tasks in `@claude` context are typically worked on during:
- System improvements sessions
- When workflows need debugging
- When new automation ideas emerge
- During vault maintenance and optimization

**Example @claude tasks**:
- Enhance task-preparer to archive completed tasks
- Add time blocking feature to prioritizer agent
- Create new slash command for weekly review
- Document new workflow in CLAUDE.md

### Remote Projects

**Remote projects** are development/code projects where code lives in a separate repository outside the vault, while project tracking happens in the vault using standard GTD structure.

**When to use remote projects:**
- Development projects with their own repositories
- Technical tools requiring version control
- Projects with complex dependencies (node_modules, build artifacts)
- Projects you might share publicly without exposing vault

**Structure:**
- **Vault**: Project file in `Projects/[Name]/` acts as tracker with repository link
- **Repository**: Independent git repo outside vault with code and CLAUDE.md
- **Tasks**: Managed normally in Next.md with project tag
- **Tag notation**: `PROJECT-TAGS.md` includes "(remote: /path/to/repo)" to indicate external repository

**Benefits:**
- Clean separation (vault = tracking, repo = code)
- No git submodule complexity
- Standard GTD workflows work unchanged
- Independent code versioning

**Examples**:
- [[Projects/Task Viewer/Task Viewer]] - Local task viewer application (first formal implementation)
- [[Projects/FocusCraft AI/FocusCraft AI]] - Commercial GTD product (public GitHub repo)

**Full documentation**: [[Reference/Concepts/GTD/Architecture/Remote Project Pattern]]

## Project File Structure
Each project should include these sections:
- **Tasks** - Organized by category with checkboxes and completion dates
- **Log** - Chronological updates and decisions
- **Information** - Project context, requirements, and key details
- **Confluence Links** - Relevant company resources for data gathering and reference
  - I can either convert these to markdown documentation or extract data on-the-fly
  - Include page URLs with brief descriptions of their relevance

## Person Pages Workflow
Person pages are stored in the `People/` folder as `username.md` files to serve as linking hubs.

### When Creating or Updating a Person Page:

**IMPORTANT: Gather information first, THEN ask clarifying questions to improve first draft quality.**

**Step 1: Information Gathering**
1. **Search vault** for `[[username]]` links and mentions (Daily/, Projects/, all files)
2. **Search emails** using MS Graph tools (search by person's name/email) for recent communications
3. **Check Confluence** for profile and 1:1 meeting pages
4. **Identify patterns**: Recent topics, recurring issues, key projects

**Step 2: Ask Clarifying Questions** (after seeing what information exists)
Present what you found, then ask you:
1. **Relationship**: "What is your relationship with [person]? (direct report, peer, reports to them, external?)"
2. **Context**: "What context do you need this page for? (1:1 prep, project collaboration, feedback tracking?)"
3. **Key topics**: "From what I found, these topics came up: [list]. Which are most relevant to focus on?"
4. **Priority info**: "What information would be most useful to track about them going forward?"
5. **Clarifications**: Ask about any confusing or conflicting information found

**Step 3: Create/Update Page**
Use the recommended structure with information gathered and refined based on clarifying answers.

### When Queried About a Person:
1. **Read** `People/username.md` file
2. **Check People/CLAUDE.md** for any special cases or exceptions for this person
3. **Check structure** - flag if missing:
   - Confluence profile links
   - Role/department information
   - Context or relevant project links
4. **Search all vault files** for `[[username]]` links and mentions (not just Daily/ and Projects/)
5. **Check for meeting notes**:
   - Search `Meetings/` folder for recent notes
   - **Always also search `Reference/Meetings/`** for archived/strategic discussions
   - Pattern: Check BOTH locations before concluding no meeting notes exist
6. **Check Confluence** if links are provided in the person page (unless People/CLAUDE.md says otherwise)
7. **Search emails** using MS Graph tools for recent communications

### Special Cases for Meeting Notes:
See `People/CLAUDE.md` for detailed information about people with non-standard meeting note storage (e.g., people without Confluence 1:1 pages).

### Recommended Person Page Structure:
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
- [Confluence Profile](URL)
- [1-on-1 Notes](link if recurring)
- [OKR Page](link to Confluence OKR page if exists)

## HYIs
- [HYI YYYY-MM-DD](link) - Brief context
- [HYI Feedback YYYY](link) - Feedback collection page

## Related Pages
- [[Project]] - context
- [[Meeting YYYY-MM-DD]] - context

## Notes
[Key information, observations, etc.]
```

## Email Access
**Primary method**: Use MS Graph email tools (search_emails, list_emails, get_email_details)
- These tools access live email from Microsoft 365
- Can search by keywords, sender, subject, date range
- Can retrieve email bodies and full details

**Fallback method** (if MS Graph unavailable): Read from folders:
- `~/Documents/MailExports`
- `~/Library/CloudStorage/OneDrive-yourcompany.com/Emails`

## Historical Archives

**Old Task Management System:**
If searching for very old work information, projects, or meeting notes, check your historical archive folders:
- Location: Configure your archive path in vault settings
- Contains: Old task management files, historical meeting notes, and past projects
- Purpose: Historical reference only - current work is in this Obsidian vault

## Maintenance Tasks

**REMINDER**: At the start of each month (first Claude session), remind you to run recurring maintenance tasks.

### What Are Maintenance Tasks?
Maintenance tasks are recurring monitoring activities that:
- Are NOT projects (no deliverables, just monitoring)
- Produce reports/findings that need review
- Track patterns over time
- Are stored in `Maintenance/` folder

**Available Maintenance Tasks:**
1. **Time Tracking Review** - Review work tickets for misreported project work (monthly, first week)
2. **Documentation Audit** - Prevent documentation drift and duplication creep (monthly, first week)
3. **CLAUDE.md Audit** - Legacy audit task (replaced by Documentation Audit)

### How to Execute
When you mentions a maintenance task or it's time to run one:
1. Read detailed instructions from `Maintenance/CLAUDE.md` (automatically loaded when working in Maintenance/ folder)
2. Follow the workflow specified in the maintenance task file
3. Update History section in the specific task file with findings
4. Present summary to you

**Detailed Instructions**: See `Maintenance/CLAUDE.md` for complete workflows and procedures

## Important Lessons Learned

### Email Verification Accuracy
**Date**: 2025-10-01
**Context**: Verifying sent email to Benjamin about hiring proposal

**Issue**: When asked to verify a sent email using a subagent, I initially provided a summary/paraphrase instead of reading and reporting the actual exact content that was sent.

**Learning**: When verifying sent emails or any documents:
1. Always read the COMPLETE actual content, not just metadata or summaries
2. Report the EXACT text/content that appears in the document
3. Do not paraphrase or summarize unless explicitly asked
4. Be precise and accurate - the user needs to verify what was actually sent, not what should have been sent
5. If asked to verify again, recognize this means the first attempt was not accurate enough

**Application**: Use Read tool to get full content. Quote or present the actual text verbatim. Distinguish clearly between what was drafted vs. what was actually sent.

### Meeting Agenda Preparation - Prioritize Recent Topics
**Date**: 2025-10-07
**Context**: Preparing meeting agenda for username

**Issue**: When preparing meeting agendas from Confluence pages, I included old topics from the "Meeting Agenda" section that were not the most recent discussions.

**Learning**: Always prioritize recent meetings over old planned agenda items when preparing meeting agendas.

**Application**: See [Meeting Agenda Preparation Rules - Rule 1](#meeting-agenda-preparation-rules) for the complete implementation of this lesson.

### Task Ownership Clarity
**Date**: 2025-10-21
**Context**: Alex RT proposal investigation

**Issue**: Spent significant time investigating Alex's RT setup and time tracking proposal without first verifying who owned the task. Later discovered it was actually Blaž's responsibility, not you's.

**Learning**: Always verify task ownership before starting work on a task:
1. Who assigned this task? (Was it assigned to me directly?)
2. Who actually owns this work? (Am I the owner or just helping?)
3. What's my role? (Lead, collaborate, or support?)
4. Is this my responsibility or should it be delegated?

**Application**:
- When receiving task assignments, ask: "Who assigned this and am I the owner?"
- Before deep investigation, confirm: "Is this mine to solve?"
- If unclear ownership, check with you before significant time investment
- Distinguish between "investigate and solve" vs "provide input/help"

### Feedback Writing Process
**Date**: 2025-10-22
**Context**: Writing Sarah DH Grill feedback

**Issue**: Writing high-quality feedback efficiently requires structured approach. Ad-hoc writing can miss important context or not match organizational tone.

**Learning**: Structured feedback writing process works best:
1. **Gather context** - Read previous feedback examples, person pages, emails, Confluence notes
2. **Identify patterns** - What tone/structure does the organization use?
3. **Ask targeted questions** - Fill gaps with specific questions (not open-ended "tell me about them")
4. **Draft with structure** - Use proven templates and formats
5. **Iterate incrementally** - Refine one section at a time based on feedback

**Application**:
- The feedback-writer skill implements this process
- Always gather examples BEFORE drafting (don't write in a vacuum)
- Ask specific questions: "Can you give an example of when [person] showed [quality]?"
- Match organizational tone by reading previous feedback from same context
- Iterate on drafts with user, not trying to perfect first version

### Email Scanner Completeness
**Date**: 2025-10-23
**Context**: Email scanner only marking actionable emails as read

**Issue**: Initial email scanner implementation only marked actionable emails (those that created tasks) as read. Filtered/automated emails (RT, Confluence, etc.) were left unread, preventing true "Inbox Zero."

**Learning**: For inbox clearing to be complete, ALL emails must be marked as read:
1. **Filtered/automated emails** - Mark as read immediately when identified (no task needed)
2. **Actionable emails** - Mark as read after creating task
3. **FYI emails** - Mark as read even if no action taken
4. **Goal**: Total marked as read = Total scanned (complete inbox clearing)

**Application**:
- Email scanner now has two-phase marking: filtered emails (immediate) + processed emails (after task creation)
- Debug log tracks both categories separately to verify completeness
- Success criteria: "Total marked as read = Total scanned"
- This achieves true "Inbox Zero" where inbox is completely cleared

### Repository Safety - File Operations
**Date**: 2025-10-26
**Context**: FocusCraft AI product development - accidentally attempted to overwrite files

**Issue**: When working with product repositories and customer-facing files, attempted to use Write tool on existing files instead of Edit, which would have replaced entire file contents.

**Learning**: Critical safety rules for file operations:
1. **Always Read file first** before any modification attempt
2. **Use Edit tool** (with old_string/new_string) when updating existing files
3. **Use Write tool ONLY** for new files that don't exist yet
4. **Verify changes** with Read after Edit/Write to confirm correct update
5. **When unsure**, ask user before modifying any file
6. **Never assume** file contents - always read current state first

**Application**:
- Added to all file operation workflows
- Prevents data loss and accidental overwrites
- Especially critical for product repositories where mistakes could ship to customers
- Double-check before any git commit to product repositories

**Impact**: Prevents catastrophic data loss in customer-facing repositories.

## Meeting Agenda Preparation Rules

**IMPORTANT**: These rules apply to ALL meeting agenda creation.

### Rule 1: Prioritize Recent Discussions
When creating meeting agendas from Confluence 1:1 pages:
1. **Weight recent heavily** - Last 2-3 meeting entries are primary source
2. **Read level 1 links** - Check linked pages (OKR, TL Grill, etc.) for additional context
3. **Don't follow child links** - Only read direct links from the 1:1 page
4. **Recent over planned** - Recent discussions > old agenda items
5. **Verify relevance** - Confirm old agenda items are still active

### Rule 2: Meeting Scope Based on Trigger Words

**Default: Operational Focus (Bi-weekly meetings)**
- **Scope**: Current work, next 2 weeks, immediate follow-ups
- **Sources**: Recent Confluence meeting notes (last 2-3 entries), recent emails, active tasks
- **Topics**: Operational items, open issues, current projects, team updates
- **Time horizon**: Now + 2 weeks

**"Q" or "quarterly" trigger: Quarterly Review**
- **Scope**: Quarter performance, goals progress, strategic initiatives
- **Sources**: Recent meetings + OKR pages + FY planning docs + hiring plans
- **Topics**: Quarterly objectives, goal progress, resource planning, strategic initiatives
- **Time horizon**: Current quarter + next quarter planning

**"FY plan" or "annual" trigger: Annual Strategic Review**
- **Scope**: Full year strategy, long-term planning, organizational changes
- **Sources**: All of the above + FY planning documents + strategic initiatives + domain strategies
- **Topics**: Annual goals, department strategy, long-term resource planning, major initiatives
- **Time horizon**: Full fiscal year + next FY planning

### Rule 3: Default Behavior
Unless you explicitly says "Q" or "FY plan", ALWAYS use **Operational Focus** for agenda preparation.

## Task List Command

**When you says "list tasks":**
1. Search reminders with #agent tag using `mcp__task-agent__search_reminders`
2. Match tasks against existing projects:
   - Check Projects/Projects.md for active projects
   - Look for matching project folders in Projects/
   - Identify if task is already tracked in a project
3. Categorize tasks in report:
   - **Under Control**: Tasks that have corresponding projects or are tracked
   - **Not Under Control**: New tasks without projects or tracking
4. Number all tasks sequentially
5. Clearly mark which tasks are completed (so you knows which to mark done in Reminders app)
6. Show which tasks are due or overdue with dates
7. Use consistent format each time

**Report Format:**
```
## Tasks Under Control ✅
1. [Task name] - Project: [Project Name] - Status: [status]

## Tasks Not Under Control ⚠️
1. [Task name] - Due: [date if any] - Tags: [tags]

## Completed Tasks (Mark as done in Reminders)
1. [Task name] - Completed: [date]
```

**Note**: Claude cannot mark reminders as complete - only read and create them. you must mark completed tasks as done in macOS Reminders app manually.

## Task Creation Workflow (Canonical)

**This is the authoritative task creation specification. All workflows that create tasks reference this section.**

### When to Create macOS Reminder

**Only create macOS Reminder if BOTH conditions are true:**
1. Task has a **specific due date** (not "None")
2. Task is **time-sensitive** (needs notification)

**Examples of time-sensitive tasks:**
- Tasks with explicit deadlines
- Tasks mentioned in "by Friday", "end of month", etc.
- Tasks with urgency indicators

**Examples NOT time-sensitive (no reminder needed):**
- General backlog items
- Tasks with Due: "None"
- Tasks that just need tracking

### Duplicate Checking

**Only check Tasks/Next.md** for similar tasks:
- Search for similar description keywords
- If similar task found: Ask user whether to merge or create new
- Do NOT check Confluence, emails, or other sources

### Required Metadata Fields

These fields are **REQUIRED** when applicable:

**Person**:
- ALWAYS fill if task involves someone (meeting, discussion, review with person)
- Format: `[[People/username]]`
- Example: `Person:: [[People/username]]`

**Email**:
- ALWAYS fill if task came from email
- Use webLink from MS Graph API (not outlook:// protocol)
- Format: `Email:: <https://outlook.office.com/mail/...>`

**Project**:
- ALWAYS fill if task is project-related
- Use project tag format
- Format: `Project:: #project_name` (e.g., `#focuscraft_ai`)

### Source Format

Keep source format as-is from the workflow that creates the task:
- **Email**: `Email from [Sender Name]`
- **Meeting**: `Meeting - [Title/Person] (YYYY-MM-DD)`
- **Confluence**: `Confluence - [Page Title] (page link)`
- **Reminders**: `Reminders Inbox`
- **Manual**: `Manual entry (YYYY-MM-DD)`

Do NOT standardize further - preserve workflow-specific formats.

### Special Tags

**#waiting tag**:
- Add when task is **delegated** and waiting for another person to complete it
- Example: "Waiting for manager to approve budget proposal"
- Format: Add #waiting inline with other tags
- Used by Next Item Workflow to filter out tasks you can't work on yet
- Tasks with #waiting stay in Next.md as follow-up reminders but are excluded from prioritization

**#someday tag**:
- Add when task is an **idea for someday/maybe** (not actionable now)
- Example: "SOMEDAY: Create podcast about leadership lessons #someday"
- Format: Add "SOMEDAY:" prefix to task title + #someday tag inline
- Used by prioritization workflows to exclude from daily focus
- Tasks with #someday stay in Next.md for future consideration but are excluded from prioritization
- Move to active status by removing prefix and tag when ready to work on it

**#agenda tag**:
- Add when task is **agenda item** (need to discuss with person in meeting)
- Example: "Discuss TPS reorganization with Gregor"
- Format: Add #agenda inline with other tags
- Indicates task will be addressed in upcoming 1:1 meeting

**When to combine tags**:
- Task can use multiple special tags as appropriate
- Example: "Discuss promotion timeline with manager #waiting #agenda" (waiting for manager's availability + agenda item for next meeting)
- Note: #waiting and #someday are mutually exclusive (task is either blocked on someone OR deferred indefinitely)

### Task Creation Steps

**Step 1: Check for duplicates**
- Search Tasks/Next.md for similar task
- If found: Ask user (suggest merge vs create new)

**Step 2: Create reminder ID**
- Format: `#rem_YYYYMMDD_keyword`
- Date: Current date (YYYY-MM-DD)
- Keyword: 2-3 words from task description
- Example: `#rem_20251106_budget_review`

**Step 3: Determine metadata**
- **Person**: REQUIRED if task involves someone
- **Email**: REQUIRED if task from email
- **Project**: REQUIRED if task is project-related
- **Due**: YYYY-MM-DD or "None"
- **Duration**: 5min, 15min, 30min, 1hr, 2hr, 3hr+
- **Energy**: High/Medium/Low
- **Source**: Keep workflow-specific format
- **Note**: Context, rationale, next steps

**Step 4: Add special tags**
- #waiting: If delegated and blocked on person
- #someday: If idea for someday/maybe (not actionable now)
- #agenda: If discussion item for meeting
- Multiple: If task needs multiple tags (e.g., #waiting #agenda)

**Step 5: Determine context**
- @office: Work tasks (default)
- @home: Personal tasks
- @claude: Meta-tasks about system improvement

**Step 6: Write to Tasks/Next.md**
- Read current file contents first
- Add task under appropriate context section
- Use Edit tool to append task

**Step 7: Create macOS Reminder (conditional)**
- Only if: Task has due date AND is time-sensitive
- Use: `mcp__task-agent__create_reminder`
- **List name**: "Reminders" (NOT "Inbox" - Inbox is for unprocessed items only)
- Include: Task description, due date in ISO format

**Step 8: Update related pages**
- Person page: If agenda item, add to Meeting Agenda section
- Project page: If project task, link appropriately
- Daily page: Note task creation if significant

### Examples

**Example 1: Regular task**
```markdown
- [ ] Review FY26 budget proposal and provide feedback #rem_20251106_budget_review
  - Due: 2025-11-15
  - Duration: 1hr
  - Energy: High
  - Source: Email from Benjamin
  - Email: <https://outlook.office.com/mail/inbox/id/AAMk...>
  - Person: [[People/bocepek]]
  - Note: Benjamin needs feedback for Q1 planning. Focus on Services headcount allocation.
```

**Example 2: Task with #waiting (delegated)**
```markdown
- [ ] Get approval from manager for Q4 hiring plan #rem_20251106_igor_approval #waiting
  - Due: None
  - Duration: 5min (to follow up)
  - Energy: Low
  - Source: Meeting - GL Meeting (2025-11-05)
  - Person: [[People/igor]]
  - Note: Submitted hiring plan 2025-11-05. Waiting for manager's approval before proceeding with candidate interviews. Follow up if no response by Friday.
```

**Example 3: Task with #someday (idea for future)**
```markdown
- [ ] SOMEDAY: Create podcast about leadership lessons #rem_20251107_podcast #someday
  - Due: None
  - Duration: 3hr+
  - Energy: High
  - Source: Manual entry (2025-11-07)
  - Note: Idea from conversation with manager. Could be valuable for GL development, but not priority now. Revisit during quarterly review.
```

**Example 4: Task with #agenda (discussion item)**
```markdown
- [ ] Discuss TPS organizational structure options with Gregor #rem_20251106_tps_structure #agenda
  - Due: Before next 1:1
  - Duration: 30min
  - Energy: Medium
  - Source: Email from username
  - Email: <https://outlook.office.com/mail/inbox/id/AAMk...>
  - Person: [[People/username]]
  - Note: Gregor has ideas about TPS reporting structure changes. Add to next 1:1 agenda to discuss options and implications.
```

**Example 5: Task with both #waiting and #agenda**
```markdown
- [ ] Review promotion timeline with manager and get next steps #rem_20251106_promo_timeline #waiting #agenda
  - Due: None
  - Duration: 20min
  - Energy: Medium
  - Source: Meeting - Promotion Discussion (2025-11-04)
  - Person: [[People/igor]]
  - Note: Waiting for manager to review Grade 5 comparison matrix. Need to discuss timeline for remaining promotions this year. Add to next 1:1 agenda.
```

### Success Criteria

Task is properly created when:
- ✅ No duplicates in Tasks/Next.md
- ✅ Reminder ID is unique and properly formatted
- ✅ Person filled if task involves someone
- ✅ Email filled if from email source
- ✅ Project filled if project-related
- ✅ #waiting tag added if delegated and blocked
- ✅ #someday tag added if idea for future (not actionable now)
- ✅ #agenda tag added if discussion item
- ✅ Context (@office/@home/@claude) is appropriate
- ✅ macOS Reminder created only if due date + time-sensitive
- ✅ Related pages updated (person/project pages)

## Quick Task Creation

**Workflow Name**: "Quick Task Creation Workflow"
**Slash Command**: None (intent-based detection)

**Trigger phrases** - When you says any of these:
- "create task"
- "add task"
- "new task"
- "I want to create a task"
- "add this to my tasks"

**Reference**: This workflow uses the **Task Creation Workflow (Canonical)** defined above.

**Sequence**:
1. **Detect intent** - Recognize user wants to create a task
2. **Ask questions** - Use AskUserQuestion tool with ALL fields in ONE block:
   - **Task description**: What needs to be done?
   - **Due date**: When is this due? (YYYY-MM-DD format, or "None" if no deadline)
   - **Duration**: How long will this take? (5min / 15min / 30min / 1hr / 2hr / 3hr+)
   - **Energy level**: What energy does this require? (High / Medium / Low)
   - **Context**: Where will you do this? (@office / @home / @claude)
3. **Create task** using canonical workflow above:
   - Check duplicates (Next.md only)
   - Determine metadata (Person/Email/Project if applicable)
   - Add special tags (#waiting/#agenda if needed)
   - Write to Tasks/Next.md
   - Create macOS Reminder (only if due date + time-sensitive)
4. **Confirm** - Single line: "Task added to @[context]."

**Interaction-specific notes**:
- Source format: `Manual entry (YYYY-MM-DD)`
- Ask for Person/Email/Project in questions if context suggests it
- AskUserQuestion tool for efficient data gathering

**Interaction Style**:
- **Minimal**: No "great", "excellent", "have a nice day"
- **Direct**: Ask questions → Create task → Confirm → Done
- **Efficient**: 5 questions maximum, then complete
- **No fluff**: Just questions, task, confirmation

## Next Item Workflow

**Pattern**: Standard Workflow
**Slash Command**: `/next-item [low|mid|high]`

**Purpose**: Show single highest-priority actionable task at specified energy level. Quick answer to "what should I do right now?"

**Parameters**: `low` (default), `mid`, `high`

**Sequence**:
1. Get fresh date/time (see Session Date/Time Handling section)
2. Parse energy level (default: low)
3. Detect current context (Mon-Fri 6am-6pm → @office, else → @home)
4. Read Tasks/Next.md and filter:
   - Exclude completed ([x]) and #waiting
   - Match energy (exact or close if none available)
   - Prefer current context (not hard filter)
5. Sort by priority:
   - Overdue → Due today → Due this week → No due date
   - Within each: prefer project-tagged tasks
6. Select TOP task
7. Format output with task, reasoning, suggested /execute-task action
8. Handle edge cases (no tasks at energy, all WAITING, none available)

**Interaction**: Focused (one task), contextual (explain WHY), actionable (suggest automation), respectful (no celebration).

**Use cases**: Meeting cancelled, working late, between tasks, energy level changed

## Meeting Types

**group meetings** = Meetings where ALL Group Leaders are present together (group meeting format)

**Meetings with GLs** = 1:1 meetings between you and individual Group Leaders (e.g., meetings with username, username, John individually)

## Automated Workflows

### Good Morning Workflow

**Pattern**: Standard Workflow
**Trigger**: "good morning"

**Purpose**: Prepare essential work system for the day in 1-2 minutes with single consolidated report. Sequences inbox scanning and calendar checking, and presents a single "System Ready" report.

**Sequence**:

**Step 0: Get fresh date/time context**
- Run: `date +"%Y-%m-%d %A %H:%M:%S"` to get current system time
- Parse: current date (YYYY-MM-DD), day of week, time (HH:MM:SS)
- Verify: Is it morning? If after 12pm, note "Running outside typical morning hours" in report
- Store for use in calendar operations and prioritization
- **Why**: Session may have started days ago; always use fresh date for accurate calculations

**PHASE 1: Scan All Inboxes (Parallel Execution)**

**IMPORTANT EXECUTION PATTERN**: Use ONE message with 4 Task tool calls to invoke all scanners together. After all 4 scanners complete and return results, use a SECOND separate message to invoke meeting-prep.

**DO NOT invoke meeting-prep in the same message as the scanners - wait for Phase 1 results first.**

Invoke 4 scanner agents together (in one message with 4 tool calls):

1. **reminders-scanner** - Process Reminders inbox (#agent tags)
2. **email-scanner** - Process email inbox (marks ALL emails as read for Inbox Zero)
3. **meetings-scanner** - Process Meetings/ folder (extract TODOs, move to Reference/)
4. **confluence-scanner** - Process Confluence tasks (@you tags)
   - **Check weekly frequency**: Only run if hasn't been run in last 7 days
   - Check Daily page history or ask user if uncertain about last run
   - If skipped: Note "Skipped - last run YYYY-MM-DD" in report

**Wait for ALL 4 scanners to return results** - You will receive 4 separate completion messages.

Capture from each: Tasks created, items processed

**PHASE 2: Check Calendar (Sequential - After Phase 1)**

**After receiving all Phase 1 results**, invoke meeting-prep agent in a NEW message:
- Use Task tool: `subagent_type="meeting-prep"`
- Gets today's calendar events
- Prepares meeting agendas for 1:1s
- Creates context for group meetings
- Writes to Daily page
- Capture: Number of meetings, agendas prepared

**IMPORTANT**: Wait for meeting-prep to complete before proceeding to Phase 3.

**PHASE 3: Consolidate Report (After All Phases)**
Create single "System Ready" report with:

Format:
```
## System Ready for [YYYY-MM-DD]

✅ **Inboxes cleared**
- Reminders: X tasks created
- Email: X emails processed (X marked as read, X tasks created)
- Meetings: X notes processed
- Confluence: [Skipped - last run YYYY-MM-DD] OR [X tasks created]

✅ **Calendar prepared**
- X meetings today with agendas ready
- See Daily/YYYY-MM-DD.md for details

**Your day is ready. What would you like to tackle first?**
```

**Step 6: Error Handling**
If any agent fails or returns errors:
1. Note which agent failed in the report
2. Include error summary
3. Continue with remaining agents (don't stop entire sequence)
4. Mark incomplete items with ⚠️ instead of ✅

Example error format:
```
⚠️ **Email inbox** - Error accessing MS Graph (auth expired)
   Manual action needed: Re-authenticate email access
```

**Interaction Style**:

**IMPORTANT: Be efficient and direct**
- NO "good morning" greetings
- NO "great", "excellent", "have a nice day"
- NO email summaries (email-scanner already reports this)
- Just: Run workflows → Present results → Ask question

**Silent execution**:
- Don't announce "Running X agent now..."
- Just run them and show final results
- Only mention agents if they fail

**End with question**:
- "What would you like to tackle first?"
- If user mentions specific task/project in "good morning" message, highlight it in priorities

**Contextual**:
- If user mentions specific work, highlight relevant priorities
- Example: "good morning, I need to work on FocusCraft" → highlight FocusCraft tasks

**Success Criteria**:
- All 2 workflow stages complete successfully
- Consolidated report is concise (fits in single screen)
- User has clear view of inbox status and calendar
- Total execution time: 1-2 minutes

### Check Calendar Workflow

**Pattern**: Agent-Based Workflow
**Slash Command**: `/check-calendar`
**Trigger**: Explicit call or "check calendar"
**Agent**: meeting-prep

**Purpose**: Prepare for all meetings in one go, create single source of truth for meeting agendas in Daily page.

**What it does**: Retrieves today's calendar events, processes each meeting (1:1s get prepared agendas, group meetings get context summaries), creates/updates person pages as needed, and writes all meeting agendas to Daily/YYYY-MM-DD.md. Defaults to Operational Focus unless Q/FY keywords detected.

**Implementation**: See `.claude/agents/meeting-prep.md`

### Weekly Planning Workflow

**Pattern**: Agent-Based Workflow
**Slash Command**: `/plan-week`
**Trigger**: On-demand when want to plan remaining days of current week
**Agent**: weekly-planner

**Purpose**: Create comprehensive weekly plan from today through end of current week (Sunday), analyzing calendar load, project priorities, and available capacity to identify what must be accomplished vs what can be deferred.

**What it delivers**: Weekly plan file in `Weekly/` folder with:
- Week overview (focus statement, critical deadlines, key meetings)
- Projects prioritized by criteria (High/Medium/Lower with reasoning)
- Daily schedule recommendations (detailed for critical days, high-level for routine days)
- Meeting-project connections (what to discuss in 1:1s and key meetings)
- Success criteria (must/nice/defer based on formula)
- Energy and cognitive load notes

**When to use**:
- Start of week (Monday) to plan full week ahead
- Mid-week (Wed-Thu) to replan remaining days
- Weekend (Sat-Sun) to prepare for upcoming week
- When priorities shift and need to reorganize

**Key features**:
- **Smart detail**: Detailed schedules for critical days (HYIs, strategic meetings, heavy deadlines), high-level for routine days
- **Meeting opportunities**: Connects 1:1 meetings to project tasks ("Discuss #komunikacija with Sindi")
- **Criteria-based prioritization**: High/Medium/Lower based on deadlines + meeting load + cognitive capacity (transparent reasoning shown)
- **Cognitive load awareness**: Flags heavy meeting weeks, preserves energy for critical events, defers long blocks when overloaded
- **Flexible scope**: Covers today through Sunday (adapts if run mid-week)

**Implementation**: See `.claude/agents/weekly-planner.md`

**Output location**: `Weekly/YYYY-W##.md` (ISO week format)

**Example use cases**:
- "Heavy meeting week (22 meetings) with 2 HYI preparations" → Plan identifies what to defer
- "Light meeting week (8 meetings)" → Plan suggests strategic projects to advance
- "Mid-week priority shift" → Re-run `/plan-week` to regenerate plan for remaining days

### Career Evaluation Workflow

**Workflow Name**: "Career Evaluation Workflow"
**Skill Name**: `career-evaluation`
**Slash Command**: None (invoked automatically or manually)

**Trigger**:
- Automatically suggested after `/check-calendar` detects promotion or hiring meetings
- Manual invocation: `Skill: career-evaluation` with Confluence URL

**Purpose**: Evaluate promotion and hiring proposals against your company's Salary Policy Handbook, grade expectations, and mindset frameworks. Generate concise 1-page evaluation reports with clear verdicts and recommendations.

**Detection Keywords**:
- **Promotion**: "promotion", "grade", "SPH", "career advancement"
- **Hiring**: "hiring", "employment", "candidate", "offer", "new hire"

**Sequence**:

1. **Detect Evaluation Type**
   - Check calendar event title for keywords
   - Read Confluence page to confirm type (different templates for hiring vs. promotion)
   - Auto-detect: Promotion or Hiring

2. **Gather Context**
   - Read proposal page (provided URL - Confluence, OneDrive, or other)
   - Read company policy documents:
     - Location: Configure path to your company's promotion/hiring guidelines
     - Examples: Grade expectations, promotion guidelines, role handbooks
   - Find similar past examples in your reference archive
   - Search for additional context (performance pages, goal tracking)
   - Search emails for recent communications

3. **Analyze Proposal**
   - **For Promotions**: Compare current grade performance vs. next grade requirements
   - **For Hirings**: Justify proposed starting grade for external candidate
   - Apply evaluation logic:
     - Grade requirements alignment
     - Soft skills and behavioral patterns (G4: accountability, PM communication, courage)
     - Development plan assessment (direction, milestones, alignment)
     - Risk patterns (entitlement-based, avoidance, lack of business value)
     - Regional/market considerations (business-driven progression)
   - Generate challenging questions (3-5 questions)

4. **Generate 1-Page Report**
   - **Promotion Report Includes**:
     - Summary (employee, grades, years in role, key achievements, promotion type)
     - Analysis (strengths with quotes, concerns/gaps with quotes and classification)
     - Grade requirements alignment
     - Challenging questions
     - Development plan assessment
     - Policy compliance checklist
     - Coverage metric (% of proposal analyzed)
     - Verdict: APPROVE / CHALLENGE / CONDITIONAL APPROVE

   - **Hiring Report Includes**:
     - Summary (candidate, proposed grade, experience, qualifications)
     - Analysis (strengths with quotes, concerns with quotes)
     - Grade justification
     - Cultural fit assessment (motivation stability, values alignment, growth potential)
     - Challenging questions
     - Development plan assessment
     - Policy compliance checklist
     - Coverage metric
     - Classification: SAFE HIRE / CONDITIONAL HIRE / NOT READY

5. **Save Report**
   - Save to `Daily/YYYY-MM-DD.md` directly after the specific meeting's agenda
   - Use `#### Evaluation Report` as subheading under the meeting
   - Also save copy to dedicated project folder if one exists

6. **Output to User**
   - Confirm evaluation type detected
   - Show brief summary of verdict
   - Point to full report location
   - Highlight critical concerns or conditions

**Special Evaluation Logic**:

- **G3/L4 Progression Promotions**: Don't require full G3/L5 criteria, should meet ~50% expectations or overperform in some areas with clear growth plans
- **Behavioral Risk Classification**:
  - Concern (blocking) - systemic pattern
  - Watch-point (monitor) - isolated/context-driven
  - No issue - acceptable
- **Eager but Immature**: Classify as low-risk G2 growth areas with coaching actions, NOT blockers
- **Use of Quotes**: Support both strengths and risks, describe behaviors/patterns
- **Regional Considerations**: Weigh business justification (margin, retention, rate uplift) for market-driven regions (e.g., US team)

**Integration with Check Calendar Workflow**:

When meeting-prep agent completes calendar checking:
1. Reviews prepared agendas for promotion/hiring keywords
2. Asks: "I found a [promotion/hiring] meeting for [candidate/employee]. Would you like me to evaluate the proposal?"
3. If yes, invokes career-evaluation skill with Confluence URL from meeting
4. Skill runs independently and saves report to Daily page

**Success Criteria**:
- Clear verdict with solid justification
- Quotes support strengths and concerns
- Development plan thoroughly assessed
- Report is concise (1 page) and actionable
- Challenging questions ready for meeting

**Policy Documents** (automatically loaded by skill):
- Grade expectations: Configure path to your company's grade/level documentation
- Promotion proposal guidelines
- Role handbooks (PM, TL, GL, etc.)
- Contribution frameworks
- Guidelines for evaluation discussions

**Past Examples** (for comparison):
- Location: Configure path to your reference archive of past evaluations
- Purpose: Calibration and standards comparison at each grade level

### Meeting Update Workflow

**Pattern**: Standard Workflow
**Slash Command**: `/update-meetings [date]`
**Trigger**: "meeting with [person] done" or explicit command

**Purpose**: Extract TODOs from meeting notes, update next meeting agenda, mark meeting complete.

**Reference**: Uses **Task Creation Workflow (Canonical)** for creating tasks.

**Sequence**:
1. Identify person (username format: jsmith)
2. Read People/username.md, check People/CLAUDE.md for special cases
3. Find meeting notes in Meetings/ folder from specified date or on personal confluence page (you can find it in username.md file)
4. Extract and process TODOs:
   - Check if TODO exists using canonical duplicate check (Next.md only)
   - If new: Create task using canonical workflow
   - **Meeting-specific**: Source format is `Meeting - [Title/Person] (YYYY-MM-DD)`
   - **Meeting-specific**: Person field is REQUIRED for 1:1 meetings
5. Update People/username.md "Meeting Agenda" section for next meeting
   - Apply Meeting Agenda Preparation Rules
   - Remove completed, add new actions, keep pending
6. Update Daily page with [COMPLETED] marker
7. Report reminders/tasks created

### Export Session Workflow

**Workflow Name**: "Export Session Workflow"
**Slash Command**: `/export-session`

**Trigger**: When you wants to preserve current session history before compacting

**Purpose**: Export the current Claude Code session history to the Sessions/ folder for future reference. This is useful before compacting a long conversation to preserve the full context.

**Sequence**:
1. Execute bash script that copies `~/.claude/history.jsonl` to `Sessions/` folder
2. Filename format: `YYYY-MM-DD-HHMM-claude-session.txt`
3. Confirm export with file location and size

**When to use**:
- Before running `/compact` to preserve conversation history
- At end of significant work sessions for documentation
- When switching contexts or starting new major tasks

**Output**: Session file saved in `Sessions/` folder with timestamp

### Project Archival Workflow

**Workflow Name**: "Project Archival Workflow"
**Trigger**: When you says "archive projects" or when a project is marked complete

**Purpose**: Systematically archive completed projects while preserving valuable deliverables in Reference/ for future use.

**When to Archive**:
- Project status = "complete" in Projects/Projects.md
- All follow-up tasks completed (approvals received, requests submitted, etc.)
- Archive immediately after project completion (don't wait)

**Sequence**:

1. **Check for Completed Projects**
   - Read `Projects/Projects.md` to identify projects marked complete
   - For each completed project found, ask: "Archive [Project Name] now or later?"
   - User decides whether to proceed with each project

2. **Identify Valuable Deliverables** (for projects being archived)
   - Review project folder contents
   - Identify deliverables worth preserving:
     - Documents, frameworks, processes, templates
     - Research findings, analysis reports
     - Email templates, meeting agenda templates
     - Checklists, workflows, guidelines
     - Any material that might be referenced in future work
   - Present list to user for confirmation

3. **Move Deliverables to Reference/**
   - Choose appropriate Reference/ subfolder based on content type:
     - `Reference/People/` - Career frameworks, promotion examples, HYI processes
     - `Reference/Concepts/` - Workflows, methods, frameworks, checklists
     - `Reference/Business/` - Strategy docs, market analysis, business plans
     - `Reference/Planning/` - Historical planning documents
     - `Reference/Culture/` - Communication plans, cultural initiatives
   - Keep original filenames or rename for clarity and discoverability
   - Organize in subfolders if needed (e.g., `Reference/People/Promotion Examples/`)

4. **Update Project File**
   - Add "Archived Deliverables" section to project file:
     ```markdown
     ## Archived Deliverables

     **Date Archived**: YYYY-MM-DD

     | Deliverable | New Location | Purpose |
     |-------------|--------------|---------|
     | [File name] | [[Path in Reference/]] | Why valuable for future |
     | [File name] | [[Path in Reference/]] | Why valuable for future |
     ```
   - This creates permanent record of what was saved and where

5. **Move Project Folder**
   - Move entire folder: `Projects/[Project Name]/` → `Projects/Archive/[Project Name]/`
   - All project files (including updated project file) move together

6. **Update Projects/Projects.md**
   - Remove from "## Active Projects" list
   - Optionally add to "## Archive" section:
     - Format: `- [[Projects/Archive/[Project Name]]] - Completed [date]: [brief outcome]`
     - Note: This step is optional since valuable deliverables are findable in Reference/

7. **Update Control Panel Dashboard**
   - Change status to "complete" with completion date
   - Keep in dashboard permanently (per existing rule - shows accomplishments)

**Example Interaction**:
```
User: "archive projects"
Claude: "I found 2 completed projects:
1. John 5-3 Promotion - marked complete on 2025-10-20
2. G5 Comparison Matrix - marked complete on 2025-10-10

Would you like to archive:
- John 5-3 Promotion? (yes/no/later)
- G5 Comparison Matrix? (yes/no/later)"

User: "yes to both"
Claude: [Proceeds with archival workflow for each project]
```

**Important Notes**:
- **Decision point**: User decides which deliverables are valuable BEFORE archiving
- **Not for active projects**: Luka promotion project example - NOT ready to archive yet (still pending approval meeting, HR system request)
- **Preservation focus**: Archive process prioritizes preserving reusable knowledge over just moving files
- **Discoverability**: Deliverables in Reference/ should be organized for future LLM and user discoverability

### Task Archival Workflow

**Workflow Name**: "Task Archival Workflow"
**Slash Command**: `/archive-tasks`

**Trigger**: When you explicitly calls `/archive-tasks`

**Purpose**: Move completed tasks from Tasks/Next.md to Archive/Tasks/Next.md to keep the active task list focused on actionable items.

**Sequence**:

1. **Read Tasks/Next.md** and identify all completed tasks (marked [x])
2. **Count and report** to user: "Found X completed tasks ready to archive"
3. **Read or create Archive/Tasks/Next.md**
   - If file doesn't exist, create it with proper structure
   - If file exists, read current contents
4. **Move completed tasks** to archive:
   - Preserve @office/@home context structure
   - Within each context, add at top (newest first by completion date)
   - Keep full metadata (Due, Duration, Energy, Source, Person, Note, deliverables)
   - Extract completion date from ✅ YYYY-MM-DD marker
5. **Remove from Next.md** - Delete archived tasks from active list
6. **Update archive metadata** - Update "Last archived" date and total count
7. **Report summary**:
   - X tasks archived
   - Archive location
   - Next.md cleaned up

**When to use**:
- After significant work sessions
- When completed tasks accumulate (10+ suggested threshold)
- Before starting new work cycles
- When Next.md feels cluttered

**Archive File Structure**:
```markdown
---
tags:
  - "#tasks-archive"
---
# Archived Tasks

Tasks that have been completed and moved from Next.md for historical reference.

## @office

- [x] [Task description] ✅ YYYY-MM-DD
  - Due:: YYYY-MM-DD
  - Duration:: X minutes
  - Energy:: High/Medium/Low
  - Source:: [Source information]
  - Person:: [[person]]
  - Note:: [Additional context]

[Ordered by completion date, newest first]

## @home

- [x] [Task description] ✅ YYYY-MM-DD
  - [Full metadata preserved]

[Ordered by completion date, newest first]

---

**Last archived**: YYYY-MM-DD
**Total tasks in archive**: X
```

### GTD Daily Workflow

**Pattern**: Multi-Phase Workflow System
**Purpose**: Complete task management from inbox to execution (GTD methodology)

**Recommended daily workflow** for managing all tasks.

**Relationship to Good Morning Workflow**: The [Good Morning Workflow](#good-morning-workflow) automates Phase 1 (Collect) of this methodology and includes calendar prep. Use "good morning" for quick inbox clearing and calendar setup, then run `/prepare-tasks` and `/prioritize-tasks` when you need to organize work.

#### Phase 1: Collect - `/scan-inboxes`
**When**: Morning or when inboxes need processing
**Runs**: 4 scanner agents sequentially
1. Reminders Inbox (#agent tags)
2. Email Inbox (mark ALL as read for Inbox Zero)
3. Meetings Folder (extract TODOs, move to Reference/)
4. Confluence Tasks (@you tags) - weekly frequency

**Result**: All tasks in Tasks/Next.md, reports in Daily page
**Time**: 10-15 min

#### Phase 2: Clarify - `/prepare-tasks`
**When**: After scanning, before prioritizing
**Reviews**: Clarity, completeness, complexity, dependencies
**Result**: Report identifying well-formed tasks vs needing improvement
**Output**: Daily/YYYY-MM-DD.md "## Task Preparation Report" (updated if rerun)
**Time**: 5-10 min

#### Phase 3: Organize & Prioritize - `/prioritize-tasks`
**When**: Morning (8-9am) or afternoon (1-2pm)
**Analyzes**: Time/energy, calendar, urgency, energy match, duration fit, strategic value
**Result**: Daily Priority Report with Today's Focus (3-5 tasks), Quick wins, Urgent, Due this week
**Output**: Daily/YYYY-MM-DD.md "## Daily Priority Report" (updated if rerun)
**Time**: 2-3 min

#### Phase 4: Execute
**Approach**: Work through Today's Focus, match energy, use Quick Wins in gaps, re-prioritize if interrupted
**Tips**: Block calendar time, take breaks, mark complete, note blockers

#### Quick Reference Commands
**Phase 1**: `/scan-inboxes` (or individual: /scan-reminders, /scan-emails, /scan-meetings, /scan-confluence)
**Phase 2-3**: `/prepare-tasks`, `/prioritize-tasks`
**Supporting**: `/check-calendar`, `/update-meetings`, "list tasks"

#### Usage Pattern
**Every day**: Phase 1 (Collect) once, typically morning
**As needed**: Phase 2 (Clarify) after major scan, Phase 3 (Prioritize) 1-2x/day, Phase 4 (Execute) continuous

**Time investment**: Full workflow 20-30 min morning, quick check 5 min afternoon
**Return**: Clarity, reduced decision fatigue, confidence in priorities

### Improvement Documentation Workflow

**Pattern**: Standard Workflow
**Slash Command**: `/improvement`
**Trigger**: After making system improvements to GTD workflows, agents, or documentation

**Purpose**: Streamline documenting GTD system improvements with consistent format, reduce friction, ensure complete context capture.

**When to use**:
- After fixing bugs in agents or workflows
- After implementing new features or enhancements
- After optimizing existing processes
- After establishing new patterns or standards
- Right after making changes (git can detect uncommitted work)

**Sequence**:

1. **Detect changes from git**:
   - Run `git status` to see modified files
   - Run `git diff --stat` to see change summary
   - Present to user: "I see you changed X files: [list]"
   - If no uncommitted changes, check recent commits (last 24 hours)

2. **Ask 4 targeted questions** (use AskUserQuestion):
   - **Problem/Opportunity**: What issue did this solve or opportunity did it address?
   - **Type**: System improvement / Bug fix / New feature / Documentation / Standards
   - **Impact Level**: High / Medium / Low
   - **Benefits**: What benefits does this provide? (time saved, quality improved, friction reduced, etc.)

3. **Generate improvement title**:
   - Format: `YYYY-MM-DD - [Brief descriptive title].md`
   - Suggest based on problem/solution (max 8-10 words)
   - Ask user to confirm or modify

4. **Create improvement document** with standard structure:
   ```markdown
   # [Improvement Title]

   **Date**: YYYY-MM-DD
   **Type**: [Type from question]
   **Impact**: [Level] - [Brief impact statement]

   ---

   ## Problem

   [Answer to question 1]

   ---

   ## Solution

   [Summary of what was changed]

   ---

   ## Implementation

   **Files modified**:
   [Auto-detected from git diff - list files with brief description of changes]

   **Key changes**:
   - [Bullet points of significant changes]

   **Commit**: [Git commit hash if available]

   ---

   ## Impact Assessment

   [Answer to question 4]

   ### Time Savings
   [If applicable - quantify time saved]

   ### Quality Improvements
   [If applicable - describe quality benefits]

   ### Workflow Improvements
   [If applicable - describe process improvements]

   ---

   ## Pattern Established

   [If this establishes a new pattern or standard, describe it here]

   ---

   ## Related Improvements

   [Auto-detect: Check for improvements from same date or similar topics in filename]
   [List related improvements with dates and titles]

   ---

   ## Next Steps

   [If applicable - future work needed, monitoring required, validation planned]

   ---

   **Improvement Status**: ✅ Complete and documented
   ```

5. **Save document**:
   - Location: `Reference/Concepts/GTD/Improvements/`
   - Filename: [title from step 3]
   - Confirm save location and file size

6. **Report completion**:
   - Show file path (absolute)
   - Show document size (lines)
   - Optionally: Suggest adding to next git commit message

**Example Interaction**:
```
User: "/improvement"
Claude: "I see you changed 3 files:
- CLAUDE.md (Task Creation Workflow section)
- .claude/agents/prioritizer.md (Removed duplication)
- Tasks/Next.md (Added special tags header)

[Asks 4 questions via AskUserQuestion]"

User: [Provides answers]

Claude: "Suggested title: 2025-11-07 - Task Folder Structure Simplification and SOMEDAY Tag.md
Use this title? (yes/modify)"

User: "yes"

Claude: "Document created:
[vault path]/Reference/Concepts/GTD/Improvements/2025-11-07 - Task Folder Structure Simplification and SOMEDAY Tag.md
Size: 267 lines

Ready to commit."
```

**Success Criteria**:
- ✅ All sections completed
- ✅ Git changes properly detected
- ✅ Format matches existing improvement docs
- ✅ File saved to correct location
- ✅ Related improvements linked

## Control Panel Dashboard Updates

**Location**: `[control panel]/index.html`

**Current Status**: Manual updates (automation planned - see [Future Improvements](#future-improvements--migration-tasks))

**When to Update**: Whenever project status changes in Projects/Projects.md

**How to Update**:
1. Edit the `projects` array in `index.html` (around line 257)
2. Update project fields:
   - `name`: Project title
   - `status`: "active", "complete", or "planned"
   - `description`: Current state description
   - `statusDate`: Date when project entered current status (format: "YYYY-MM-DD")
   - `plannedDate`: For planned projects only, target start date (format: "YYYY-MM-DD" or `null`)
3. Stats will automatically recalculate

**Project Status Mapping**:
- **Active** → Projects currently being worked on (blue badge)
- **Complete** → Projects finished or ready for approval/review (green badge)
- **Planned** → Projects not yet started (gray badge)

**Date Fields**:
- **statusDate**: Always required - when did project enter this status?
- **plannedDate**: Only for "planned" status - when is project scheduled to start?

**Example Project Entry**:
```javascript
{
    name: "Project Name",
    status: "active",
    description: "Current state description",
    statusDate: "2025-10-11",  // When became active
    plannedDate: null          // null for active/complete
}
```

**Workflow Integration**: When updating project status in Projects/Projects.md, also update control_panel/index.html to keep dashboard in sync.

**Important**: When a project is completed:
- Remove from Projects/Projects.md active list (optionally move to Archive section)
- **Keep in control_panel** - change status to "complete" with completion date
- Completed projects remain visible in dashboard for historical tracking
- Never remove completed projects from control panel - they show accomplishments

## Session Date/Time Handling

**Problem**: Claude Code sessions can persist across multiple days, causing date/time context to become stale. The `<env>` tag shows the date when the session started, not the current date.

**Impact**: Stale dates affect:
- Due date calculations (overdue, due today, due this week)
- Context detection (@office vs @home based on time of day)
- Energy pattern matching (morning vs afternoon vs evening)
- Calendar event filtering ("today's meetings")
- Any workflow using "today", "overdue", or time-based logic

**Solution**: Always get fresh date/time at the start of date-sensitive workflows.

### When to Check Current Date/Time

Check fresh date/time when ANY of these apply:
- ✅ Calculating "due today", "overdue", "due this week"
- ✅ Detecting context (@office vs @home based on time)
- ✅ Determining energy patterns (morning vs afternoon vs evening)
- ✅ Filtering calendar events by "today"
- ✅ Making any comparison involving current date/time

### How to Get Fresh Date/Time

**Command**: `date +"%Y-%m-%d %A %H:%M:%S"`

**Output format**: `2025-10-29 Wednesday 11:37:43`

**Parse**:
- **Date**: YYYY-MM-DD (for due date calculations)
- **Day of week**: Monday-Friday vs Saturday-Sunday
- **Time**: HH:MM:SS (24-hour format)

**Context logic**:
```
Hour < 6 OR Hour >= 18 → Evening/Home
Hour >= 6 AND Hour < 18 AND (Mon-Fri) → Office
Weekend (Sat-Sun) → Home
```

**Energy pattern logic**:
```
Hour < 12 → Morning (peak energy)
Hour >= 12 AND Hour < 17 → Afternoon (execution energy)
Hour >= 17 → Evening (low energy)
```

### Implementation Pattern

Add this as **Step 0** or **Step 1** in date-sensitive workflows:

```markdown
1. **Get fresh date/time context**:
   - Run: `date +"%Y-%m-%d %A %H:%M:%S"` to get current system time
   - Parse: current date (YYYY-MM-DD), day of week, time (HH:MM:SS)
   - Store for use in priority sorting and context detection
   - **Why**: Session may have started days ago; always use fresh date for accurate calculations
```

### Updated Workflows

The following workflows have been updated to use fresh date/time:
- ✅ **Next Item Workflow** - Gets fresh date/time in Step 1
- ✅ **Prioritizer Agent** - Gets fresh date/time in Step 1.1
- ✅ **Morning Orchestrator** - Verifies current date/time in Step 0
- ✅ **Meeting Update Workflow** - Uses fresh date for "today", "yesterday" calculations

### Full Documentation

See detailed implementation guide: `Reference/Concepts/GTD/Architecture/Session Time Handling.md`
