---
description: Generate daily note log from today's vault notes and git commits
modified: 2026-01-28T09:00:00-08:00
---

Generate a synthesized log for today's daily note based on:
- **Calendar/** notes created today (meetings, threads)
- **Contexts/** changes via git diff (PRDs, specs, portfolio items)
- **~/Projects** git commits

**Prerequisite:** `Contexts/` must be a git repo. Initialize with `cd ~/Documents/My\ Vault/Contexts && git init && git add . && git commit -m "Initial commit"` if not already set up.

**1. Find today's daily note**
- Path: `Calendar/YYYY-MM-DD.md` (current date)
- If it doesn't exist, create it using the Daily Note template located here:
	- Resources/Templates/Daily Note.md

**2. Find notes touched today**

**Calendar/ folder** (meeting notes, threads):
- Search for files created today (use file creation date)
- Include types: Meeting, Thread
- These are event-based notes; their existence is the log entry

**Contexts/ folder** (git-tracked):
- Run `git status` and `git diff` to find files with uncommitted changes
- Run `git log --since="midnight"` to find files committed today
- For each changed file, extract the actual diff to summarize what changed (sections added, content removed, key edits)

Skip:
- The daily note itself
- Contexts/ files with no meaningful diff (whitespace, metadata-only)

**3. Scan git commits from ~/Projects**

For each git repository in `~/Projects` (including subdirectories like `~/Projects/APM Music/`):
- Run `git log --oneline --since="midnight" --author="$(git config user.email)"` to get today's commits
- Group commits by repository

For each commit, extract:
- Repository name (folder name)
- Commit message (first line)
- Files changed (optional, for context)

**Repo to vault mapping:** Check `CLAUDE.md` → "Git Repo to Vault Mapping" table. If a repo has a mapping, group its commits under that vault project instead of a separate "Code:" section.

Skip:
- Merge commits
- Repos with no commits today

**4. Read and extract key information**

For Calendar/ notes (meetings, threads):
- Title (from filename or `aliases:`)
- `context:` or `about:` to determine grouping
- One-line summary of what happened (from content, `one-liner:`, or summary section)

For Contexts/ notes (git-tracked):
- Title (from filename or `aliases:`)
- `context:` or `parent:` to determine grouping
- One-line summary of what actually changed based on the diff (e.g., "Added success metrics section, removed MVP scope item")

For git commits:
- If repo has a vault mapping, group under that project (commits appear alongside related vault notes)
- If no mapping, use `Code: repo-name` as grouping
- Summarize related commits into coherent work items (don't list every commit separately if they're part of the same feature/fix)

**5. Generate the log**

Format:
```markdown
### Log
- [[Project/Initiative]]
	- [[YYYY-MM-DD Note Title|Short Name]] - one-line summary of what happened or changed
	- [[Another Note|Name]] - summary
	- (commits) Summary of code work (if repo maps to this project)
- [[Another Project]]
	- [[Note|Name]] - summary
- Code: unmapped-repo-name
	- Summary of work done (for repos without vault mapping)
- Other
	- Ungrouped items
```

Rules:
- Group vault notes by project/initiative/product as parent bullets
- Use full wikilinks on parent items, no aliases
- Use aliases on nested items for readability (strip date prefix, shorten long titles)
- One-line summaries: what decision was made, what changed, what was discussed
- For mapped repos, add commit summaries under the vault project (prefix with "(commits)")
- For unmapped repos, use `Code: repo-name` as parent (no wikilink)
- Synthesize multiple related commits into a single summary line when possible
- No bold formatting
- No extra whitespace between groups
- "Other" category for items that don't fit a project

**6. Update the daily note**

Replace the `### Log` section content with the generated log.

Preserve:
- Frontmatter
- Any other sections (if present)

**7. Commit Contexts/ changes**

After generating the log, commit today's Contexts/ changes to establish a clean baseline for tomorrow:
- `cd ~/Documents/My\ Vault/Contexts && git add . && git commit -m "Daily snapshot: YYYY-MM-DD"`
- This ensures tomorrow's diff only shows tomorrow's work

**8. Output**

Show the updated log section. Confirm:
- Number of Calendar/ notes processed
- Number of Contexts/ files with changes (and brief diff summary)
- Number of repos scanned, commits found

If any notes couldn't be categorized, list them and ask if grouping is correct.
