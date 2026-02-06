---
description: Weekly APM initiative updates for JIRA Idea Board
---

Generate JIRA-ready comments for APM initiatives that had activity in the past week.

**Cadence:** Weekly
**Audience:** Stakeholders (via JIRA Idea Board)
**Output:** Separate 2-3 sentence comment per active initiative, ready to paste

---

## 1. Find Active APM Initiatives

Scan `Contexts/APM Music/Portfolio/` for initiatives.

For each initiative, check for activity in the past 7 days:
- Documents/ changes (git log)
- Calendar/ meetings or threads with `context: "[[APM Music]]"` and `about:` linking to the initiative
- Daily note mentions

**Only include initiatives with activity.** Skip those with no changes.

---

## 2. Gather Activity Per Initiative

For each active initiative:

**What changed:**
- Specs updated, decisions made
- Meetings held, stakeholder feedback received
- Code shipped or in progress

**What's next:**
- Upcoming milestones
- Blockers or dependencies

---

## 3. Generate JIRA Comments

For each active initiative, generate a standalone comment:

```markdown
## [Initiative Name]

[2-3 sentences: what changed this week, what's next. High level, no implementation details.]
```

**Style guidance:**
- Lead with the most important change
- Keep it high level (stakeholders don't need technical details)
- End with forward momentum (what's coming, not what's stuck)
- If blocked, mention briefly but frame constructively

**Example:**
> Completed search API integration and deployed to staging. Design review scheduled for Thursday to finalize the UI. On track for next week's release window.

---

## 4. Output

Display each initiative's comment separately, clearly labeled so you can copy/paste into the corresponding JIRA ticket.

```markdown
---
### [[Initiative A]]
[comment]

---
### [[Initiative B]]
[comment]
```

If no APM initiatives had activity this week, say so.
