---
description: Generate weekly status update for all projects in a context
---

Generate a status update for projects within a context.

**Input:** $ARGUMENTS
- Required: Context name (Yamaha / APM)
- Optional: Time window (default: 1 week)
- Examples: "Yamaha", "APM 2 weeks", "Yamaha Guitar Group past month"

**Workflow:**

1. **Parse arguments:**
   - Extract context (Yamaha Guitar Group or APM Music)
   - Extract time window if specified, otherwise default to 1 week
   - Calculate date range

2. **Find all projects in context:**
   - Yamaha: Products/Platforms in Portfolio folder
   - APM: Initiatives in Portfolio folder

3. **For each project, gather activity from the time window:**
   - Calendar entries (meetings, working sessions) with `about:` linking to project
   - Daily notes mentioning the project
   - Recently modified Documents in project folder
   - Work item status changes (completed, started, blocked)

4. **Ask user format preference:**
   - Bullets or paragraph? (Note: APM typically prefers paragraphs, Yamaha prefers bullets)

5. **Generate status update per project:**
   - Focus on: decisions made, progress, blockers, next steps
   - Keep concise: 2-4 bullets OR 2-3 sentences per project
   - Skip projects with no activity in the time window
   - Output directly to terminal for user to copy/paste

**Output style:**
- Tighter is better — short sentences, just the facts
- Status-focused: what shipped, what's in progress, what's blocked
- No narrative or exposition — details live in project notes
- Split distinct features even if they ship together
- Use "post-launch refinements identified" instead of listing them
- Skip background work, infrastructure issues, or items on hold unless user asks
- APM prefers paragraphs; Yamaha prefers bullets

**Example (APM paragraph style):**
> **Waveform Highlighting:** Feature complete and deployed to lower environment, with release scheduled for 12/11. Steering committee identified post-launch refinements.
>
> **Segment Seed:** Feature complete and deployed to lower environment, with release scheduled for 12/11. Product eval confirmed implementation matches spec. Demo with steering committee and music team revealed post-launch refinements.
>
> **Ignore Vocals & Prioritize BPM:** Search API work is complete, waiting on final design comps. Will review with stakeholders next week.
