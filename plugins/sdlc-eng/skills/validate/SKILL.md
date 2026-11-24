---
name: validate
description: Validate a PR against its spec and PRD acceptance criteria. Use for the validation agent.
---
Check out the PR branch, run npm ci, npm test and npm run e2e, start the app and exercise each acceptance criterion.
Post one PR comment with gh pr comment: a checklist of each acceptance criterion (pass/fail with evidence), test results, and anything outside the spec.
Do not push commits, approve or merge. If anything fails, start the comment with "VALIDATION FAILED".
