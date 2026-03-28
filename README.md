# daily-research

Automated daily research agent powered by Claude Code cloud scheduled tasks.

## How It Works

A cloud scheduled task runs every weekday and:
1. Researches current news across defined topics using direct source URLs and web search
2. Logs findings in `research-results.md` (rolling 30-day window)
3. Creates Gmail drafts — a daily summary (personal) and a weekly deep-dive (distributed)

A separate monthly task reviews source quality and recommends changes.

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

## Scheduled Tasks

- **Daily task:** Runs weekday mornings via Claude Code cloud scheduled tasks
- **Monthly task:** Runs 1st of each month via a separate cloud scheduled task

## Setup

1. Clone this repo
2. Update `distribution-list.md` with actual email addresses
3. Review and customize `topics.md` and `sources.md`
4. Create two cloud scheduled tasks at claude.ai/code/scheduled (see session descriptions in setup docs)
5. Connect Gmail MCP connector in Claude Code settings
