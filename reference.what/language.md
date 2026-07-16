# Llux Language Reference

**Status:** Pre-release reference  

This page describes the active Llux language direction. Older drafts used `computed`, `command`, `effect`, `resource`, and `layout`; those terms should be treated as historical or draft terminology unless reintroduced deliberately.

## Core Principles

1. **Plain names, clear intention.** Keywords use ordinary words.
2. **Explicit scope.** State is addressed through scopes such as `app.count`, `session.user`, or `component.value`.
3. **Four core constructs.** The language centers on `state`, `bind`, `action`, and `view`.
4. **One language everywhere.** `.llux` carries implementation; `.llux.md` can reference Llux expressions with `@`.
5. **Kind errors.** Errors should identify the root cause, location, and likely fix.

## The Transit Contract (Surface ↔ Engine)

Every Llux project defines a bi-directional bridge between the **Surface** (the UI) and the **Engine** (the business logic or real world).

| Direction | What it does | Defined in |
| :--- | :--- | :--- |
| **Out** (Surface → Engine) | User actions (clicks, inputs, gestures) | `action` definitions |
| **In** (Engine → Surface) | State updates, data, real-time metrics | `state` definitions |

The `.llux` file is the **formal contract** for this transit. The compiler uses it to generate:

- A C header (`.h`) for the developer to implement the Engine
- A binary module (`.so`/`.dylib`/`.dll`) that renders the Surface and dispatches Actions

The contract is the **single source of truth** between designer and developer.

### Mock Data for Design Exploration

Designers can preview the Surface without an Engine using the `@mock` prefix:

```markdown
::: Label { text: "User: " + @mock.user.name }
::: Button { action: "AddToCart" }
```

The `@mock` prefix tells the compiler: "generate fake data for this binding." The preview runs with rich, domain-appropriate mock data so the designer can iterate freely.

### Extracting a Contract from a Surface

When a designer has built a complete Surface using `@mock` data and inline action names, the compiler can extract the formal contract:

```bash
llux extract --from=surface.llux.md --to=contract.llux
```

The extracted contract contains all referenced state fields and actions, ready for the developer to implement.
```

## File Types

| Extension | Purpose |
| :--- | :--- |
| `.llux` | Logic, state, actions, and views. |
| `.llux.md` | Intent, layout, semantics, and design-time explanation. |
| `.lmd` | Short extension for Llux Layout Markdown. |

## Entrypoint

| Item | Decision |
| :--- | :--- |
| Entrypoint file | `start.llux` |
| Root view | `RootView` |

The naming follows the same style as `README`: direct and human-oriented. `start.llux` means “start here.”

## Constructs

### `state`

Mutable data. State should be explicitly scoped.

```llux
app state {
    count = 0
}

session state {
    user = null
}
```

Use scoped references:

```llux
app.count
session.user
component.value
```

### `bind`

Derived data or reactive binding.

```llux
bind double = app.count * 2
```

### `action`

A state-modifying operation.

```llux
action Increment(amount = 1) {
    app.count += amount
}
```

### `view`

Visual structure.

```llux
view RootView {
    Panel {
        Label { text: "Count: " + app.count }
        Button { label: "+1"; action: Increment(1) }
    }
}
```

## Layout Markdown Glue

Layout Markdown is for structure and intent. Use `@` when a Markdown attribute should be interpreted as a Llux expression.

```markdown
::: button action=@Increment(1) label="+1"
::: label text=@app.count
```

The `@` prefix means “evaluate this as Llux.”

## Components

The planned component model uses one folder per component:

```text
component/
  component.toml
  intent.llux.md
  logic.llux
  assets/
  tests/
```

Components communicate through declared capabilities rather than hidden cross-component coupling.

## Current Parser Note

The parser also recognises supporting top-level forms such as `services`, `import`, and `component`. Public examples should still emphasise the four core constructs unless they are documenting those supporting forms directly.

## Historical Terminology

| Older term | Current direction |
| :--- | :--- |
| `computed` | Prefer `bind`. |
| `command` | Prefer `action`. |
| `layout` | Prefer `view` for `.llux`; use Layout Markdown for `.llux.md`. |
| `resource` / `effect` | Treat as draft design space until re-specified. |
