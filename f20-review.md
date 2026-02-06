---
description: Prep bullets for weekly F20 Product & PM Sync
---

Generate prep notes for the weekly F20 sync meeting with Carol, Beth (Project Management), and Rick (Product).

**Cadence:** Weekly
**Audience:** Project Management and Product leadership
**Output:** Bullets to prep from (not to paste verbatim)

---

## 1. Calculate Time Window

- Find the most recent F20 sync meeting note (search Calendar/ for meetings with `about: "[[F20]]"` or title containing "F20")
- If found, use that date as the start of the window
- If not found, default to 7 days ago
- End date: today

---

## 2. Gather F20 Activity

**Documents/ changes (via git):**
```bash
cd ~/Documents/My\ Vault/Contexts && git log --since="$START_DATE" --name-only --pretty=format:"" -- "Yamaha Guitar Group/Portfolio/F20/"
```
- For each changed file, read the diff to understand what changed
- Summarize: sections added, decisions captured, specs updated

**Calendar/ notes:**
- Find meetings and threads with `about:` or `context:` linking to F20 or Yamaha
- Extract key points, decisions, action items

**Daily note mentions:**
- Search daily notes from the time window for `[[F20]]` mentions
- Extract the log entries and summaries

**Git commits (if applicable):**
- Check ~/Projects for any F20-related repos (per daily-notes.md mapping)
- Summarize code work if present

---

## 3. Generate Prep Bullets

Organize into sections:

```markdown
## F20 Sync Prep - [Date]

### Progress
- What moved forward this week
- Specs updated, decisions made, milestones hit

### Blockers
- What's stuck or waiting on others
- Dependencies, open questions

### Decisions Needed
- Items requiring PM or Product input
- Trade-offs to discuss

### Questions for the Room
- Clarifications needed from Carol, Beth, or Rick
- Scope or timeline concerns to raise
```

**Tone:** Internal prep notes. Direct, specific. Include enough context that you can speak to each point without referring back to source docs.

---

## 4. Output

Display the prep bullets directly. Do not create a new note (this is ephemeral prep, not a permanent artifact).

If no F20 activity found in the time window, say so and ask if the window should be extended.
