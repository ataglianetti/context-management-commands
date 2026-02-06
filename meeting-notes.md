---
description: Format rough meeting notes into structured meeting note
---

Format rough meeting notes into a structured meeting note, leveraging vault context for accurate linking and interpretation.

**Input:** File path to existing meeting note with frontmatter and rough bullets/outline

## 1. Read & Validate

Read the file at `$ARGUMENTS`. Check frontmatter for required fields:
- `context:` → organizational context
- `with:` → attendees
- `about:` → product/project being discussed

**Ask only if critical fields are empty:**
- Who attended? (if `with:` empty)
- Which context? (if `context:` empty)
- Main subject? (if `about:` empty and unclear from content)

## 2. Gather Context

Per document-traversal, follow frontmatter links to build working context:

- **`about:` notes** → Read each linked note for aliases, sub-items, current state
- **`series:` note** → If present, read for recurring meeting context (typical attendees, standing topics)
- **Recent meetings** → Check 2-3 recent meetings in same series or overlapping `about:` topics for continuing discussions
- **Recent daily notes** → Scan last few days for related activity

This context informs: interpreting shorthand, linking to prior discussions, identifying entities that appear in the raw notes.

## 3. Entity Search

Before formatting, search the vault for every notable entity in the raw notes. Per wikilink discipline: search then link, no orphan wikilinks, and no duplicating frontmatter links in body text.

Only wikilink entities in the body that frontmatter doesn't already capture:

- **People not in `with:`** → Someone mentioned in discussion who wasn't an attendee. Search vault, link as `[[Full Name]]`
- **Products/projects not in `about:`** → A related product that came up but isn't the meeting's main subject. Search aliases, link as `[[Note Name|Code]]`
- **Prior discussions** → Where a topic carries over from a previous meeting, link to that meeting

## 4. Format

Preserve existing frontmatter. Fill gaps:
- Add `one-liner:` if empty (brief meeting purpose)
- Update `about:` if content reveals more specific topics:
	- For series meetings, keep the general topic for continuity
	- Add specific topics discussed, but only if notes exist in the vault

Replace raw content with structured output:

```markdown
## Summary
[2-3 sentences: key themes and outcomes]

**Topic A**
- Key point
	- Detail or sub-point

**Topic B**
- Key point

## Action Items
- Task I committed to
- Another task I committed to
```

## 5. Formatting Rules

**Structure:**
- `## Summary` and `## Action Items` are the only H2 headings
- Topic sections use `**bold text**`, not `##` headings
- Collapse over-categorized headings from transcription tools (Granola, etc.) into fewer, tighter groupings

**Action items:**
- Signaled by checkboxes (`- [ ]`) in raw notes
- Only extract items where the user committed to doing something
- Other people's work/next steps stay in relevant topic sections
- Convert checkboxes to plain bullets in final Action Items section
- If no checkboxes in raw notes, omit Action Items section entirely

**Content:**
- Use frontmatter context to interpret ambiguous bullets
- Keep bullets concise
- Group related points under clear topic sections
- Preserve all existing frontmatter fields
