# Task 004: analyze

## Workflow
strategy-research-loop

## Type
PROMPT (LLM reasoning — synthesis and strategic analysis)

## Description
Synthesizes research findings into a structured analysis with executive summary, insights, implications, and recommended actions.

## Prompt
```
Synthesize the research into a structured analysis.

Read `.kairon/current-topic.md` and `.kairon/research.md`.

Write an analysis to `.kairon/analysis.md` with:
- Executive summary (2-3 sentences)
- Key insights (bulleted, prioritised by impact)
- Supporting evidence (data, quotes, references)
- Strategic implications (what this means for the business/goal)
- Recommended actions (specific, actionable, time-bound)
- Open questions for follow-up

Keep it focused on this single topic — don't scope beyond the queue item.
```

## Acceptance Criteria
- [x] `.kairon/analysis.md` written with all required sections
- [x] Executive summary is concise (2-3 sentences)
- [x] Insights are prioritised by impact
- [x] Recommended actions are specific and time-bound
