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
