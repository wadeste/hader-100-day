# Task 002: select-next-topic

## Workflow
strategy-research-loop

## Type
PROMPT (LLM reasoning — read context, write output)

## Description
Reads `tasks/queue.md` and selects the first unchecked research topic. Writes the selected topic to `.kairon/current-topic.md` for downstream tasks.

## Prompt
```
Read `tasks/queue.md`. Find the FIRST unchecked item (marked `- [ ]`).

Extract:
- Topic title
- Research question or objective
- Any constraints, data sources, or specific angles mentioned

Write the selected topic to `.kairon/current-topic.md` in this format:
```
# Current Research Topic
Title: {title}
Objective: {research question or objective}
Constraints: {any constraints or focus areas}
```

If ALL items are checked `[x]`, write "QUEUE_COMPLETE" to `.kairon/current-topic.md`.
```

## Acceptance Criteria
- [x] First unchecked topic is selected
- [x] `.kairon/current-topic.md` is written with title, objective, constraints
- [x] If queue is complete, writes QUEUE_COMPLETE
