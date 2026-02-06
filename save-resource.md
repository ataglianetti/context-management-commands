---
description: Process article/video into summarized note with key insights
---

Process a resource (article, video, PDF) into a vault note:

**Input:** URL or file path to resource

**Workflow:**

1. **Fetch and analyze** the resource:
   - For URLs: use WebFetch to retrieve content
   - For files: Read the file directly
   - Identify: title, author, date, source type

2. **Search vault** for related content:
   - Check if resource already captured
   - Find related Documents, Portfolio items, or people
   - Identify which context this belongs to (Yamaha, APM, Personal/Career)

3. **Extract key insights:**
   - Core argument/thesis (1-2 sentences)
   - Key takeaways (3-5 bullets max)
   - Actionable implications for user's work
   - Notable quotes (1-2 max, only if valuable)

4. **Ask user** where to save:
   - Suggest location based on content (e.g., Career/Professional Development for PM articles)
   - Confirm before creating

5. **Create Document note** with frontmatter:
   ```yaml
   type: Document
   document-type: Research
   document-status: Final
   context: "[[Context]]"
   parent: (if applicable)
   source-url: (original URL)
   source-author: (if known)
   source-date: (if known)
   ```

**Style:**
- Dense summarization - insights, not regurgitation
- Focus on what's actionable for user's PM work
- Link to related vault notes where relevant
- No fluff - capture essence only
