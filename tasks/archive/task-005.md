# Task 005: write-findings

## Workflow
strategy-research-loop

## Type
PROMPT (LLM reasoning — document output and commit)

## Description
Writes the final findings to `research-log.md` (the main output file) and commits the changes.

## Prompt
```
Write the final findings to the project's output file.

1. Read `.kairon/current-topic.md` and `.kairon/analysis.md`
2. Append findings to `research-log.md` (create it if it doesn't exist) with this format:

```
## {Title} — {YYYY-MM-DD}
### Objective
{research question}

### Key Findings
- Finding 1
- Finding 2

### Strategic Implications
- Implication 1
- Implication 2

### Recommended Actions
- [ ] Action 1
- [ ] Action 2

### Sources
- Source 1 (URL)
- Source 2 (URL)

---
```

3. If the topic relates to a specific document (e.g., a 100-day plan), also update that document with relevant sections or suggestions.
4. Commit the output: `git add -A && git commit -m "research: {title}"`
```

## Acceptance Criteria
- [x] `research-log.md` appended with formatted findings
- [x] Related documents updated if applicable
- [x] Changes committed with descriptive message
