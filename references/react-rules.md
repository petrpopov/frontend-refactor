# React Rules for Refactoring

## 1. Responsibility boundaries

Prefer these boundaries:
- **Route/page**: params, queries, mutations, top-level orchestration, section composition
- **Feature section/component**: one scenario, card, panel, table, form, modal body, or interaction cluster
- **Custom hook**: behavior or state transitions that become clearer when separated from the view
- **Shared UI**: primitives or reusable composites with multiple realistic consumers

Avoid these anti-patterns:
- one file that fetches data, transforms it, stores UI state, renders multiple sections, and defines helper views inline
- a “shared” component that depends on one feature's vocabulary or API shape
- splitting into container/presentational everywhere by default

## 2. When to extract a component

Extract when at least one is true:
- a JSX block is a clear visual section with its own heading or role
- a repeated block appears more than once
- the parent component becomes easier to scan top-to-bottom after extraction
- the extracted component can be named by responsibility, not by location on screen alone

Do not extract when:
- the child would only forward many props with no clearer boundary
- the block is tiny and used once
- extraction would force awkward names like `LeftPart` or `InnerWrapper`

## 3. When to extract a custom hook

Extract a hook when:
- state transitions or event handlers dominate the component
- the same behavior is reused
- remote/query state and local UI state need a clear adapter layer
- separating behavior makes the render section noticeably simpler

Do not extract a hook when:
- it only hides a long file without clarifying ownership
- it returns too many unrelated values and handlers
- it exists only to move imperative code out of sight

## 4. State rules

Keep state as local as possible.

Prefer:
- query/cache state in query libraries
- local UI state in the nearest component that needs it
- computed values derived during render with plain expressions or `useMemo` only when justified

Avoid:
- copying query results into local state without a sync reason
- storing filtered, mapped, counted, or selected data that can be recomputed
- mirroring props into state unless the component intentionally forks or edits a draft

## 5. Effect rules

Use `useEffect` only for external synchronization:
- subscriptions
- timers
- DOM or browser APIs
- syncing with URL, storage, or network lifecycle when render cannot express it

Do not use effects for:
- deriving data for render
- reacting to one piece of state just to update another piece of state
- orchestrating what should happen directly inside event handlers

If you think you need an effect, first ask:
- can this value be computed during render?
- can this happen in the event handler that caused it?
- can the source of truth move closer to where it is used?

## 6. Query-state boundaries

With React Query or similar tools:
- let query hooks own fetching and cache lifecycle
- keep page components responsible for choosing which queries/mutations to call
- adapt raw API data into view-specific props close to the consumer, unless the transformation is broadly reused
- avoid scattering invalidation logic across unrelated UI components

## 7. File and size heuristics

These are heuristics, not laws:
- ~50–120 lines: usually healthy
- ~120–200 lines: inspect responsibility boundaries
- 200+ lines: likely contains multiple concerns
- route pages can be longer, but should mostly compose sections rather than embed everything inline

Large files are acceptable only if they are still easy to scan by responsibility.

## 8. Style rules

Prefer visible structure over style noise.

Good candidates for cleanup:
- repeated inline style objects
- role-based styling repeated in many places
- visual primitives hidden inside domain components

Be careful not to replace simple readable styles with over-abstracted styling helpers.
