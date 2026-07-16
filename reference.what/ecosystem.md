# A Relational View of the Llux Ecosystem

## The Core Primitives

Before we draw the diagram, let's identify the primitives. These are the **atomic concepts** that everything else is built on:

| Primitive | Description | Role |
| :--- | :--- | :--- |
| **Intent** | What the user wants to achieve. Natural language, descriptive, declarative. | The writer's raw expression. |
| **Component** | A reusable, self-contained unit of UI or logic. Has a purpose, behaviour, and appearance. | The building block. |
| **Registry** | A knowledge base that maps intent to components, services, and patterns. | The resolver's reference. |
| **Resolver** | The engine that reads intent, queries the registry, and generates a concrete specification. | The bridge between intent and implementation. |
| **Compiler** | The traditional translation engine (lexer, parser, AST, codegen). | Produces the binary. |
| **Layout** | Spatial arrangement of components on a canvas. | The visual structure. |
| **Logic** | State, actions, reactivity, data flow. | The behavioural structure. |
| **Service** | External capability (API, persistence, logging). | The connection to the outside world. |

---

## High‑Level Relational Diagram (Surface ↔ Transit ↔ Engine)

Every interactive system—whether a smart-home dashboard, an industrial HMI, a VFX render farm monitor, or a museum installation—follows the same pattern.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                        SURFACE (Designer)                           │   │
│   │   .llux.md — Layout, styling, animations, accessibility             │   │
│   │   Binds to state and actions via `@` references                     │   │
│   └───────────────────────────────┬─────────────────────────────────────┘   │
│                                   │                                         │
│                                   │ Transit Contract (.llux)                │
│                                   │ Defines: State (In) & Actions (Out)     │
│                                   ▼                                         │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                      LLUX BINARY (Compiler)                         │   │
│   │   .so / .dylib / .dll + .h header                                   │   │
│   │   Renders the Surface. Dispatches Actions out.                      │   │
│   │   Accepts State updates in.                                         │   │
│   └───────────────────────────────┬─────────────────────────────────────┘   │
│                                   │                                         │
│                                   │ C API (ui_action_dispatch, ui_state_set)│
│                                   ▼                                         │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                        ENGINE (Developer)                           │   │
│   │   Business logic, APIs, databases, hardware drivers, PLCs           │   │
│   │   Receives Actions. Emits State.                                    │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### The Workflow in Three Steps

| Step | Who | Artifact |
| :--- | :--- | :--- |
| 1. Build the Surface | Designer | `.llux.md` (intent + layout) |
| 2. Define the Transit | Compiler (or Designer) | `.llux` (state + actions) |
| 3. Implement the Engine | Developer | Business logic (C/C++/Rust/Zig) |

The Llux binary bridges the Surface and the Engine. The developer never touches the Surface; the designer never touches the Engine.


---

## The Three Layers of Intent

Intent exists at three levels, each feeding into the next:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  LAYER 1: USER INTENT                                                       │
│  What the user wants to achieve.                                            │
│                                                                             │
│  "I want a counter app. The user clicks a button and the number goes up."   │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│  LAYER 2: DESIGN INTENT                                                     │
│  What the designer wants the UI to look like.                               │
│                                                                             │
│  "The counter is in the center. The button is below it and is blue."        │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│  LAYER 3: IMPLEMENTATION INTENT                                             │
│  What the developer wants the system to do.                                 │
│                                                                             │
│  "The counter is state. The button triggers an action. The state updates."  │
└─────────────────────────────────────────────────────────────────────────────┘
```

**The Resolver bridges all three layers.** It reads the highest-level intent and resolves it down to implementation.

---

## The Data Flow Pipeline

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  Intent      │    │  Resolver    │    │  Compiler    │    │  Binary      │
│  (Natural    │───▶│  (Matches    │───▶│  (Generates  │───▶│  (Runs on    │
│  Language)   │    │   Intent     │    │   C Code)    │    │   Anywhere)  │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
                           │                    │
                           ▼                    ▼
                    ┌──────────────┐     ┌──────────────┐
                    │  Registry    │     │  AST         │
                    │  (Mappings)  │     │  (Tree)      │
                    └──────────────┘     └──────────────┘
```

