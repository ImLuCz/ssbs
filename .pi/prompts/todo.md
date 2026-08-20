---
description: Add a task to TODO.md under the right time horizon
argument-hint: "<today|week|month|someday> <task>"
---
Add "${@:2}" as a checkbox item to TODO.md under the section matching "$1"
(today -> ## Today, week -> ## This Week, month -> ## This Month, someday ->
## Someday). If $1 doesn't clearly map to one of these, ask me instead of
guessing.
