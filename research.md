---
description: Deep research with web search, capture findings to vault
---

Research mode - investigate a topic and capture findings:

**Workflow:**

1. **Clarify scope** (if needed) - brief question to confirm research direction
2. **Search vault first** - check if related content exists in Documents/ or Portfolio/
3. **Deep research** using WebSearch:
   - Search multiple angles
   - Find key insights, patterns, data
   - Identify credible sources
4. **Present findings** to user:
   - Key insights (bullets, not essays)
   - Trade-offs or considerations
   - Sources
5. **Offer to capture** - ask if user wants findings saved to vault

**If capturing to vault:**
- Determine appropriate location based on context (Yamaha, APM, Personal)
- Use Document type with proper frontmatter
- Place in parent item's Documents/ folder per portfolio structure
- Link to related notes

**Style:**
- Concise synthesis, not exhaustive reports
- Surface trade-offs explicitly
- Recommend, then rationale
- Use wikilinks to connect to existing vault notes where relevant

---

## Competitive Intel Mode (Trade Shows)

**Trigger:** Research query mentions trade show, competitor products, or product launches (e.g., "NAMM 2026 pedals", "Musikmesse guitar amps")

**Workflow:**

1. **Search trade publications:**
   - Guitar World, MusicRadar, Premier Guitar, Reverb News, Guitar.com
   - Manufacturer press releases

2. **Search community discussions:**
   - Reddit: r/guitarpedals, r/Guitar, r/GuitarAmps, r/Bass, r/offset
   - The Gear Page, other forums mentioned in results

