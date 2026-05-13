# frontend-refactor

**RU** | [EN](#en)

Claude Code skill для безопасного рефакторинга frontend-кода — React-first, но применим к любым компонентным архитектурам.

## Когда использовать

- Компоненты или страницы слишком большие для понимания с первого взгляда
- Хуки, data fetching, формы и разметка перемешаны в одном файле
- Дублирующийся JSX или повторяющиеся объекты стилей
- Feature-код утёк в shared-папки
- Локальный стейт дублирует query-стейт

## Как подключить

Добавьте репо как submodule или скопируйте в `.claude/skills/`:

```bash
git submodule add https://github.com/petrpopov/frontend-refactor .claude/skills/frontend-refactor
```

## Использование

```
/frontend-refactor
```

Skill проводит анализ, строит problem map, декомпозирует компоненты пошагово и верифицирует результат перед завершением.

---

<a name="en"></a>

**EN**

Claude Code skill for safe, deliberate frontend refactoring — React-first, applicable to any component-based codebase.

## When to use

- Route or page files too large to understand at a glance
- Components mixing orchestration, data fetching, forms, and markup
- Duplicated JSX blocks or repeated style objects
- Feature-specific code leaked into shared folders
- Local state duplicating query or derived state

## Setup

Add as a submodule or copy into `.claude/skills/`:

```bash
git submodule add https://github.com/petrpopov/frontend-refactor .claude/skills/frontend-refactor
```

## Usage

```
/frontend-refactor
```

The skill analyzes the codebase, builds a problem map, decomposes components in small safe steps, and verifies behavior before completion.