**The pipeline is linear:** Intent → Resolver → Compiler → Binary.

**The registry is a reference, not a stage.** It is queried by the resolver.

**The AST is an internal structure, not a user-facing output.**

---

## The Abstraction Stack

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  USER EXPERIENCE                                                            │
│  What the user sees and interacts with.                                     │
│  (Binary output)                                                            │
└─────────────────────────────────────────────────────────────────────────────┘
                                      ▲
                                      │
┌─────────────────────────────────────────────────────────────────────────────┐
│  IMPLEMENTATION LAYER                                                       │
│  Explicit code, explicit syntax, explicit references.                       │
│  (.llux, .llux.md with explicit syntax)                                     │
└─────────────────────────────────────────────────────────────────────────────┘
                                      ▲
                                      │
┌─────────────────────────────────────────────────────────────────────────────┐
│  RESOLUTION LAYER                                                           │
│  Intent → Implementation mappings.                                          │
│  (Resolver, Registry, Services, Learning)                                   │
└─────────────────────────────────────────────────────────────────────────────┘
                                      ▲
                                      │
┌─────────────────────────────────────────────────────────────────────────────┐
│  INTENT LAYER                                                               │
│  What the writer wants to achieve.                                          │
│  (Natural language, descriptive, relational)                                │
└─────────────────────────────────────────────────────────────────────────────┘
```

**The writer works in the Intent Layer.** The system handles the rest.

---

## The Two-File Approach: A Detailed View

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  .llux.md (Intent + Layout + Semantics)                                     │
│  - Natural language intent                                                  │
│  - `:::` layout containers                                                  │
│  - Semantic roles and metadata                                              │
│  - `@` references to logic                                                  │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│  .llux (Logic + State + Actions)                                            │
│  - `state`, `action`, `bind`                                                │
│  - `view` with explicit components                                          │
│  - Services and capabilities                                                │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│  Resolver generates .llux from .llux.md                                     │
│  - Reads intent from .llux.md                                               │
│  - Queries registry                                                         │
│  - Generates explicit .llux code                                            │
└─────────────────────────────────────────────────────────────────────────────┘
```

**The .llux.md is the primary human artefact.** The .llux is generated or co-evolved.

---

## The Registry: A Closer Look

```
┌───────────────────────────────────────────────────────────────────────────┐
│  REGISTRY                                                                 │
│  ┌─────────────────────────────────────────────────────────────────────┐  │
│  │  Component Registry                                                 │  │
│  │  - Panel, Label, Button, Flex, Grid, Page, Card...                  │  │
│  │  - Each with: purpose, properties, behaviour, variants              │  │
│  └─────────────────────────────────────────────────────────────────────┘  │
│  ┌─────────────────────────────────────────────────────────────────────┐  │
│  │  Service Registry                                                   │  │
│  │  - API, Persistence, Logging, Auth...                               │  │
│  │  - Each with: purpose, interface, available methods                 │  │
│  └─────────────────────────────────────────────────────────────────────┘  │
│  ┌─────────────────────────────────────────────────────────────────────┐  │
│  │  Pattern Registry                                                   │  │
│  │  - Common UI patterns: login form, search bar, dashboard...         │  │
│  │  - Each with: structure, behaviour, usage examples                  │  │
│  └─────────────────────────────────────────────────────────────────────┘  │
│  ┌─────────────────────────────────────────────────────────────────────┐  │
│  │  Design Token Registry                                              │  │
│  │  - Colors, fonts, spacing, radius, elevation...                     │  │
│  │  - Each with: values, relationships, semantics                      │  │
│  └─────────────────────────────────────────────────────────────────────┘  │
└───────────────────────────────────────────────────────────────────────────┘
```

