---
description: Draft reply to a Thread note
---

**Input (one of the following):**
- Thread note path or wikilink (e.g., `[[2026-01-15 Project status update]]`)
- If invoked immediately after `/save-thread`, use the thread from conversation context
- If no input provided, ask which thread to reply to

**1. Load the thread**

If given a path or wikilink:
- Read the thread note from Calendar folder
- Parse the Thread section to understand the conversation

If using conversation context:
- Use the thread content already discussed in this session

**2. Analyze the thread**

Identify:
- Who sent the last message
- Open questions or requests requiring response
- Action items assigned to [[Anthony Taglianetti]]
- Decisions that need to be communicated
- Tone and formality level of the conversation

**3. Generate the draft**

Create a reply that:
- Matches the tone and formality of the thread
- Addresses all open questions or action items
- Uses bracketed placeholders for decisions you need to make (e.g., `[specific date TBD]`, `[confirm with engineering first]`)
- Is complete enough to send with light editing

**4. Add draft to the thread note**

Append the draft at the bottom of the Thread section:
```
---
**[[Anthony Taglianetti]] - DRAFT**

[draft content here]
```

**5. Iterate with the user**

Present the draft and ask for feedback. Continue refining until the user is satisfied.

**6. Copy final reply to clipboard**

When the user approves the draft:
- Copy to clipboard as **plain text**
- Strip markdown formatting (remove `**` bold markers, wikilinks, etc.)
- Convert wikilinks to plain names: `[[John Smith]]` becomes `John Smith`
- Use regular hyphens, not en-dashes
- Use this command pattern:
  ```bash
  cat << 'EOF' | pbcopy
  plain text content here
  EOF
  ```

**7. Update the thread note**

After the user confirms they've sent the reply:
- Update the DRAFT header with actual date/time: `**[[Anthony Taglianetti]] - [[YYYY-MM-DD|M/D/YYYY]] h:mm AM/PM**`
- Save the updated note
