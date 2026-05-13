# Validation Gate

## Minimum verification before completion

Run the best matching checks available in the project:
- typecheck
- lint
- focused tests for touched areas
- broader test/build checks appropriate to the change

Do not say “done”, “fixed”, or “safe” without verification evidence.

## UI verification

If the refactor touched visible UI, also verify:
- the route or screen still renders
- primary interactions still work
- loading, empty, error, and success states still make sense
- extracted sections receive the right props
- no obvious visual regressions were introduced

Use browser automation, screenshots, manual inspection, or story/demo surfaces if available.

## Final self-review checklist

Before finishing, answer these questions:
- Is each new file easier to understand than the original file?
- Did the page become more orchestration-focused?
- Did any extracted hook gain too many responsibilities?
- Did any new shared abstraction appear without real reuse?
- Did style cleanup improve readability rather than hide it?
- Did I avoid storing derived state?
- Did I avoid effect-based derivation?
- Can I explain each extracted unit in one sentence?

If any answer is “no”, keep refining.

## Good completion evidence

A strong completion note includes:
- problem summary
- new boundaries
- files changed
- commands run
- any remaining risks or next-step refactors
