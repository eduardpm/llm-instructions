---
name: android-app-foundation
description: Build maintainable Android apps from day one with clean feature structure, clear data/domain/presentation boundaries, and reusable state/mutation flows. Use when starting a new Android app (React Native or Kotlin/Compose) or planning an app architecture before implementation so screens do not accumulate duplicated CRUD/loading logic.
---

# Android App Foundation

Use this skill at project start to set architecture, conventions, and feature scaffolding that prevent duplicated per-screen handlers for load, add, update, delete, toggle, and refresh.

## Scope

Apply this before building features:
- Define feature-first folder/module boundaries.
- Define shared mutation and refresh contracts per feature.
- Define repository and state ownership rules.
- Define testing strategy by layer.
- Define error/loading/empty conventions.

## Inputs

Gather:
- Product requirements and first 1-3 core features.
- Chosen stack (React Native/Expo or Kotlin/Compose).
- Data sources (local DB, API, sync requirements).
- Navigation and auth requirements.

## Workflow

1. Define architecture decisions before coding screens.
- Choose feature-first structure.
- Choose state owner per feature (hook or ViewModel).
- Choose mutation result model (`Result`/sealed type).

2. Define feature contract for each core feature.
- Create a single feature API for load/mutate/refresh.
- Keep screens dependent on feature contract only, never direct DB/API calls.

3. Scaffold state orchestration once per feature.
- Put loading, mutation, error, and refresh orchestration in one place:
  - React Native: custom hook in a feature module.
  - Kotlin/Compose: ViewModel plus use cases.

4. Centralize data access from day one.
- Keep persistence and network logic in repository/data-source layers.
- Expose typed models and typed mutation functions.

5. Standardize mutation and refresh behavior.
- Use one shared mutation path per feature instead of ad-hoc `mutate -> reload` in screens.
- Apply optimistic updates only if rollback is defined.

6. Standardize UI state model.
- Return typed results (`Success`/`Error` or equivalent).
- Ensure every screen handles loading, empty, error, success, and retry consistently.

7. Add tests as part of initial scaffolding.
- Unit-test use cases and feature state owner (hook/ViewModel).
- Add one integration test per core feature flow.
- Keep UI snapshot/render tests minimal.

## Recommended Feature Layout

Use one feature folder per domain:

```text
feature/todos/
  domain/
    models
    use-cases
    repository-interface
  data/
    repository-impl
    local-or-remote-data-sources
  presentation/
    screens
    components
    state (hook or ViewModel)
```

## Build Rules

- Do not call storage/network APIs from screen composables/components.
- Do not duplicate mutation handlers across screens.
- Keep one source of truth for feature state.
- Keep cross-feature coupling behind interfaces.
- Keep business rules out of UI files.

## Done Criteria

- Core features are scaffolded with shared feature contracts.
- New screens are thin and mostly presentational.
- Repository boundaries are respected.
- Error/loading/empty behavior is consistent app-wide.
- Tests exist for feature state and use cases.

## References

- React Native/Expo pattern: `references/react-native.md`
- Kotlin/Compose pattern: `references/kotlin-compose.md`
