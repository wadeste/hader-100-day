# Task 008: refinement-cycle

## Workflow
strategy-research-loop

## Type
PROMPT (LLM reasoning — deepen existing research)

## Description
When all queue topics are complete, enters refinement mode to deepen existing research, add missing data, and improve strategic recommendations.

## Prompt
```
All queue items are complete. Now enter refinement mode.

1. Read `research-log.md` to review existing findings
2. Pick the FIRST topic in the queue that has `[x]`
3. Identify ONE area that could be deepened:
   - Missing data points or more recent information?
   - Competitor analysis that's thin?
   - Strategic implications that need more depth?
   - Actionable recommendations that are too vague?
   - New developments since the original research?
4. Research the gap (web search, data lookup)
5. Append updated findings to `research-log.md` with a "Refinement — {YYYY-MM-DD}" section under the original topic
6. Commit: `git add -A && git commit -m "refine: deepen {topic_title} — {what changed}"`
7. Move to the next topic on the next iteration. Keep cycling through all topics.

**Good refinements:**
- Added recent competitor pricing data
- Expanded strategic implications with financial modelling
- Turned vague recommendations into specific action items with timelines
- Incorporated new market research or regulatory changes

**Bad refinements:**
- Rephrasing existing findings without adding substance
- Adding generic platitudes ("this is important", "further research needed")
- Repeating the same analysis with slightly different wording
```

## Acceptance Criteria
- [x] Reads existing `research-log.md` to identify gaps
- [x] Picks one topic to deepen
- [x] Performs new research on the identified gap
- [x] Appends refinement to `research-log.md` with date stamp
- [x] Commits with descriptive message
- [x] Moves to next topic on subsequent iterations