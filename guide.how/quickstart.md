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


Here is the plan to reframe `llux.org` to reflect what Llux actually is—a tool for independent creators who need to move fast, own their work, and never be trapped by a platform.

---

## The Reframing Strategy

### The Core Message

**Llux is for creators who want to build software that runs anywhere, without being tied to a single platform or ecosystem.**

**The audience will say "yes, of course" because:**

| What they hear | Why it resonates |
| :--- | :--- |
| "Build once, run anywhere" | They have been burned by platform lock-in |
| "You own the binary" | They want control over their work |
| "No dependencies, offline-first" | They want simplicity and reliability |
| "Designer-first" | They want to work the way they think |
| "AI-assisted" | They want to move faster |

---

## What Changes

| Page | Change | Why |
| :--- | :--- | :--- |
| **Homepage (README.md)** | New hero section that frames Llux as a tool for independent creators | First impression must land |
| **Homepage "Who This Is For"** | Add "Independent creators, entrepreneurs, and solo founders" | Signal the primary audience |
| **Philosophy (index.md)** | Add "Independence and Autonomy" section | Explain the "why" without triggering rebellion concerns |
| **Philosophy (index.md)** | Add "Not Rebellion" section | Preempt misinterpretation |
| **Quickstart** | Add "The Creator's Path" section | Show the journey from intent to ownership |
| **Roadmap** | Add "Creator-First" section | Signal that independence is a priority |

---

## The Actual Text

### 1. Homepage (`README.md`)

**Replace the current hero section (lines 1-9) with:**

```markdown
Llux is a tool for independent creators.

It turns your interface ideas into native software that runs anywhere—without platform lock-in, hidden dependencies, or surprises.

You describe the intent. Llux compiles it to a binary. You own it.

---

Every interactive system—whether a smart-home dashboard, a CNC machine HMI, or a museum installation—follows the same pattern: **Surface ↔ Transit ↔ Engine**. Llux compiles the Surface and the Transit rules. You bring the Engine.

**No platform lock-in. No hidden dependencies. No surprises.**
```

**Add a new bullet to "Who This Is For" (after the first bullet):**

```markdown
- Independent creators, entrepreneurs, and solo founders who want to build software that runs anywhere, without being tied to a single platform or ecosystem.
```

---

### 2. Philosophy Page (`philosophy.why/index.md`)

**Add this section after "The Covenant" and before "Design Philosophy":**

```markdown
## Independence and Autonomy

Llux is built on the principle that creators should be free to build what they want, where they want, without asking permission.

This is not about rebellion. It is about **autonomy**: the ability to make your own choices.

### What Independence Means in Llux

| Aspect | What It Means |
| :--- | :--- |
| **Platform independence** | Your software runs on any platform—desktop, embedded, server, or web. |
| **Offline-first** | You do not need the internet to build or run your software. |
| **Zero dependencies** | Your software does not depend on others' code or services. |
| **Native binary** | Your software is an executable you own and control. |
| **Plain source** | Your code is readable, understandable, and yours. |

### What Autonomy Means for Creators

- **You choose your tools.** Llux does not lock you into a specific IDE, editor, or workflow.
- **You choose your partners.** Llux enables collaboration but does not require it.
- **You choose your future.** Llux does not force you into a single path.

### Independence is Not Isolation

Llux is built for collaboration—not solitude. The independence it provides is the freedom to work with anyone, on any platform, without being trapped.

Independence means you are free to choose your partners, not that you have to work alone.
```

**Add this after "AI as a Transition Compass" (or as a new section at the end):**

```markdown
## Not Rebellion

Llux is not about fighting platforms or ecosystems. It is about **choice**.

We believe that creators should be able to choose the tools, platforms, and partners that work best for them. Llux does not replace or reject other tools—it enables you to work with them on your terms.

Independence is not isolation. It is the freedom to collaborate without being trapped.
```

---

## The Creator's Path

Llux is built for creators who want to move fast and stay independent.

### Step 1: Describe Your Intent

You do not need to write code. Write what you want the UI to do.

```markdown
# app.llux.md

A simple counter app. The user sees a number and a button.
When the button is pressed, the number goes up.
```

### Step 2: Preview Your Work

See your app running instantly. No compilation time. No dependencies.

```bash
llux preview
```

### Step 3: Extract the Contract

When you are ready, Llux extracts the formal contract from your intent.

```bash
llux extract
```

### Step 4: Build and Run

Llux compiles your intent to a native binary. It runs anywhere.

```bash
llux build
llux run
```

### Step 5: Own It

The binary is yours. No platform lock-in. No hidden dependencies.

You can distribute it, embed it, or deploy it—however you choose.
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
