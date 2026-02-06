# Product Sentiment Tracker

Scrape The Gear Page and Reddit for community sentiment around a Line 6 product.

## Arguments

- `$PRODUCT` - Product name to search for (e.g., "HX One", "Helix", "POD Go")

## Instructions

You are gathering market intelligence for a Line 6 product. This data informs firmware updates, manufacturing changes, and future product decisions.

### Step 1: Gather Data

**The Gear Page:**
Use the `mcp__tgp-scraper__search_tgp` tool to search for threads about $PRODUCT. Then use `mcp__tgp-scraper__fetch_tgp_thread` to get full content from the most relevant threads (up to 5 threads, 3 pages each).

Search queries to try:
- "$PRODUCT"
- "Line 6 $PRODUCT"
- "$PRODUCT review"
- "$PRODUCT problems"
- "$PRODUCT vs" (for competitive comparisons)

**Reddit:**
Use WebSearch to find Reddit discussions. Search queries:
- "site:reddit.com $PRODUCT"
- "site:reddit.com Line 6 $PRODUCT review"
- "site:reddit.com $PRODUCT issues"
- "site:reddit.com $PRODUCT vs Strymon"
- "site:reddit.com $PRODUCT vs Boss"

For promising results, use WebFetch to get thread content.

### Step 2: Analyze and Categorize

Organize findings into these categories:

1. **Overall Reception** - General sentiment (positive/negative/mixed), common praise, first impressions
2. **Pain Points & Bugs** - Reported issues, firmware bugs, hardware problems, usability complaints
3. **Feature Requests** - What users want added or changed
4. **Competitive Comparisons** - How users compare to Strymon, Boss, Eventide, etc. What they chose and why

### Step 3: Update the Sentiment Document

Check if a sentiment document already exists at:
`Contexts/Yamaha Guitar Group/Portfolio/$PRODUCT/Documents/$PRODUCT Sentiment Tracker.md`

**If it exists:** Read it first. Add new findings under a dated section (## YYYY-MM-DD Update). Preserve all previous content. Update the summary sections only if sentiment has materially shifted.

**If it doesn't exist:** Create it with this structure:

```markdown
---
type: Document
document-type: Research
document-status: Living
context: "[[Yamaha Guitar Group]]"
parent: "[[$PRODUCT]]"
created: {today's date}
modified: {today's date}
---

## Summary

{2-3 sentence executive summary of overall sentiment}

## Overall Reception

{Synthesized view of community sentiment}

## Pain Points & Bugs

| Issue | Frequency | Source | Actionable? |
|-------|-----------|--------|-------------|
| ... | ... | ... | ... |

## Feature Requests

| Request | Frequency | Source | Feasibility Notes |
|---------|-----------|--------|-------------------|
| ... | ... | ... | ... |

## Competitive Comparisons

{How the product stacks up against competitors in user discussions}

---

## Research Log

### {today's date} - Initial Scan

**Sources searched:**

| Source | Thread | URL |
|--------|--------|-----|
| TGP | {thread title} | {full URL} |
| Reddit | {thread title} | {full URL} |
| ... | ... | ... |

**Key findings this session:**
{bullet points of notable discoveries}
```

**IMPORTANT:** Always include clickable URLs in the Research Log table so the user can review source threads directly. The scrapers return URLs for every result - capture them.

### Step 4: Report Back

After updating the document, provide a brief summary to the user:
- Total sources reviewed
- Key themes identified
- Any urgent issues that need attention
- Suggested next steps (firmware fix? FAQ update? competitive response?)
