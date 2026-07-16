# Quick Start

**Status:** Pre-release. The core toolchain is under active development; the quick-start flow is being stabilised.

Llux is a designer-first tool. You can start building the interface immediately, without waiting for a developer. The compiler guides you toward a production-ready contract when you're ready to scale.

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
