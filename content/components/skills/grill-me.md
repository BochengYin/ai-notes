---
title: Grill Me
summary: A pre-implementation interview skill that turns vague plans into implementation-ready specs by combining codebase exploration with structured planning.
component_type: skill
status: active
tags:
  - claude-code
  - agents
  - skills
  - workflow
updated: 2026-06-22
artifact_path: artifacts/skills/grill-me/SKILL.md
---

# Grill Me

## What It Is

`grill-me` is a pre-implementation skill for turning an unclear plan into a shared, implementation-ready understanding.

Instead of letting the agent jump straight into code, it makes the agent interview the user about every important branch of the decision tree: product goal, implementation scope, constraints, edge cases, tradeoffs, and unresolved dependencies.

The key rule is simple: ask one question at a time, recommend an answer for each question, and keep going until the plan is clear enough to execute.

## When To Use It

Use `grill-me` when the problem is still underspecified:

- You have a product or feature idea but not a clear spec.
- You are about to start a multi-file implementation.
- You are unsure which tradeoffs matter.
- You want the agent to expose hidden assumptions before coding.
- You need a design conversation, not a patch.

Do not use it for tiny, obvious edits where the diff can be described in one sentence.

## How To Use It

Start with a rough plan and explicitly ask the agent to grill you before implementation:

```text
Use grill-me on this plan.
Interview me one question at a time until the requirements, tradeoffs, and execution plan are clear.
For each question, include your recommended answer.
If the answer can be discovered from the codebase, inspect the codebase instead of asking me.
```

The output should be a clarified plan, not implementation. Once the plan is settled, start a separate implementation step or session.

## Artifact

The reusable skill artifact lives at:

```text
artifacts/skills/grill-me/SKILL.md
```

## Notes

`grill-me` is not a full build workflow. It does not implement, verify, commit, or open a PR. Its job is to make the early stages sharper.

Claude Code's official best-practice workflow has four phases:

1. Explore
2. Plan
3. Implement
4. Commit

`grill-me` intentionally uses the first two:

- `Explore`: if the answer is discoverable from the codebase, the agent should inspect the codebase instead of asking the user.
- `Plan`: the agent interviews the user until the design tree and execution plan are clear.

Verification still belongs downstream. After `grill-me`, the implementation prompt should include a concrete check: tests, typecheck, lint, screenshot comparison, or another pass/fail signal.

## Provenance

This component is based on a local adaptation of Matt Pocock's `grill-me` skill.

It also adapts two Claude Code best practices:

- Claude Code recommends separating research and planning from implementation in the `Explore -> Plan -> Implement -> Commit` workflow.
- Claude Code also recommends having Claude interview the user for larger features before implementation.

Sources:

- Matt Pocock, `grill-me` skill: [mattpocock/skills/skills/productivity/grill-me/SKILL.md](https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md)
- Claude Code Best Practices: [Explore first, then plan, then code](https://code.claude.com/docs/en/best-practices#explore-first-then-plan-then-code)
- Claude Code Best Practices: [Let Claude interview you](https://code.claude.com/docs/en/best-practices#let-claude-interview-you)