**The registry is the "knowledge base" of the system.** The resolver queries it to translate intent to implementation.

---

## The Resolver (Patchbay) in Detail

```
┌───────────────────────────────────────────────────────────────────────────┐
│  RESOLVER (The Patchbay)                                                  │
│  ┌─────────────────────────────────────────────────────────────────────┐  │
│  │  Intent Parser                                                      │  │
│  │  - Reads natural language intent                                    │  │
│  │  - Extracts: what, where, how, constraints                          │  │
│  └─────────────────────────────────────────────────────────────────────┘  │
│                                      │                                    │
│                                      ▼                                    │
│  ┌─────────────────────────────────────────────────────────────────────┐  │
│  │  Match Engine                                                       │  │
│  │  - Queries registry for matching components/services                │  │
│  │  - Uses: synonyms, context, priorities, preferences                 │  │
│  └─────────────────────────────────────────────────────────────────────┘  │
│                                      │                                    │
│                                      ▼                                    │
│  ┌─────────────────────────────────────────────────────────────────────┐  │
│  │  Ambiguity Handler                                                  │  │
│  │  - If multiple matches, suggests alternatives                       │  │
│  │  - If no matches, suggests closest                                  │  │
│  └─────────────────────────────────────────────────────────────────────┘  │
│                                      │                                    │
│                                      ▼                                    │
│  ┌─────────────────────────────────────────────────────────────────────┐  │
│  │  Code Generator                                                     │  │
│  │  - Produces explicit .llux from resolved intent                     │  │
│  └─────────────────────────────────────────────────────────────────────┘  │
└───────────────────────────────────────────────────────────────────────────┘
```

**The Resolver is not a compiler.** It is a **translation engine** that converts intent into explicit syntax.

---

## The Complete Relational Diagram (Textual)

```
                           ┌─────────────────┐
                           │     WRITER      │
                           │  (Human)        │
                           └────────┬────────┘
                                    │
                                    │ Writes
                                    ▼
                           ┌─────────────────┐
                           │     .llux.md    │
                           │  Intent +       │
                           │  Layout +       │
                           │  Semantics      │
                           └────────┬────────┘
                                    │
                                    │ Passes to
                                    ▼
                           ┌─────────────────┐
                           │   RESOLVER      │
                           │  (Patchbay)     │
                           └────────┬────────┘
                                    │
                ┌───────────────────┼───────────────────┐
                │                   │                   │
                ▼                   ▼                   ▼
       ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
       │   REGISTRY      │ │   SERVICES      │ │   LEARNING      │
       │  Intent → Impl. │ │  External I/O   │ │  Preferences    │
       └─────────────────┘ └─────────────────┘ └─────────────────┘
                │                   │                   │
                └───────────────────┼───────────────────┘
                                    │
                                    │ Generates
                                    ▼
                           ┌─────────────────┐
                           │     .llux       │
                           │  Explicit       │
                           │  Syntax         │
                           └────────┬────────┘
                                    │
                                    │ Passes to
                                    ▼
                           ┌─────────────────┐
                           │   COMPILER      │
                           │  Lexer → Parser │
                           │  → AST → Codegen│
                           └────────┬────────┘
                                    │
                                    │ Produces
                                    ▼
                           ┌─────────────────┐
                           │    BINARY       │
                           │  Executable     │
                           └─────────────────┘
```

---

### Importers & Exporters (The Extensibility Layer)

The compiler is built around a canonical AST. Importers translate foreign source formats into this AST; exporters translate the AST into target formats.

```
                    ┌─────────────────┐
                    │  Llux AST       │
                    │  (Canonical)    │
                    └────────┬────────┘
                             │
           ┌─────────────────┼─────────────────┐
           │                 │                 │
           ▼                 ▼                 ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│   IMPORTERS     │ │   EXPORTERS     │ │   COMPILER      │
│ SwiftUI → AST   │ │ AST → Native    │ │  (Core)         │
│ React → AST     │ │ AST → HTML      │ │                 │
│ HTML → AST      │ │ AST → React     │ │                 │
└─────────────────┘ └─────────────────┘ └─────────────────┘
```

