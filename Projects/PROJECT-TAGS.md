# Project Tags - Master List

**Purpose**: Unique tags for connecting tasks in Next.md to their parent projects
**Format**: snake_case (lowercase with underscores)

---

## Example Project Tags

| Project Name | Tag | Folder |
|--------------|-----|--------|
| Q1 Planning | #q1_planning | Projects/Q1 Planning/ |
| Website Redesign | #website | Projects/Website Redesign/ |
| Team Onboarding | #onboarding | Projects/Team Onboarding/ |
| Product Launch | #launch | Projects/Product Launch/ |
| Marketing Campaign | #marketing | Projects/Marketing Campaign/ |

**Note**: These are examples. Replace with your actual projects.

---

## Tag Naming Rules

1. **Format**: snake_case (lowercase, underscores for spaces)
2. **Length**: Keep short but meaningful (2-3 words max)
3. **Uniqueness**: Each project has exactly one tag
4. **Simplicity**: Drop unnecessary words if clear without them

**Good examples**:
- "Q1 Budget Planning" → #q1_budget
- "Website Redesign Phase 2" → #website_v2
- "Customer Onboarding" → #onboarding

**Avoid**:
- #q1_budget_planning_project (too long)
- #qbp (too abbreviated)
- #Q1Budget (use lowercase)

---

## Usage in Tasks/Next.md

**Task format**:
```markdown
- [ ] Task description #project_tag #other_tags
  - Due:: YYYY-MM-DD
  - Duration:: X minutes
  - Energy:: High/Medium/Low
  - Source:: Where it came from
  - Person:: [[person]] (if applicable)
  - Note:: Additional context
```

**Example**:
```markdown
- [ ] Draft Q1 budget proposal #q1_planning
  - Due:: 2025-11-15
  - Duration:: 2hr
  - Energy:: high
  - Note:: Include department breakdown and headcount projections
```

---

## Finding Project Tasks

**Search by tag**:
- **Obsidian**: Click any #project_tag or search
- **Grep**: `grep "#q1_planning" Tasks/Next.md`
- **Claude Code**: `Grep pattern="#q1_planning" path="Tasks/Next.md"`

**Result**: See all tasks for that project instantly

---

## Integration with Workflows

**When creating tasks from projects**:
1. Identify project tag from this file
2. Add tag inline in task title
3. Also add other relevant tags (#waiting, #someday, etc.)

**When reviewing projects**:
- Grep for project tag to see all related tasks
- Update project status based on task completion
- Sync between project file and Next.md via tag search

---

## Archived Projects

**When project is archived**:
- Keep project tag on completed tasks (for historical tracking)
- Don't add tag to new tasks for that project
- Tag remains searchable for reference

---

**This file is your master reference for all project tags.**

Add new projects here as you create them. Keep tags consistent and unique.
