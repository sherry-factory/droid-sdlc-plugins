---
name: implement
description: Implement an approved spec as one PR. Use in the engineering stage.
---
Inputs: tickets/<id>/spec.md and prd.md from the pipeline space.
Branch: <id-lowercase>-<slug>. Implement only what the spec lists, add the tests in its Test plan, run npm test and npm run e2e until green.
Open one PR titled "[<ID>] <ticket title>" whose body links the ticket, quotes the acceptance criteria, and lists the tests. Never push to main, never force-push, never merge.
