---
description: Re-onboarding interview to refresh Claude rules and context. Dictation-friendly.
---

Conversational interview to update your Claude rules. Designed for dictation (natural speech).

**1. Read current state**

Read these files to understand what's already documented:
- `Resources/Meta/Claude/rules/core/user-profile.md`
- `Resources/Meta/Claude/rules/core/memory.md`
- `Resources/Meta/Claude/rules/yamaha/context.md`
- `Resources/Meta/Claude/rules/yamaha/collaborators.md`
- `Resources/Meta/Claude/rules/yamaha/portfolio.md`
- `Resources/Meta/Claude/rules/apm/context.md`
- `Resources/Meta/Claude/rules/apm/collaborators.md`

**2. Area selection**

Use AskUserQuestion with multiSelect to ask which areas need refreshing:

| Option | Label | Description |
|--------|-------|-------------|
| 1 | How we work together | Communication style, output preferences, pacing |
| 2 | Current priorities | What you're focused on, blockers, active work |
| 3 | Yamaha context | Team, products, org dynamics, schedule pressure |
| 4 | APM context | Team, search, org dynamics, CEO navigation |
| 5 | Career & goals | Professional direction, recognition, skills building |

**3. Interview loop**

For each selected area, conduct a brief conversational interview:

| Area | Files to Update | Interview Prompt |
|------|-----------------|------------------|
| How we work together | `user-profile.md` | "How has your working style evolved? Any changes to pacing, depth, or how you want me to push back?" |
| Current priorities | `memory.md` | "What's top of mind right now? What are you actively working on, and what's blocking you?" |
| Yamaha context | `yamaha/context.md`, `yamaha/collaborators.md`, `yamaha/portfolio.md` | "Any changes at Yamaha? Team shifts, product updates, schedule pressure situations? How's the promotion track going?" |
| APM context | `apm/context.md`, `apm/collaborators.md` | "How's the APM landscape? Any shifts in the search team, your positioning, or how you're navigating leadership?" |
| Career & goals | Both context files, `user-profile.md` | "What's evolved in your career goals? New skills you're building, recognition you're working toward, or shifts in direction?" |

For each area:
1. State what's currently documented (brief summary)
2. Ask the interview question
3. Wait for response (expect dictation: run-on sentences, filler words, stream of consciousness)
4. If they gave a short answer, ask one follow-up to go deeper
5. When done with an area, summarize what you heard before moving to the next

**4. Process dictation**

Clean up their responses:
- Remove filler words (um, uh, like, you know)
- Fix obvious speech-to-text errors
- Preserve their voice and meaning
- Extract concrete updates (people, roles, priorities, preferences)

**5. Confirm before saving**

Present a summary of all proposed changes across all areas:
"Here's what I'll update:

**[Area 1]:**
- [bullet points of changes]

**[Area 2]:**
- [bullet points of changes]

Does this capture it, or should I adjust anything?"

Wait for confirmation. Handle:
- "yes" / "that's right" / "looks good" → proceed to save
- Corrections → incorporate and re-confirm
- "add [X]" → include additional point

**6. Apply updates**

Edit each relevant file:
- Preserve existing structure and sections
- Update only the specific sections that changed
- For memory.md: also update "Last Session" with today's date and "Refreshed context via /refresh"
- Update "Last updated" timestamp in memory.md

**7. Summarize what changed**

Show a brief summary:
"Updated:
- `user-profile.md`: [what changed]
- `memory.md`: [what changed]
- ..."

---

## Dictation tips (for user)
- Speak naturally, Claude will clean up transcription
- Use numbers for selections ("one and three")
- "That's right" / "add that" / "change that" for confirmations
- One area at a time, as deep as you want to go
