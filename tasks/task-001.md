# Task 001: read-queue

## Workflow
strategy-research-loop

## Type
DETERMINISTIC (bash command — execute exactly as written)

## Description
Checks if `tasks/queue.md` exists and counts unchecked items. If the queue is empty, signals the loop to enter refinement mode.

## Bash Command (DETERMINISTIC)
```bash
if [ ! -f "tasks/queue.md" ]; then
  echo "ERROR: tasks/queue.md not found. Create a queue file first."
  exit 1
fi
# Count unchecked items
UNCHECKED=$(grep -c '^- \[ \]' tasks/queue.md || true)
echo "Queue status: $UNCHECKED items remaining"
if [ "$UNCHECKED" -eq 0 ]; then
  echo "QUEUE_EMPTY"
fi
```

## Acceptance Criteria
- [x] Verify queue.md exists
- [x] Print unchecked item count
- [x] Print QUEUE_EMPTY if all items are checked
