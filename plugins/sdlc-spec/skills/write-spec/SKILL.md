---
name: write-spec
description: Turn an approved PRD into an implementation spec. Use when a ticket is in the spec stage.
---
Inputs: tickets/<id>/prd.md from the pipeline space and the repository.
Write a spec with: Summary, Files to change (paths), Data model changes, UI changes, Test plan (unit + e2e cases mapped to PRD acceptance criteria by number), Rollout and risks, Out of scope.
Every PRD acceptance criterion must map to at least one test. Do not write code, push, or open PRs.
