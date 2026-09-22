---
name: spec-new
description: Interview the user in depth about a feature, then write a feature specification (what and why, not how) to the project's specs folder. Invoked explicitly as /spec-new <feature name>.
disable-model-invocation: true
argument-hint: <feature name>
---

Write a feature specification for: $ARGUMENTS

## 1. Decide where it goes

- If a CLAUDE.md names a spec location, use that.
- Else if the repo already has a specs folder (`docs/specs`, `specs/`, `doc/rfc`, …), use it.
- Else default to `docs/specs/`. If the project clearly keeps documentation somewhere else,
  ask instead of creating `docs/specs`.

File name: `NNN-<slug>.md` — `NNN` is the next free three-digit number in that folder
(`001` if empty), `<slug>` is the feature name in kebab-case.

## 2. Interview

Read the relevant code first, so you never ask what the repo already answers.

Then interview with AskUserQuestion, in focused batches, covering:

- **Scope** — the problem, who it is for, what triggers it
- **User-facing behaviour** — the flow, the states, what people see
- **Data and interfaces** — models, fields, endpoints, jobs, events, external systems
- **Edge cases** — empty, concurrent, permissions, limits, existing data
- **Errors** — what can fail, what the user sees, retried vs surfaced
- **Non-goals** — what this deliberately does not do

Rules:

- Dig into the hard parts: ambiguity, trade-offs, anything where two readings produce
  different features. Skip questions with an obvious answer — record the assumption in the
  spec instead.
- Offer concrete options with their consequences, not open-ended prompts.
- Keep going until every area above is settled. Several rounds is normal; one batch is never
  enough.

## 3. Write the spec

Always in English, whatever language the interview was in.

WHAT and WHY only — no implementation plan, no file-by-file task list, no code, no schema
DDL. Naming the modules, endpoints and models involved is fine and wanted.

Sections: Summary · Goals · Behaviour · Data & interfaces · Edge cases & errors ·
Out of scope · Open questions (only if any remain) · Acceptance criteria.

**Acceptance criteria** are checkable statements and end with one end-to-end verification
step someone can actually run to prove the feature works.

## 4. Finish

Print the path, then tell the user to start a fresh session and run `/spec-plan <NNN>` there
before implementing.
