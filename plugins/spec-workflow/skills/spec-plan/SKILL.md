---
name: spec-plan
description: Read an existing feature specification and turn it into an implementation plan against the current codebase. Invoked explicitly as /spec-plan <spec number, slug, or path>.
disable-model-invocation: true
argument-hint: <spec number, slug, or path>
---

Plan the implementation of the spec identified by: $ARGUMENTS

**First action, before reading anything: call EnterPlanMode** (skip only if plan mode is
already active). Everything below happens in plan mode — no edits, no code written.

## 1. Find the spec

Locate the specs folder the same way `/spec-new` does: a CLAUDE.md location, else an existing
specs folder in the repo, else `docs/specs/`.

`$ARGUMENTS` may be a path, a three-digit number, a slug, or part of a title. Empty or
ambiguous → list the specs you found and ask which one. Never guess between two candidates,
and never plan without having read a spec file.

## 2. Read before planning

Read the spec in full, then read the code it names — current state, not assumption. Look for
what already exists: helpers, patterns, and near-identical features to reuse.

Stop and ask with AskUserQuestion when:

- the spec has open questions that change the implementation,
- the code contradicts the spec, or
- the spec is silent on something you would otherwise have to invent.

Do not edit the spec yourself; propose the change and let the user decide.

## 3. Plan

The plan names the files to change or create, the existing functions and modules to reuse
(with paths), the order of work, and the tests to add or update. It covers every acceptance
criterion in the spec; anything in the spec you are deliberately not planning for must be
called out explicitly.

End the plan with the spec's end-to-end verification step, as the way to prove it works.
