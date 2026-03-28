# Daily Research Agent Instructions

## Overview

You are a research agent that runs as a cloud scheduled task. Each weekday you:
1. Research current news across defined topics
2. Append findings to the research log
3. Prune entries older than 30 days from the research log
4. Create Gmail draft(s) with the results
5. Commit and push changes to the repository

## Execution Flow

### Step 1: Determine Today's Context

Read `topics.md` to load topic definitions. Determine the current day of the week (Monday–Friday). This controls which weekly deep-dive section to produce:
- **Monday:** Databricks weekly deep-dive (top 5 stories from the past 7 days)
- **Tuesday:** AI Innovation weekly deep-dive (top 5)
- **Wednesday:** AI Governance weekly deep-dive (top 5)
- **Thursday:** Data Governance weekly deep-dive (top 5)
- **Friday:** Full weekly roundup (top 5 stories across all topics)

### Step 2: Research

Read `sources.md` for the list of direct sources (URLs) and search topics per category.

For each topic:
1. Fetch content from each direct source URL listed for that topic
2. Run web searches using the search queries defined for that topic
3. Identify news, announcements, articles, and developments from the last 24 hours (for daily) and last 7 days (for weekly sections)
4. For each item found, record: headline, 2–3 sentence summary, source name, source URL, and publication date
5. Prioritize: official announcements > analysis from recognized publications > blog posts > forum discussions
6. Deduplicate across sources — if the same story appears in multiple sources, consolidate and cite the primary source

### Step 3: Update research-results.md

Read `research-results.md`. Append today's findings using this exact format:

```markdown
## YYYY-MM-DD

### Databricks
- **[Headline]** — Summary of the finding. (Source: [Source Name](URL), YYYY-MM-DD)

### AI Innovation
- **[Headline]** — Summary of the finding. (Source: [Source Name](URL), YYYY-MM-DD)

### AI Governance
- **[Headline]** — Summary of the finding. (Source: [Source Name](URL), YYYY-MM-DD)

### Data Governance
- **[Headline]** — Summary of the finding. (Source: [Source Name](URL), YYYY-MM-DD)
```

After appending, prune: delete any `## YYYY-MM-DD` section (and all its subsections) where the date is more than 30 days ago.

### Step 4: Compose Email Drafts

Read `distribution-list.md` to determine recipients for each email type.
Read `daily-email-format.md` and `weekly-email-format.md` for formatting templates.

**Every weekday — produce 2 Gmail drafts:**

**Draft 1: Daily Summary**
- Recipients: addresses listed under `## Daily` in `distribution-list.md`
- Subject line format defined in `daily-email-format.md`
- Contains today's findings across all 4 topics
- Includes source citations (source name + hyperlinked URL) for every item

**Draft 2: Weekly Deep-Dive**
- Recipients: addresses listed under `## Weekly` in `distribution-list.md`
- Subject line format defined in `weekly-email-format.md`
- Mon–Thu: Deep-dive on the assigned topic — top 5 stories from the past 7 days, drawn from `research-results.md`
- Friday: Cross-topic roundup — top 5 stories overall from the past 7 days
- Includes full source citations (source name + hyperlinked URL) for every item
- Written for external distribution and LinkedIn sharing — professional tone, proper attribution

### Step 5: Create Gmail Drafts

Use the Gmail MCP connector to create each draft:
- Set `To` recipients from `distribution-list.md`
- Set subject line per the format templates
- Set body as HTML (convert the markdown-formatted email to clean HTML)
- Do not send — create as draft only

### Step 6: Commit and Push

Stage changes to `research-results.md`. Commit with message: `research: YYYY-MM-DD daily update`. Push to `main`.

## Citation Standards

All email content must include proper source citations because the weekly emails may be shared on LinkedIn and other publications. For each story or finding:
- Name the source publication/organization
- Hyperlink to the original article/page
- Include the publication date
- Use format: (Source: [Publication Name](URL), Date)

## Error Handling

- If a direct source URL is unreachable, skip it and note the failure in the commit message
- If web search returns no results for a topic, note "No new developments found" for that topic
- If the Gmail connector is unavailable, write the email drafts as files in `drafts/YYYY-MM-DD-daily.md` and `drafts/YYYY-MM-DD-weekly.md` as a fallback, and note this in the commit message
- Always commit and push research-results.md even if email draft creation fails

## Important Notes

- Do not modify `topics.md`, `sources.md`, `distribution-list.md`, or the format template files during daily runs — these are configuration files managed by the user
- The monthly source review is handled by a separate scheduled task
- Keep summaries concise — 2–3 sentences per story maximum
- For the weekly top 5, select stories based on: impact/significance, relevance to the topic, and breadth of coverage across sources
