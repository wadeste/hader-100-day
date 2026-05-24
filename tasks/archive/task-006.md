# Task 006: mark-complete

## Workflow
strategy-research-loop

## Type
PROMPT (LLM reasoning — update queue state)

## Description
Marks the completed research topic as done in `tasks/queue.md` so the loop can advance to the next topic.

## Prompt
```
Mark the completed topic as done in `tasks/queue.md`.

1. Read `.kairon/current-topic.md` to get the topic title
2. Find that exact line in `tasks/queue.md` (the `- [ ] {title}` line)
3. Change it to `- [x] {title} — researched {YYYY-MM-DD}`
4. Commit the queue update: `git add tasks/queue.md && git commit -m "chore: complete research topic: {title}"`

This is CRITICAL — the next iteration needs to see this topic as completed so it can move to the next one.
```

## Acceptance Criteria
- [x] Queue item changed from `[ ]` to `[x]`
- [x] Date stamp added to completed item
- [x] Queue committed with descriptive message
