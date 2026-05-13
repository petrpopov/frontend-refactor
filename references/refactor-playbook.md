# Refactor Playbook

## Smell → likely action

- **Large route/page file** → keep orchestration there, move visible sections into feature-local components
- **Huge modal** → split into shell, header, body sections, metadata rows, action area
- **Large form** → separate data loading/mutation orchestration from the form view; split repeated field groups
- **Mixed query + local UI logic** → keep query hook near orchestration, isolate UI state and event logic
- **Duplicated JSX rows/cards** → create a row/card component or a tiny render helper
- **Feature code in shared** → move it back into the feature and only keep truly reusable primitives in shared
- **Inline style overload** → convert repeated role-based styles into classes, primitives, or local style helpers

## Decomposition patterns

### Overgrown page

Target shape:
- page file
- feature section components
- optional feature hook
- small shared primitives only if reused across features

Example mental model:
- page = chooses data + wires actions + composes sections
- section = owns one visible slice
- row/card/item = repeated leaf UI

### Overgrown modal

Target shape:
- modal shell
- header/status area
- participants/details/body sections
- row/table primitives if repeated
- external links/action cluster

### Overgrown form

Target shape:
- page or card orchestrator
- form component
- optional field-group components
- validation schema/helpers near the form domain
- mutation stays near orchestration unless reused

### Overgrown builder/editor screen

Target shape:
- page orchestrator
- toolbar/actions
- canvas/main workspace
- side panel/editor panel
- adapter helpers for serialization or validation
- hook only if behavior logic dominates the page

## Style cleanup playbook

Use this order:
1. delete dead styles
2. collapse repeated inline values
3. replace repeated role-based inline styles with classes or tiny local primitives
4. keep one-off inline styles only when they are truly local and self-explanatory

Do not create a global styling abstraction for one component.

## Naming rules

Prefer names that reveal responsibility:
- `ConnectionsStatusSection`
- `TestSendCard`
- `BotGraphToolbar`
- `EventMetaTable`

Avoid names that reveal only position:
- `LeftBlock`
- `InnerContent`
- `SectionTwo`

## Refactor sequencing

When possible:
1. move pure view pieces first
2. stabilize props and boundaries
3. extract behavior next
4. simplify state
5. remove obsolete helpers
6. run verification again
