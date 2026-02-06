---
description: Save email/Slack/Teams thread as Thread note
modified: 2026-01-15T23:03:04-08:00
---

**Input:**
- If thread content is pasted below, use that
- If no content provided, read from clipboard using `pbpaste`

Format this thread as an Obsidian "Thread" note using the frontmatter structure defined in `Resources/Templates/Thread.md`. Ensure all properties match the expected field types from that template.

**1. People → `with` property**
- Extract all people mentioned in the thread and convert them to Obsidian wikilinks.
- Use proper list formatting:
  ```yaml
  with:
    - "[[Person Name]]"
    - "[[Person Name]]"
  ```

**2. Context → `context` property**
- Set `context` to either `[[APM Music]]` or `[[Yamaha Guitar Group]]`, based on the thread content.

**3. Related projects → `about` property**
- Identify related projects or products mentioned in the thread.
- Only add items that exist as notes in the vault.
- Use proper list formatting:
  ```yaml
  about:
    - "[[Product Name]]"
    - "[[Product Name]]"
  ```
- If there are no valid related projects, leave the `about` property empty.

**4. One-liner**
- Write a concise one-line summary of the thread (maximum one sentence).
- Store it in the `one-liner:` frontmatter field.

**5. Body content formatting**

After the frontmatter, format the note body as follows:

- **Summary:** Write a 2-3 sentence summary of the thread.
  - Project references MUST use this format: `[[Full Note Name|Short Alias]]`
    - ✅ CORRECT: `[[Stompbox FX|F20]]`
    - ❌ WRONG: `F20 ([[Stompbox FX]])`
    - ❌ WRONG: `[[Stompbox FX]]`
  - Use the same reference format consistently throughout the entire note body

- **Key Points:** section (only if applicable)
  - Include decisions, action items, and important context as bullet points.

- **Thread:** section
  - Order messages **chronologically (oldest first)**
  - For each message in the thread:
    - Add a header in this format:
      `**[[Person Name]] – [[YYYY-MM-DD|M/D/YYYY]] h:mm AM/PM**`
    - Clean up formatting for readability.
    - Remove signatures, email footers, and boilerplate.
  - Separate each message block with a line containing only: `---`
  - **User identification:** The user is [[Anthony Taglianetti]]. When the user adds their own response to the thread, use this name.

**6. Title, filename, and aliases**
- Create a descriptive title for the note based on the thread content.
- The filename format must be: `YYYY-MM-DD Descriptive title`
- Add this same descriptive title to the `aliases:` property in the frontmatter.
- Use proper list formatting:
  ```yaml
  aliases:
    - Descriptive title
  ```

**7. Update person notes from signatures**

Before formatting, check email signatures for useful metadata. Only update person notes when:
- The person note exists AND
- The target field is currently empty AND
- The signature contains clear, unambiguous information

Fields to extract (strict list):
- `title:` - Job title only (e.g., "VP of Engineering", "Product Manager")
- `company:` - Organization name
- `email:` - Work email address

Never extract:
- Phone numbers, addresses, social links
- Marketing taglines, legal disclaimers
- Generic company descriptions
- Anything requiring interpretation

Process:
1. Check if `[[Person Name]].md` exists in the vault
2. If yes, read the note and check if `title:`, `company:`, or `email:` are empty
3. If empty fields exist and signature has clear data, update the frontmatter
4. Do not ask for confirmation, just update silently

**8. Save the note**
- Save the formatted Thread note to the Calendar folder.
- Do NOT add to daily note's Log section (the `/daily-note` command gathers all work at end of day).

**Output:**
- Return the complete Obsidian note, including frontmatter and body content, ready to be saved.
- After showing the note, ask the user to review it and whether they want to save it to Calendar.

**9. Copy reply to clipboard (when user drafts a response)**
- When the user drafts a reply to add to the thread, copy it to their clipboard as **plain text**
- Strip markdown formatting (remove `**` bold markers, etc.)
- Use en-dashes sparingly; prefer regular hyphens for compatibility
- Use this command pattern:
  ```bash
  cat << 'EOF' | pbcopy
  plain text content here
  EOF
  ```

**Rules:**
- ALL person names → `[[First Last]]` wikilinks
- Extract names from emails: john.smith@company.com → [[John Smith]]
- Separate messages with `---`