3. **For each product found:**
   - Extract: manufacturer, product name, key specs, price, availability
   - Write a summary (synthesize, don't copy-paste)
   - Capture community sentiment from discussions

4. **Rate sentiment** using the rubric below

5. **Output structure:**
   - Individual product notes to segment folders
   - Update index note with all findings

**Segments (Yamaha Guitar Group):**

| Segment | Owner | Keywords |
|---------|-------|----------|
| Single-Effect Pedals | You | stompbox, pedal, drive, delay, reverb, fuzz |
| Multi-Effects & Modelers | Eric Klein | multi-fx, floor processor, modeler, pedalboard |
| Digital Guitar Amps | Rick Gagliano | modeling amp, digital amp, combo amp |
| Bass Amplification | Dom Liberati | bass amp, bass cabinet, bass head, bass effects |
| Guitars | Nick (Guild/Córdoba) | electric guitar, acoustic guitar, classical guitar |

**Sentiment Rating Rubric:**

Sentiment measures aggregated community/press reception, not objective product quality. A 4/5 means "people are excited about this," not "this is objectively good."

| Rating | Label | Definition |
|--------|-------|------------|
| 5/5 | Exceptional | Universal praise; "must-have" consensus; no meaningful concerns |
| 4.5/5 | Very Positive | Strong enthusiasm; minor concerns don't dampen reception |
| 4/5 | Positive | Generally well-received; some valid concerns raised |
| 3.5/5 | Mixed-Positive | More praise than criticism, but notable reservations |
| 3/5 | Mixed | Divided reception; significant praise AND concerns |
| 2.5/5 | Mixed-Negative | More criticism than praise; potential not realized |
| 2/5 | Negative | Predominantly critical; few defenders |
| 1.5/5 | Very Negative | Strong backlash; widespread disappointment |
| 1/5 | Hostile | Active rejection; brand damage territory |

**Sources considered:** Trade publication tone, forum discussion sentiment, Reddit threads, review scores where available.

**Output locations:**
```
Contexts/Yamaha Guitar Group/[Event] Intel/
├── [Event] Competitive Intel.md     (index)
├── Single-Effect Pedals/
├── Multi-Effects & Modelers/
├── Digital Guitar Amps/
├── Bass Amplification/
└── Guitars/
```

**Product note format:**
```markdown
---
type: Document
document-type: Research
context: "[[Yamaha Guitar Group]]"
segment: [segment-slug]
product: "[Product Name]"
manufacturer: "[Manufacturer]"
price: "[Price if known]"
availability: "[Availability if known]"
first-seen: [YYYY-MM-DD]
last-updated: [YYYY-MM-DD]
---

## Summary
[2-3 sentence synthesis of what this product is and why it matters - updated in place on refresh]

## Key Specs
- [Bullet list of notable specifications - updated in place if specs change]

## Competitive Relevance
[Analysis of impact on Yamaha Guitar Group - updated in place as market context evolves]

## Sources
- [Source Name](url) - [brief description]
[New sources appended on update]

## Sentiment

**Current ([YYYY-MM-DD]):** [Label] ([X]/5)
- **Praise:** [What people like]
- **Concerns:** [What worries them]

> [!info] Rating Key
> 5=Exceptional, 4.5=Very Positive, 4=Positive, 3.5=Mixed-Positive, 3=Mixed, 2.5=Mixed-Negative, 2=Negative, 1.5=Very Negative, 1=Hostile. Measures community/press reception, not objective quality.

### Sentiment History
| Date | Rating | Trend | Driver |
|------|--------|-------|--------|
| [YYYY-MM-DD] | [X]/5 | -- | [Initial/update reason] |

---

## Updates

[Reverse-chronological entries added during update mode]
```

**Index note format:**
```markdown
---
type: Document
document-type: Research
context: "[[Yamaha Guitar Group]]"
event: "[Event Name]"
date-range: "[Start] - [End]"
monitor-start: [YYYY-MM-DD]
monitor-end: [YYYY-MM-DD]
monitor-status: [active/complete]
---

## Overview
[Brief summary of event significance and key themes]

## Monitor Status

| Setting | Value |
|---------|-------|
| Event Dates | [Start] - [End] |
| Monitor Window | [monitor-start] - [monitor-end] |
| Status | [Active/Complete] |
| Last Run | [YYYY-MM-DD] |

### Run History
| Date | Products Updated | Notes |
|------|------------------|-------|
| [YYYY-MM-DD] | [N] | [Brief note] |

## By Segment

### Single-Effect Pedals
| Product | Manufacturer | Price | Relevance |
|---------|--------------|-------|-----------|
| [[Product Name]] | Mfr | $X | [Why it matters to YGG] |

### Multi-Effects & Modelers
...

### Digital Guitar Amps
...

### Bass Amplification
...

### Guitars
...

## Key Trends
- [Trend 1]
- [Trend 2]

## Competitive Implications
[What this means for Yamaha Guitar Group products]
```

---

## Update Mode (Monitoring)

**Trigger:** `/research [event] updates` (e.g., "NAMM 2026 updates")

**Purpose:** Refresh existing competitive intel notes with new coverage, track sentiment evolution.

**Workflow:**

1. **Locate index note** at `[Event] Intel/[Event] Competitive Intel.md`
   - Verify `monitor-status: active` and within `monitor-end` window
   - If past window, prompt to run summary mode instead

2. **Search trade publications** for new coverage:
   - Guitar World, MusicRadar, Premier Guitar, Reverb News, Guitar.com
   - Look for hands-on reviews, NAMM floor impressions, new announcements

3. **Search community forums for sentiment** (required):
   - **The Gear Page (thegearpage.net):**
     - Use `mcp__tgp-scraper__search_tgp` to find threads (may return empty if login required)
     - Use WebSearch with `site:thegearpage.net "[product name]"` to find thread URLs
     - Use `mcp__tgp-scraper__fetch_tgp_thread` with thread URL to get full posts
     - Extract: specific quotes with usernames, like counts, praise points, concerns
   - The Gear Forum (thegearforum.com) - often more accessible for fetching via WebFetch
   - Reddit: r/guitarpedals, r/Guitar, r/GuitarAmps, r/Line6Helix (note: WebFetch blocked, use WebSearch for indexed content)
   - Extract: specific quotes, praise points, concerns, overall vibe
   - Note if forum content is blocked/inaccessible

4. **For each product note in the intel folder:**
   - Search for recent coverage (news articles, forum discussions, reviews)
   - Compare against existing content
   - Skip if no new information found

5. **When new information found:**
   - Update Summary/Key Specs/Competitive Relevance sections in place
   - Append new sources to Sources section (include forum thread links even if content blocked)
   - Update sentiment with new date, incorporating forum feedback
   - Add row to Sentiment History table with trend indicator (↑/↓/--)
   - Add entry to `## Updates` section with:
     ```markdown
     ### [YYYY-MM-DD]
     **Source:** [Where new info came from - include forum names]
     **Changes:** [What was updated]

     **Forum sentiment:** [Summary of community reaction with specific quotes]
     **Sentiment shift:** [X/5 → Y/5] ([reason]) or "No change"
     ```
   - For TGP updates specifically, use this format:
     ```markdown
     ### [YYYY-MM-DD] (TGP Update)
     **Source:** The Gear Page ([N] posts)
     **Changes:** [What was learned]

     **TGP Forum Quotes:**
     - "[Quote]" ([username], [N] likes)
     - "[Quote]" ([username])

     **TGP Sentiment:** [Summary of TGP-specific reaction]
     **Sentiment shift:** [X/5 → Y/5] [reason] or "No change"
     ```

6. **Update index note:**
   - Update `Last Run` date
   - Add row to Run History table
   - Update any changed prices/relevance in segment tables

**Output:** Report summary including:
- Products updated (count and names)
- Sentiment shifts (table format: Product | Before | After | Driver)
- Key forum quotes (verbatim where possible)
- Note any forums that were inaccessible (TGP often blocks fetches)

---

## Summary Mode (Final Deliverable)

**Trigger:** `/research [event] summary` (e.g., "NAMM 2026 summary")

**Purpose:** Generate executive summary synthesizing all monitored intelligence for product team.

**Workflow:**

1. **Read all product notes** in the intel folder
2. **Analyze sentiment trajectories** from Sentiment History tables
3. **Identify patterns:**
   - Products with rising/falling sentiment
   - Pricing trends by segment
   - Emerging competitive threats
4. **Generate executive summary note**

**Executive summary format:**
```markdown
---
type: Document
document-type: Research
document-status: Final
context: "[[Yamaha Guitar Group]]"
parent: "[[{Event} Competitive Intel]]"
---

## {Event} Competitive Intelligence Summary

**Monitoring Period:** [monitor-start] - [monitor-end]
**Products Tracked:** [N]

## Executive Highlights

### Immediate Threats
1. **[Product]** ($[price]) - [brief threat description]
   - Sentiment trajectory: [X/5 → Y/5] ([Rising/Falling/Stable])
   - Implication: [specific recommendation]

### Emerging Opportunities
[Products that stumbled, market gaps identified]

### Key Trends
[Synthesized from monitoring period]

## Sentiment Summary

| Product | Launch | Final | Trajectory |
|---------|--------|-------|------------|
| [Product] | X/5 | Y/5 | ↑/↓/-- |

## Recommendations by Product Line

### Line 6 / HX
[Specific actions based on multi-fx/modeler findings]

### THR / Modeling Amps
[Specific actions based on digital amp findings]

### Guild / Córdoba
[Specific actions based on guitar findings]

### Ampeg / Bass
[Specific actions based on bass findings]
```

5. **Update index note:**
   - Set `monitor-status: complete`
   - Add final row to Run History

**Output:** Path to generated summary note, key highlights verbally reported.
