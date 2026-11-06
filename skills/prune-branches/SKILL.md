---
name: prune-branches
---

For each branch, find associated PR.

Report:
- Branch
- PR
- PR status

Delete branch (and its worktree if it has one) if:
- It's associated PR is merged/closed
- It has no commits beyond origin master
