---
description: Perform a code review
argument-hint: "Commit id or revset"
effort: max
---

Code review this commit or PR for quality and potential bugs or issues: `$ARGUMENTS`

Launch sub-agents IN PARALLEL using the Task tool to analyze each area concurrently:

1. Potential Bugs analysis
2. Test coverage analysis
3. Architecture (for larger changes)

Once they have all completed synthesise the results and report back your findings. Tag each issue with the sub-agents that identified the issue.
