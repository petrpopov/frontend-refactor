---
name: frontend-refactor
description: Use when refactoring frontend code, especially React codebases with oversized components, tangled hooks or state, weak file boundaries, duplicated JSX, or messy styling that needs disciplined decomposition without changing behavior
---

# Frontend Refactor

## Overview

Use this skill to refactor frontend code safely and deliberately. It is React-first, but most rules also apply to general component-based frontend code.

This is a **rigid workflow**. Do not jump straight to edits. Do not rename "cleanup" if you have not identified the actual problems. Preserve behavior unless the user explicitly asks for behavior changes.

## When to Use

Use when you see one or more of these symptoms:
- route or page files are too large to understand at a glance
- components mix orchestration, business rules, data fetching, forms, and markup in one file
- hooks or effects are hard to reason about
- local state duplicates query state or derived state
- repeated JSX blocks or repeated style objects appear in several places
- feature-specific code has leaked into shared folders
- inline styles dominate the file and hide the component structure

Do not use this skill for greenfield UI implementation from scratch or for pure visual redesign work.

## Tool-Agnostic Rule

Use the best equivalent tools available in the current harness for:
- directory and file inspection
- search and grep
- reading targeted files
- running typecheck, lint, tests, and build commands
- browser or UI inspection when a visible surface is affected

Do not depend on any single IDE, MCP server, or CLI.

## Required Reading

- Read `references/react-rules.md` before planning any React refactor.
- Read `references/refactor-playbook.md` before decomposing files.
- Read `references/validation.md` before claiming the work is complete.

## The Workflow

### 1) Analyze before editing

Required actions:
1. Inspect the relevant file tree and identify the exact frontend slice in scope.
2. Read only the files needed to understand boundaries, data flow, styles, and tests.
3. Produce a **problem map** before making changes.

Your problem map must name:
- file or files involved
- the specific smell in each file
- why it harms readability, reuse, testability, or safety
- user-visible or regression risk

If you cannot state the problem map clearly, stop and analyze further.

### 2) Plan the target decomposition

Before editing, define the intended boundaries:
- which file stays as orchestration
- which parts become feature-local components
- which logic, if any, becomes a custom hook
- which pieces are truly shared
- how styles will be simplified or normalized
- which verification commands will prove safety

Do not split code “because it feels cleaner.” Every extracted unit needs one clear responsibility.

### 3) Refactor in small safe steps

Prefer a sequence like this:
1. extract passive UI sections
2. extract repeated local helpers
3. move feature-specific logic next to the feature
4. extract hooks only when the logic becomes clearer or reusable
5. reduce style duplication
6. delete dead intermediate abstractions

Keep each step reviewable. Avoid broad rewrites.

### 4) Apply React-first rules while refactoring

Mandatory rules:
- route/page components should mostly orchestrate data, params, actions, and sections
- feature components should represent one scenario or one visible section
- custom hooks should own behavior, not hide random JSX coupling
- do not store derived state when it can be computed during render
- use effects only for synchronization with external systems
- shared UI must be genuinely shared, not just moved away
- prefer feature-local code over premature shared abstractions
- split by responsibility, not by the old “stateful vs stateless” dogma

See `references/react-rules.md` for exact heuristics.

### 5) Verify before claiming success

Minimum expectation:
- run the narrowest relevant checks first
- then run the broader project checks that cover the touched area
- inspect affected UI behavior when the refactor touches visible surfaces
- confirm no accidental behavior changes were introduced

See `references/validation.md` for the mandatory verification gate.

### 6) Perform a final smell review

Before finishing, check for these failures:
- the old giant component simply moved into a new file
- a hook now does too many unrelated things
- “shared” code has only one realistic consumer
- effects are still used for derivation or event choreography
- props became harder to follow after the split
- style cleanup created indirection without clarity

If any of these are true, keep refactoring.

## Hard Stop Conditions

Stop and rethink if you are about to do any of these:
- split a component without being able to name the new responsibility
- extract a hook that is only a dumping ground for code moved out of sight
- move code into `shared` to avoid making a feature folder
- introduce new abstractions before removing duplication in the current file
- preserve a misleading component name after its responsibility changed
- claim success without command output or UI evidence

## Output Expectations

When using this skill, finish with:
1. a short before/after boundary summary
2. the files changed and why
3. verification commands run
4. any remaining follow-up refactors worth doing later