**Importers** read foreign source formats and produce Llux source (`.llux.md`). This enables translation from existing UI codebases into Llux.

**Exporters** read Llux source and produce target formats. The default exporter produces a native binary. Optional exporters produce static HTML (zero JavaScript), dynamic HTML (self-contained interactive prototype), or framework-specific output.

**The core compiler does not depend on any importer or exporter.** They are optional plugins. This keeps the toolchain offline-first and dependency-free while enabling broad interoperability.

---

## How This Fits Together

1. **The writer starts with intent** (natural language, descriptive).
2. **The writer adds layout and semantics** (using `:::` containers).
3. **The writer adds logic references** (using `@` to refer to state, actions, etc.).
4. **The resolver reads the intent** and queries the registry.
5. **The resolver generates explicit `.llux` code** from the resolved intent.
6. **The compiler compiles the `.llux` code** to a binary.
7. **The binary runs** and displays the UI.

**The writer only interacts with the top layer.** The resolver handles the translation to explicit syntax. The compiler handles the translation to binary.

---

## The Relational Matrix: Which Parts Depend on What

| Component | Depends On | Is Depended On By |
| :--- | :--- | :--- |
| **Intent** | None (primary input) | Resolver |
| **Resolver** | Registry, Services, Learning | Compiler (via generated .llux) |
| **Registry** | Component definitions, Service definitions | Resolver |
| **Services** | External APIs, DB, etc. | Resolver, Runtime |
| **Learning** | Resolver output, Writer preferences | Resolver |
| **.llux** (generated) | Resolver | Compiler |
| **Compiler** | .llux | Binary |
| **Binary** | Compiler | Runtime |

---

## The Keep-or-Throw-Away Decision

| Component | Action | Rationale |
| :--- | :--- | :--- |
| **Current compiler pipeline** | ✅ Keep | It works. It's the foundation. |
| **Current syntax (.llux)** | ✅ Keep | It's the explicit implementation layer. |
| **Current AST** | ✅ Keep | It's the internal representation. |
| **Current code generator** | ✅ Keep | It produces C code. |
| **Current UI backend** | ✅ Keep | It's the binary output layer. |
| **Current CLI** | ✅ Keep | It's the user entry point. |
| **Current lexer/parser** | ✅ Keep | They're part of the compiler. |
| **Current doctor** | ✅ Keep | It validates explicit code. |
| **Current diagnostics** | ✅ Keep | It reports errors. |
| **Current registry (stub)** | ⚠️ Extend | Needs to become the resolver's knowledge base. |
| **Current `:::` syntax** | ✅ Keep | It's the layout layer. |
| **Current `@` glue** | ✅ Keep | It's the bridge to logic. |
| **Intent layer** | ➕ Add | New layer above the resolver. |
| **Resolver (patchbay)** | ➕ Add | New engine that bridges intent to implementation. |
| **Learning system** | ➕ Add | New subsystem that tracks preferences. |
| **Natural language parser** | ➕ Add | New engine that reads intent. |
| **Ambiguity handler** | ➕ Add | New subsystem that handles multiple matches. |

**The changes are additive.** We keep the existing work and add new layers above it.

---

## Final Thought

The system is a **stack**:

```
Intent Layer (Natural Language)
    │
    ▼
Resolver (Patchbay)
    │
    ▼
Implementation Layer (.llux + .llux.md)
    │
    ▼
Compiler (Lexer → Parser → AST → Codegen)
    │
    ▼
Binary (Executable)
```

**The writer works at the top of the stack.** The system handles the rest.

The resolver is the **new core**—it transforms the system from a "language" to an "intent understanding system." The compiler remains the bottom layer, but it is no longer the primary interface. The writer interacts with the intent layer, and the resolver handles the translation.

**This is the high-level Llux: a system that understands intent, not a language that executes instructions.**
