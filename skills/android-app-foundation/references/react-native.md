# React Native / Expo Day-0 Blueprint

## Goal

Start with a feature architecture that keeps screens thin and avoids duplicated CRUD/loading logic.

## Recommended Initial Layout

```text
app/
components/
feature/
  todos/
    data/
      todosRepository.ts
      todosLocalDataSource.ts
    domain/
      todosTypes.ts
      todosUseCases.ts
    presentation/
      useTodosFeature.ts
      TodosScreenState.ts
theme/
db/
```

## Day-0 Contracts

Define these before screen implementation:

1. Feature state contract:
- `loading`, `error`, `data`, and derived sections.

2. Feature actions contract:
- `refresh`, `add`, `toggle`, `remove`, `updateDescription`.

3. Repository contract:
- Typed read/write methods only; no UI concerns.

## Hook Pattern

- One feature hook owns orchestration.
- Screens consume hook outputs and call hook actions.
- Screens never call DB/API modules directly.

## Error and Retry Pattern

- Normalize errors once in feature hook.
- Provide `retry()` in hook for all failed loads.

## Testing Baseline

- Unit test use cases.
- Unit test feature hook transitions:
  - initial load success/failure
  - mutation success/failure
  - refresh after mutation
- Add one integration test for critical path (create -> view -> complete).
