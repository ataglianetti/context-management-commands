---
description: Weekly review of active work items - update statuses
---

Review and update status of work items:

**1. Find all "In Progress" items:**

Search for Stories and Tasks with `status: In Progress` across both contexts.

**2. For each item, ask user:**
- Still actively working on this?
- If yes → keep In Progress
- If done → Complete
- If paused → On Hold (ask why - blocked? deprioritized?)
- If not started after all → back to Ready or Backlog

**3. Present items grouped by context:**

Use AskUserQuestion with multi-select for batch updates:
- Show item name and parent project
- Let user select which ones to update
- Ask for new status

**4. Update selected items:**
- Edit the `status:` field in frontmatter
- Add `modified:` date

**5. Summary:**
- Report what was updated
- Show remaining In Progress count per context

**Status definitions:**
- **Backlog** - Not started, not yet prioritized
- **Ready** - Not started, ready to pick up
- **In Progress** - Actively being worked on
- **Review** - Done, awaiting review/approval
- **Complete** - Done
- **On Hold** - Started but paused (blocked, deprioritized, waiting)

**Epics use simplified statuses:**
- **Active** - Has work happening
- **Complete** - All work done
- **On Hold** - Paused

