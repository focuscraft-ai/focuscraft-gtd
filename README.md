# FocusCraft GTD System

**Version 0.9.3** | [Documentation](CLAUDE.md) | [Get License](#get-license)

**AI Chief of Staff that saves managers 6 hours/week**

Complete GTD system powered by Claude Code. Scans inboxes, clarifies tasks, recommends priorities, executes work autonomously. Built by a manager of 100+ people who uses it daily.

**💾 Source-available** (code visible, license required to use) | **🔒 100% local processing** (privacy-first)

---

## Get License

This code is source-available for transparency and auditability. **License required to use.**

### Personal Use
**Pay What You Want** (Suggested €149, minimum €0)

For personal productivity, hobbies, non-work tasks.

**[Get Personal License →](https://focuscraft.lemonsqueezy.com/buy/3710cab5-3c72-4cbe-ba9b-770d1f4ebe25)**

### Commercial Use
**€299 per user** (One-time payment)

For work, business, managing teams. **ROI in less than one working day** (6 hours/week saved).

**[Get Commercial License →](https://focuscraft.lemonsqueezy.com/buy/5bf67e32-3f7d-4f90-84c1-9f61bca72a1d)**

**Need 5+ licenses?** Email support@focuscraft.io for bulk pricing.

---

## Key Features

- **Automated Inbox Processing** - Scan emails, meetings, and tasks automatically
- **AI-Powered Prioritization** - Get daily recommendations based on context and energy
- **Meeting Preparation** - Agendas ready before every meeting
- **Task Execution** - Autonomous agents that complete tasks for you
- **Zero Configuration** - Works immediately with file-based mode

---

## Quick Start (5 Minutes)

### 1. Open This Vault in Your Markdown Editor

**Option A: Obsidian** (Recommended for GTD features)
```bash
open -a Obsidian "/path/to/focuscraft-gtd"
```
Or: File → Open Vault → Select this folder

**Option B: VS Code**
```bash
code "/path/to/focuscraft-gtd"
```
Or: File → Open Folder → Select this folder

**Option C: Any Other Editor**
- Typora, Sublime Text, Vim, Emacs, Zettlr, or any markdown editor
- Just open the folder and edit .md files directly

### 2. Try the File-Based System

The vault works immediately without any setup! Try it:

1. **Add a task** to `Inbox/tasks/example-task.md` (see example files)
2. **Run** `/scan-inboxes` in Claude Code
3. **Check** `Tasks/Next.md` - your task is now there!
4. **Run** `/prioritize-tasks` to get today's recommended priorities

That's it! You're using the GTD system.

### 3. Daily Workflow

Every morning:
```
/scan-inboxes        # Collect all tasks from inboxes
/prepare-tasks       # Review task quality
/prioritize-tasks    # Get today's focus list
```

Before meetings:
```
/check-calendar      # Prepare meeting agendas
```

That's your complete daily workflow!

---

## What Is This?

FocusCraft GTD is an **intelligent task management system** that:

- ✅ **Works immediately** - No configuration needed
- ✅ **Processes inboxes automatically** - Email, meetings, tasks
- ✅ **Suggests priorities** - Knows when you have energy for each task
- ✅ **Prepares meetings** - Agendas ready before you join
- ✅ **Grows with you** - Start simple, add power as needed

---

## How It Works

### The GTD Method

GTD (Getting Things Done) is a proven productivity methodology with 5 steps:

1. **Collect** - Gather everything from all inboxes
2. **Clarify** - Is it actionable? What's the next action?
3. **Organize** - Put it in the right place
4. **Reflect** - Review and prioritize
5. **Engage** - Do the work

FocusCraft automates steps 1-4 so you can focus on step 5.

### Two Operating Modes

**Mode 1: File-Based (Default)**
- Inboxes are folders with markdown files
- Everything works locally
- No external services needed
- Perfect for getting started

**Mode 2: MCP-Enhanced (Optional)**
- Connects to Microsoft 365 (calendar, email)
- Connects to Atlassian (Confluence, Jira)
- Connects to macOS Reminders
- Automatic inbox scanning

**All agents work in both modes.** They try MCP first, fall back to files automatically.

---

## Folder Structure

```
├── Inbox/               # File-based inboxes (add items here)
│   ├── emails/         # Email-like messages
│   ├── meetings/       # Meeting notes awaiting processing
│   ├── tasks/          # Miscellaneous tasks
│   └── other/          # Other items
├── Tasks/
│   └── Next.md         # All active tasks (THE core file)
├── Projects/           # Project folders
│   └── Projects.md     # Project index
├── People/             # Person pages for 1:1s
├── Daily/              # Daily notes (YYYY-MM-DD.md)
├── Drafts/             # Work-in-progress deliverables
├── Reference/          # Permanent reference material
├── Templates/          # Note templates
└── CLAUDE.md           # Complete system documentation
```

---

## Key Features

### 1. Intelligent Inbox Processing

**File-Based**:
- Drop markdown files in `Inbox/` folders
- Run `/scan-inboxes`
- Tasks automatically extracted to `Tasks/Next.md`
- Inbox cleared, files archived

**MCP-Enhanced**:
- Scans live email inbox
- Processes calendar events
- Reads Reminders app
- Checks Confluence tasks

### 2. Smart Prioritization

Run `/prioritize-tasks` to get:
- **Today's Focus**: 3-5 top tasks with time blocks
- **Quick Wins**: Sub-15min tasks for gaps
- **Urgent Items**: Due today or overdue
- **Energy Matching**: High-energy tasks in morning, low-energy in evening

The prioritizer considers:
- Current time and energy level
- Calendar schedule
- Task urgency and deadlines
- Strategic value

### 3. Meeting Preparation

Run `/check-calendar` to:
- Get today's meetings (from calendar or Daily note)
- Prepare agendas for 1:1s (from person pages)
- Summarize context for group meetings
- Write everything to today's Daily note

Never walk into a meeting unprepared again.

### 4. Task Quality Control

Run `/prepare-tasks` to:
- Identify vague tasks
- Flag missing metadata
- Suggest improvements
- Find hidden projects

Get actionable tasks, not just to-do items.

---

## File-Based Inbox System

The vault includes sample inbox files showing the format. Here's how to use them:

### Email Inbox

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

### Meeting Notes

Create files in `Inbox/meetings/` with this structure:

```markdown
---
date: 2025-10-26
attendees: [John Smith, Sarah Chen]
---

# Meeting: Q1 Planning Review

**Date**: 2025-10-26 10:00-11:00
**Attendees**: John Smith, Sarah Chen, Alex Rivera

## Notes
- Discussed budget approval process
- Need to finalize team assignments by Friday

## Action Items
- [ ] John: Draft Q1 budget proposal (Due: Friday)
- [ ] Sarah: Schedule team kickoff meeting
```

### Task Inbox

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

Then run `/scan-inboxes` to process everything!

---

## Optional: MCP Integration

### What is MCP?

MCP (Model Context Protocol) lets Claude Code connect to external services. It's **completely optional** - the system works great without it.

**Want to unlock the full power of FocusCraft? Add MCP servers!**

MCP servers enable live integrations with your tools, making the system even more powerful. The good news: **you can add them instantly** using Claude Code's built-in MCP support.

**Official Documentation**: [How to Add MCP Servers to Claude Code](https://docs.claude.com/en/docs/claude-code/mcp)

### Why Add MCP?

**File-based mode is fully functional**, but MCP adds:
- **Live calendar integration** - Auto-read your calendar (no manual Daily note updating)
- **Automatic email scanning** - Scan real inbox (no manual file creation)
- **Direct Reminders app integration** - Sync with macOS Reminders
- **Confluence/Jira task reading** - Pull tasks directly from Atlassian
- **Real-time data** - Work with live data instead of manual file updates

### Which Agents Benefit from MCP?

| Agent | Without MCP | With MCP |
|-------|-------------|----------|
| **email-scanner** | Scans `Inbox/emails/` files | Scans live Microsoft 365 inbox |
| **meeting-prep** | Reads Daily/ notes for meetings | Reads live calendar via MS Graph |
| **inbox-scanner** | Scans `Inbox/tasks/` files | Reads macOS Reminders app |
| **meeting-scanner** | Scans `Inbox/meetings/` files | Can access Confluence meeting notes |
| **execute-task** | Uses vault files only | Can search emails, check calendar, read Confluence |

**All agents automatically detect MCP and use it when available. No configuration changes needed!**

### How to Add MCP

**Quick Start**: Follow the [official Claude Code MCP documentation](https://docs.claude.com/en/docs/claude-code/mcp) for step-by-step setup.

**Basic Steps**:

1. **Open Claude Code Settings**
   - Click gear icon
   - Go to "MCP Servers" tab

2. **Add Server Configurations**

Example configurations (add to MCP settings):

**Microsoft 365** (Calendar, Email, Teams, OneDrive):
```json
{
  "mcpServers": {
    "ms-graph-tools": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-microsoft-graph"]
    }
  }
}
```

**Atlassian** (Confluence, Jira):
```json
{
  "mcpServers": {
    "atlassian": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-atlassian"]
    }
  }
}
```

**macOS Reminders**:
```json
{
  "mcpServers": {
    "task-agent": {
      "command": "npx",
      "args": ["-y", "mcp-task-server"]
    }
  }
}
```

3. **Authenticate**
   - First use will prompt for authentication
   - Follow OAuth flow for each service
   - Permissions stored securely

4. **Test**
   - Run `/check-calendar` - if you see actual meetings, it's working!
   - Run `/scan-inboxes` - if emails are scanned, email MCP works!

**All agents automatically detect MCP and use it if available. Zero configuration changes needed.**

**Need help setting up MCP?** Check the [official documentation](https://docs.claude.com/en/docs/claude-code/mcp) for detailed instructions and troubleshooting.

---

## Slash Commands Reference

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/scan-inboxes` | Scan all inboxes and collect tasks | Morning or when inbox is full |
| `/prepare-tasks` | Review task quality and clarity | After scanning inboxes |
| `/prioritize-tasks` | Get today's priority recommendations | Morning, afternoon, or when priorities shift |
| `/check-calendar` | Prepare meeting agendas | Morning or before important meetings |
| `/archive-tasks` | Move completed tasks to archive | Weekly or when Next.md is cluttered |

---

## Example Daily Workflow

### Morning (8:00 AM)

```
You: "good morning"
Claude: [Greeting and overview]

You: /check-calendar
Claude: [Prepares agendas for today's 3 meetings]

You: /scan-inboxes
Claude: [Processes 15 emails, 2 meetings, 5 task files]
        [Creates 8 tasks in Tasks/Next.md]

You: /prepare-tasks
Claude: [Reviews 8 new tasks + 12 existing]
        [Identifies 3 vague tasks, suggests improvements]

You: [Clarifies the 3 vague tasks]

You: /prioritize-tasks
Claude: [Analyzes 20 tasks, calendar, energy]
        [Suggests 5 priorities for today]

You: [Starts working on top priority]
```

**Time invested**: 15-20 minutes
**Return**: Complete clarity on what to work on, all inboxes cleared

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

All workflows are documented in `CLAUDE.md`. Modify them to match your:
- Work style
- Team structure
- Industry needs
- Personal preferences

---

## Learning Path

1. ✅ **Day 1**: Read this README, try file-based inboxes
2. ✅ **Week 1**: Use daily workflow every morning
3. ✅ **Week 2**: Add person pages for your team
4. ✅ **Week 3**: Create your first project
5. ✅ **Month 1**: Add MCP integrations (optional)
6. ✅ **Month 2**: Customize workflows to your needs

---

## Troubleshooting

### Agents Not Finding Files

**Problem**: Agent can't read Tasks/Next.md
**Solution**: Check file paths are absolute, verify folder structure matches documentation

### Tasks Not Being Extracted

**Problem**: Inbox files processed but no tasks created
**Solution**: Check task format matches examples, review scanner agent rules

### MCP Tools Not Working

**Problem**: MCP integration errors
**Solution**: Agents automatically fall back to file mode. Check MCP server configuration and authentication

### Priority Suggestions Seem Off

**Problem**: Prioritizer recommends wrong tasks
**Solution**: Check task metadata (Duration, Energy, Due date), ensure it's accurate

---

## Getting Help

### Documentation Hierarchy

1. **This README** - Quick start and overview
2. **CLAUDE.md** - Complete system guide (read this for deep understanding)
3. **Agent files** (`.claude/agents/`) - Specific agent behaviors
4. **Command files** (`.claude/commands/`) - Slash command prompts

### Questions?

- Check example files in the vault - they show realistic usage
- Read workflow documentation in CLAUDE.md
- Look at Daily notes for scanner output examples
- Review Tasks/Next.md for task format examples

---

## What Makes This Different?

**Traditional Task Managers**:
- Manual inbox processing
- No context awareness
- Static priority lists
- Disconnected from work tools

**FocusCraft GTD**:
- ✅ **Automated** - Inboxes process themselves
- ✅ **Intelligent** - Understands energy, time, context
- ✅ **Dynamic** - Priorities adapt to your day
- ✅ **Integrated** - Optional connections to your tools
- ✅ **Transparent** - All data in readable markdown files
- ✅ **Flexible** - Works file-based or MCP-enhanced

---

## Philosophy

**Start Simple, Add Power**:
- File-based mode works immediately
- Learn the workflows before adding complexity
- Add MCP only when you feel the pain of manual processing
- Customize gradually based on real needs

**System Grows With You**:
- Week 1: Basic task management
- Month 1: Full GTD workflow
- Month 3: Team collaboration patterns
- Month 6: Custom workflows and integrations

**Trust the Process**:
- GTD has worked for millions
- The system automates the tedious parts
- Your job: focus on doing the work
- Let FocusCraft handle the rest

---

## Credits

- **GTD Method**: David Allen
- **Obsidian**: Excellent knowledge base platform (recommended but not required)
- **Claude Code**: AI-powered automation
- **You**: For choosing to take control of your tasks

---

## License

This vault structure and workflows are provided as-is for personal and commercial use. Feel free to adapt to your needs.

---

**Ready to get started?**

1. Open this vault in your markdown editor (Obsidian, VS Code, or any editor)
2. Run `/scan-inboxes` to see it work
3. Check `CLAUDE.md` for deep understanding
4. Build your productivity system!

*Your future organized self will thank you.*
