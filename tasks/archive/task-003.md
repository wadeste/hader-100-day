# Task 003: research

## Workflow
strategy-research-loop

## Type
PROMPT (LLM reasoning — web search, data gathering, analysis)

## Description
Researches the selected topic using web search, existing project files, and known context. Writes findings to `.kairon/research.md`.

## Prompt
```
Read `.kairon/current-topic.md` and research the topic.

1. Review any existing context files in the work directory (plans, briefs, data files)
2. Search the web for current data, market insights, competitor information, or relevant research
3. Cross-reference with known context from the vault or project files
4. Identify gaps, risks, opportunities, and actionable insights

Write findings to `.kairon/research.md` with:
- Key findings (with sources/URLs)
- Data points or metrics discovered
- Gaps or unanswered questions
- Risks and opportunities identified
- Initial recommendations or next steps
```

## Acceptance Criteria
- [x] Web research performed for the topic
- [x] Existing context reviewed
- [x] `.kairon/research.md` written with findings, data, gaps, risks, opportunities
- [x] Sources documented with URLs
