---
description: Review time allocation across work contexts for the previous calendar month
---

Generate a time allocation report showing how time was distributed across contexts and projects for the previous calendar month.

**Input:** $ARGUMENTS
- No argument → all contexts, percentages show cross-context distribution
- Context name (e.g., "Yamaha", "APM") → filter to that context only, 100% represents that context's internal distribution

**Prerequisite:** `Contexts/` must be a git repo. Initialize with `cd ~/Documents/My\ Vault/Contexts && git init && git add . && git commit -m "Initial commit"` if not already set up.

---

## 1. Parse Input and Calculate Date Range

- Check $ARGUMENTS for optional context filter (case-insensitive match: "yamaha" matches "Yamaha Guitar Group", "apm" matches "APM Music")
- Calculate previous calendar month bounds:
  - If today is Feb 3, 2026 → target month is January 2026 (Jan 1-31)
  - Use `date` commands or calculate programmatically
- Store: `$START_DATE` (YYYY-MM-01) and `$END_DATE` (YYYY-MM-[last day])

---

## 2. Gather Contexts/ Document Activity (Weight: 3)

Run git log in ~/Documents/My Vault/Contexts:

```bash
cd ~/Documents/My\ Vault/Contexts && git log --since="$START_DATE" --until="$END_DATE" --name-only --pretty=format:""
```

For each file changed:
- Extract context from path: `Contexts/[Context Name]/...` → Context Name
- Count unique files changed per context
- Each unique file = 3 units

If context filter is active, only count files matching that context.

---

## 3. Gather ~/Projects Git Commits (Weight: 2)

Scan all git repos under ~/Projects (including nested like ~/Projects/APM Music/):

```bash
find ~/Projects -name ".git" -type d 2>/dev/null
```

For each repo found:
```bash
git -C [repo_path] log --oneline --since="$START_DATE" --until="$END_DATE" --author="$(git config user.email)"
```

**Repo to vault mapping:** Read the mapping table from `Resources/Meta/Claude/rules/vault/daily-notes.md`:

| Repo Path | Vault Project | Context |
|-----------|---------------|---------|
| `~/Projects/APM Music/*` | Various | APM Music |
| `~/Projects/Inner Dialogue/*` | Inner Dialogue | Personal |
| `~/Projects/context-management-*` | Various | Personal |

Derive context from:
1. Explicit mapping in daily-notes.md
2. Path structure (e.g., `~/Projects/APM Music/` → APM Music)
3. Unmapped repos → "Personal" (default)

Each commit = 2 units. Group by project.

If context filter is active, only count commits from repos matching that context.

---

## 4. Gather Calendar/ Notes (Weight: 2)

Find notes from target month:

```bash
ls Calendar/$YEAR-$MONTH-*.md 2>/dev/null
```

For each Calendar note:
- Read frontmatter to extract `context:` field (wikilink format: `"[[APM Music]]"`)
- Determine note type from `type:` field (Meeting, Thread, Journal)
- Meetings and Threads = 2 units each
- Journal (daily notes) = 0 units (they aggregate other work, avoid double-counting)

If context filter is active, only count notes with matching context.

---

## 5. Gather Daily Note Project Mentions (Weight: 1)

Read daily notes from target month (`Calendar/YYYY-MM-DD.md`):

For each daily note:
- Find the `### Log` section
- Parse parent bullets (project references like `- [[Project Name]]`)
- Extract project names from wikilinks
- Determine context from the project's location or frontmatter

Each unique project mention per day = 1 unit.

If context filter is active, only count mentions of projects in that context.

---

## 6. Compile Discovered Themes

Group all activity:
- **Level 1:** Context (derived from Contexts/ paths, frontmatter, repo mapping)
- **Level 2:** Project/Initiative (specific item within context)

Build a structure:
```
{
  "Yamaha Guitar Group": {
    "F20": { units: 15, breakdown: { docs: 6, commits: 4, meetings: 4, mentions: 1 } },
    "Stadium": { units: 8, ... }
  },
  "APM Music": {
    "AIMS Unified Search": { units: 22, ... },
    "Video Search": { units: 10, ... }
  },
  "Personal": {
    "Inner Dialogue": { units: 5, ... }
  }
}
```

For items that can't be attributed to a known context/project, group under "Unattributed".

---

## 7. Ask User Which Themes to Include

Present discovered projects as a multiSelect question:

Group options by context for clarity. Pre-check all by default.

Example format for AskUserQuestion:
```
Question: "Which projects should be included in the timesheet?"
Options grouped by context:
- Yamaha Guitar Group
  - [ ] F20 (15 units)
  - [ ] Stadium (8 units)
- APM Music
  - [ ] AIMS Unified Search (22 units)
  - [ ] Video Search (10 units)
- Personal
  - [ ] Inner Dialogue (5 units)
```

Wait for user selection before proceeding.

---

## 8. Calculate and Present Allocation

After user confirms themes:

**All contexts mode (no filter):**
- Total = sum of all selected units across all contexts
- Context % = (context total / grand total) * 100
- Project % = (project units / grand total) * 100

**Single context mode (filter active):**
- Total = sum of selected units from specified context only
- 100% represents that context's internal distribution
- Project % = (project units / context total) * 100

Round all percentages to whole numbers.

---

## Output Format

```markdown
## [Month Year] Time Allocation

### [Context Name] (XX%)
| Project | % |
|---------|---|
| Project A | XX |
| Project B | XX |

### [Context Name] (XX%)
| Project | % |
|---------|---|
| Project C | XX |
| Project D | XX |

### Unattributed (X%)
| Item | % |
|------|---|
| Misc work | X |
```

**For single-context mode:** Omit context-level header (since there's only one), just show projects:

```markdown
## [Month Year] Time Allocation: [Context Name]

| Project | % |
|---------|---|
| Project A | XX |
| Project B | XX |
| Other | X |
```

---

## Summary Statistics

After the table, include:

```markdown
---
**Data sources:** X documents edited, Y commits, Z meetings/threads, W daily log entries
**Total weighted units:** N
```

---

## Error Handling

- **Contexts/ not a git repo:** Warn and skip document tracking; proceed with other sources
- **No activity found:** "No activity found for [month]. Either the month is too old for git history, or no tracked work occurred."
- **Context filter matches nothing:** "No context matching '[filter]' found. Available contexts: [list]"
