# Quick Start

**Status:** Pre-release. The core toolchain is under active development; the quick-start flow is being stabilised.

Llux is a tool for independent creators. It turns your interface ideas into native software that runs anywhere—without platform lock-in, hidden dependencies, or surprises.

You can start building the interface immediately, without waiting for a developer. The compiler guides you toward a production-ready contract when you're ready to scale.

---

## The Syntax in Brief

| Purpose | Syntax | Example |
| :--- | :--- | :--- |
| **Static Configuration** | `key=value` | `min=0 max=100` |
| **Inbound Stream** | `@key <- source` | `@text <- app.count` |
| **Bi‑directional Sync** | `@key <-> source` | `@value <-> app.search_query` |
| **Outbound Stream** | `@key -> target` | `@press -> app.increment` |

**The `@` Rule:** `@` marks a **component property as live and reactive**. It belongs on the target (the component's property key), not on the source.

---

## The Creator's Path

Llux is built for creators who want to move fast and stay independent.

### Step 1: Describe Your Intent

You do not need to write code. Write what you want the UI to do.

```markdown
# app.intent.md

A simple counter app. The user sees a number and a button.
When the button is pressed, the number goes up.
```

### Step 2: Build the Surface

Create your layout in `.llux.md` with live bindings.

```markdown
# app.llux.md

::: page
  ::: flex gap-4
    # Inbound: Label's @text pulls from app.count
    ::: Label { @text <- "Count: " + app.count }
    
    # Sync: Slider's @value syncs with app.count
    ::: Slider { @value <-> app.count min=0 max=100 }
    
    # Action: Button's @press pushes to app.increment
    ::: Button { @press -> app.increment label="+1" }
  :::
:::
```

### Step 3: Preview Your Work

See your app running instantly. No compilation time. No dependencies.

```bash
llux preview
```

### Step 4: Extract the Contract

When you are ready, Llux extracts the formal contract from your intent.

```bash
llux extract
```

### Step 5: Build and Run

Llux compiles your intent to a native binary. It runs anywhere.

```bash
llux build
llux run
```

### Step 6: Own It

The binary is yours. No platform lock-in. No hidden dependencies.

You can distribute it, embed it, or deploy it—however you choose.

---

## Designer First Steps (No Developer Required)

```bash
# Create a new project with mock data pre-configured
llux new my-app --with-mock
cd my-app

# Edit the surface (app.llux.md) — layout, styling, and bindings
# Edit the logic (app.llux) — state, actions, and contracts

# Preview your work with live mock data
llux preview

# Let the AI scan your work and suggest improvements or recipes
llux suggest

# When you're ready to formalise the interface, extract the contract
llux extract

# Generate a developer handoff package (contract + C header + plain-language brief)
llux prepare --for=team
```

---

## Developer Handoff (After the Designer Extracts the Contract)

The designer has built the surface and extracted the contract. You receive:

- `contract.llux` — The formal state and action definitions
- `ui_interface.h` — The C header for your app
- `surface.llux.md` — The designer's layout (unchanged)
- A plain-language brief explaining the data flow

```bash
# Build the Llux surface to a native binary module (.so / .dylib / .dll)
llux build

# Integrate the .h into your C/C++/Rust/Zig app
# Implement the action handlers
# Feed state back into the surface via ui_state_set()

# Run the integrated app
llux run
```

---

## Exporting (Documentation & Prototyping)

The same surface can be exported to other formats without changing the contract:

```bash
# Zero-JavaScript HTML — perfect for documentation and design reviews
llux build --target=html-static

# Self-contained interactive HTML prototype — for user testing
llux build --target=html-dynamic

# Export to other UI frameworks (planned)
llux export --to=react
llux export --to=swiftui
```

The native binary remains the primary output. HTML exports are optional extras.

---

## The Complete Example

### Contract (`app.llux`)

```llux
app state {
    count: int = 0
}

action Increment(amount: int = 1) {
    app.count += amount
}
```

### Surface (`app.llux.md`)

```markdown
::: page
  ::: flex gap-4
    # Static: Label displays a static message
    ::: Label { text: "Welcome to the counter app" }
    
    # Inbound: Label's @text pulls from app.count
    ::: Label { @text <- "Count: " + app.count }
    
    # Configuration: Slider properties
    # Sync: Slider's @value syncs with app.count
    ::: Slider { @value <-> app.count min=0 max=100 step=1 }
    
    # Action: Button's @press pushes to app.increment
    ::: Button { @press -> app.increment label="+1" }
  :::
:::
```

### Dataflow Diagram

```
┌───────────────────────────────────────────────────────────────────────────┐
│                                                                           │
│   ┌───────────────────────────────────────────────────────────────────┐   │
│   │                        SURFACE (app.llux.md)                      │   │
│   │                                                                   │   │
│   │   Label { @text <- "Count: " + app.count }   ← Inbound            │   │
│   │   Slider { @value <-> app.count }            ← Sync               │   │
│   │   Button { @press -> app.increment }         ← Outbound           │   │
│   └───────────────────────────────┬───────────────────────────────────┘   │
│                                   │                                       │
│                                   │ Transit Contract (.llux)              │
│                                   ▼                                       │
│   ┌───────────────────────────────────────────────────────────────────┐   │
│   │                        ENGINE (app.llux)                          │   │
│   │   state { count: int = 0 }                                        │   │
│   │   action Increment(amount: int = 1) { count += amount }           │   │
│   └───────────────────────────────────────────────────────────────────┘   │
│                                                                           │
└───────────────────────────────────────────────────────────────────────────┘
```

---

## Next Steps

- Read the full [Language Reference](../reference.what/language.md)
- Explore the [Ecosystem Overview](../reference.what/ecosystem.md)
- Join the [Community](../community.who/contributing.md)

---

*Llux: Tool for independent creators. Build once. Run anywhere. Own it.*
