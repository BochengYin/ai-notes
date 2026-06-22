---
title: TDD
summary: A test-first development skill focused on observable behavior, tracer bullets, and vertical red-green loops.
component_type: skill
status: verified
tags:
  - tdd
  - testing
  - agents
  - skills
  - workflow
updated: 2026-06-22
source_url: https://github.com/mattpocock/skills/blob/main/skills/engineering/tdd/SKILL.md
---

# TDD

## What It Is

This is a test-driven development skill from Matt Pocock's skills repository.

The core idea is behavior-first development: write one test for one visible behavior, make that test pass with the smallest useful implementation, then repeat. The skill pushes the agent toward public interfaces and integration-style tests instead of tests that are tightly coupled to implementation details.

## My Takeaway

The most useful term in this skill is `tracer bullet`.

The term comes from *The Pragmatic Programmer* by Andrew Hunt and David Thomas. Their software analogy comes from tracer ammunition: visible rounds let you see where the real rounds are going, then adjust quickly under real conditions. In software, a tracer bullet is a thin working path through the real system.

After switching into software engineering, this term became a very useful mental model for me. Normal feature work should prove the vertical path first: router, server, domain logic, database, and back through the public interface. Once that path works end to end, the rest of the behavior can be added incrementally.

Matt's observation is precise for agents. Agents often drift into horizontal test creation: write a batch of imagined tests first, then fill in code later. That looks productive, but it can create tests for the shape of the implementation rather than the behavior of the system. The tracer bullet loop forces the agent to learn from one red-green cycle before writing the next test.

## Example

Imagine adding a simple `POST /transfers` endpoint.

Start with one tracer bullet test:

- Red: a user can submit a valid transfer request and receive a created transfer id.
- Green: route the request through the handler, service, and database with the smallest implementation that makes the behavior pass.

That first test proves the path works end to end. After that, add one behavior at a time:

- reject insufficient balance
- reject invalid destination account
- record an audit event
- make duplicate request handling idempotent

Each new behavior gets its own red-green loop. The test names stay close to user-visible behavior, and the implementation grows from real feedback instead of a guessed test matrix.

## Notes

This skill is useful when the agent is about to build or fix behavior where tests should guide the implementation. I would use it when I want a vertical slice first, especially in repo areas where integration boundaries matter.

## Provenance

This component is based on Matt Pocock's `tdd` skill.

The tracer bullet explanation references *The Pragmatic Programmer* by Andrew Hunt and David Thomas and the Artima interview where they explain tracer bullets as a feedback technique for software development.

Sources:

- Matt Pocock, `tdd` skill: [mattpocock/skills/skills/engineering/tdd/SKILL.md](https://github.com/mattpocock/skills/blob/main/skills/engineering/tdd/SKILL.md)
- Artima interview: [Tracer Bullets and Prototypes](https://www.artima.com/articles/tracer-bullets-and-prototypes)
- O'Reilly book listing: [The Pragmatic Programmer, Topic 12: Tracer Bullets](https://www.oreilly.com/library/view/the-pragmatic-programmer/9780135956977/f_0030.xhtml)
