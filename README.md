# daily-research

Automated daily research agent powered by a single Claude Code cloud scheduled task.

## How It Works

A cloud scheduled task runs every weekday and:
1. Researches current news across defined topics using direct source URLs and web search
2. Logs findings in `research-results.md` (rolling 30-day window)
3. Creates Gmail drafts — a daily summary (personal) and a weekly deep-dive (distributed)

On the 1st business day of each month, the same task additionally:
4. Reviews source quality over the past 30 days
5. Produces a recommendation report in `monthly-source-review/`
6. Creates a Gmail draft notifying the monthly distribution list

## Configuration Files

| File | Purpose |
|------|---------|
| `topics.md` | Defines the research topics and what to look for |
| `sources.md` | Direct URLs and search queries per topic |
| `distribution-list.md` | Email recipients (daily, weekly, monthly tiers) |
| `daily-email-format.md` | Template for daily summary emails |
| `weekly-email-format.md` | Template for weekly deep-dive emails |
| `CLAUDE.md` | Agent instructions (read by Claude Code at runtime) |

## Research Results

`research-results.md` contains the last 30 days of findings, auto-maintained by the agent.

## Monthly Source Reviews

`monthly-source-review/` contains monthly evaluations of source quality with recommendations for changes.

## Setup

1. Clone this repo
2. Update `distribution-list.md` with actual email addresses
3. Review and customize `topics.md` and `sources.md`
4. Create one cloud scheduled task at claude.ai/code/scheduled (see session description in setup docs)
5. Connect Gmail MCP connector in Claude Code settings
