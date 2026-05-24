# Task 007: check-queue

## Workflow
strategy-research-loop

## Type
DETERMINISTIC (bash command — execute exactly as written)

## Description
Checks if all queue items are complete. If so, signals the loop to enter refinement mode.

## Bash Command (DETERMINISTIC)
```bash
UNCHECKED=$(grep -c '^- \[ \]' tasks/queue.md || true)
if [ "$UNCHECKED" -eq 0 ]; then
  echo "ALL_TOPICS_COMPLETE"
else
  echo "$UNCHECKED topics remaining — continuing to next iteration"
fi
```

## Acceptance Criteria
- [x] Prints ALL_TOPICS_COMPLETE if queue is empty
- [x] Prints remaining count if items are pending
