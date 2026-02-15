# Kotlin / Compose Day-0 Blueprint

## Goal

Start with clean feature boundaries so composables stay presentational and business logic does not spread.

## Recommended Initial Layout

```text
feature/todos/
  domain/
    model/Todo.kt
    repository/TodosRepository.kt
    usecase/
      GetTodosUseCase.kt
      AddTodoUseCase.kt
      ToggleTodoUseCase.kt
      DeleteTodoUseCase.kt
      UpdateDescriptionUseCase.kt
  data/
    repository/TodosRepositoryImpl.kt
    local/
      TodoEntity.kt
      TodoDao.kt
      TodoMapper.kt
  presentation/
    TodosViewModel.kt
    TodosUiState.kt
    TodosEvent.kt
    TodosScreen.kt
```

## Day-0 Contracts

Define before building screens:

1. `UiState`:
- `isLoading`, `error`, feature data, derived sections.

2. UI events/intents:
- `OnRefresh`, `OnAdd`, `OnToggle`, `OnDelete`, `OnUpdateDescription`.

3. Use case and repository interfaces:
- Domain-facing contracts only.

## ViewModel Pattern

- ViewModel is the only owner of mutation orchestration.
- Composables dispatch events and render state.
- Composables do not call repository/DAO directly.

## Error and Retry Pattern

- Map exceptions to domain-level failure types.
- Keep retry in ViewModel and expose it as an intent.

## Testing Baseline

- Unit test use cases (business rules).
- Unit test ViewModel state transitions.
- Add one integration/UI test for key flow (create -> view -> complete).
