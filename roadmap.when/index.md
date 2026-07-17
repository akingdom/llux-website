# Llux Strategic Roadmap

**Status:** Pre-release, Phase 0 in progress  
## Mission

Enable more people to turn interface intent into working software with fewer hidden assumptions, fewer unnecessary barriers, and more control over the resulting artefacts.

## Current Direction

The active public direction is:

| Area | Current decision |
| :--- | :--- |
| **Language constructs** | `state`, `bind`, `action`, `view` |
| **Entrypoint** | `start.llux` |
| **Root view** | `RootView` |
| **Default UI engine** | `dump` |
| **Compiler** | C, with TCC/Clang/GCC/Zig detection |
| **Architecture** | Intent -> Resolver -> Implementation -> Runtime |
| **Component model** | One component folder with `component.toml` |
| **Runtime direction** | Workspace with WCPS protocol |

### Dataflow Direction (Settled)

| Operator | Purpose | Status |
| :--- | :--- | :--- |
| `@key <- source` | Inbound stream | Settled |
| `@key <-> source` | Bi‑directional sync | Settled |
| `@key -> target` | Outbound stream | Settled |
| `key=value` | Static configuration | Settled |

`@` marks the component property as live and reactive. It belongs on the target.

## Phase 0 Focus

### Compiler and CLI

- [ ] Keep `llux` self-contained and offline-first.
- [ ] Parse the core `.llux` language.
- [ ] Generate C from the AST.
- [ ] Build through the best available local compiler.
- [ ] Stop on the first clear error.
- [ ] Support `--verbose` diagnostics for compiler internals.
- [ ] Keep `dump` as the zero-dependency UI engine.

### Language Stabilisation

- [ ] Stabilise the four core constructs: `state`, `bind`, `action`, `view`.
- [ ] Standardize explicit scopes: `app`, `session`, `component`.
- [ ] Standardize `start.llux` as the entrypoint.
- [ ] Standardize `RootView` as the root view name.
- [ ] Reconcile older examples that use `command`, `computed`, or `layout`.

### Website and Documentation

- [ ] Publish docs around `llux.org`.
- [ ] Keep public docs organised by `guide.how/`, `reference.what/`, `philosophy.why/`, `community.who/`, and `roadmap.when/`.
- [ ] Mark every major page as Implemented, Pre-release, Draft, or Historical.
- [ ] Ensure runnable examples match the current parser.
- [ ] Keep historical planning material separate from public launch pages.

---

## Creator-First Focus

Independence and autonomy are not afterthoughts. They are the foundation.

| Priority | Why It Matters |
| :--- | :--- |
| **Platform independence** | Creators must be able to run their software anywhere. |
| **Offline-first** | Creators must not depend on the internet to build or run. |
| **Zero dependencies** | Creators must not depend on others' code or services. |
| **Native binary** | Creators must own their executable. |
| **Plain source** | Creators must understand their own code. |

Every feature is evaluated against these priorities. If it does not serve the creator's independence, it does not belong.

---

## Next Planned Areas

| Area | Purpose |
| :--- | :--- |
| **Component manifests** | Add `component.toml` and one-component-per-folder packaging. |
| **Layout Markdown intent layer** | Use `.llux.md`/`.lmd` for intent, structure, semantics, and `@` Llux expressions. |
| **Resolver / Patchbay** | Resolve natural-language or layout intent into explicit `.llux`. |
| **Registry** | Store intent-to-implementation mappings for components, services, patterns, and design tokens. |
| **Workspace runtime** | Host-neutral execution surface for components and services. |
| **WCPS** | Worker protocol with deterministic JSON channels. |
| **Additional UI engines** | Add `tty`, `nuklear`, and `json` after `dump` is stable. |
| **Localisation** | Expand keyword maps, locale files, and translated diagnostics. |

## AI & Extensibility (Active Direction)

The following features are planned to complete the Transition Compass and universal bridge model:

| Feature | Description | Status |
| :--- | :--- | :--- |
| `llux suggest` | AI-driven pattern detection and recipe suggestions | Planning |
| `llux extract` | Extract a formal contract from a surface | Planning |
| `llux prepare --for=team` | Generate developer handoff package | Planning |
| `llux apply <recipe>` | Apply pre‑built engine integrations (MQTT, SQLite, etc.) | Planning |
| `--target=html-static` | Zero‑JavaScript HTML export | Planning |
| `--target=html-dynamic` | Self‑contained interactive HTML prototype | Planning |
| Importer: SwiftUI | Translate SwiftUI source to `.llux.md` | Research |
| Importer: React | Translate React/JSX to `.llux.md` | Research |
| Exporter: React | Export Llux AST to React components | Research |
| Exporter: SwiftUI | Export Llux AST to SwiftUI source | Research |

The core compiler (lexer → parser → AST → C codegen) is already stable for basic programs. The work ahead is additive — building the AI layer and the import/export system without changing the existing foundation.

## Success Measures

| Measure | Target |
| :--- | :--- |
| Time to first successful build | Under 5 minutes |
| Distribution size | Under 40 MB |
| Offline behaviour | No network required |
| Default UI engine | Zero external dependencies |
| Error style | Clear location, specific cause, actionable help |
| Language accessibility | Plain names and multilingual keyword support |

## Governance

- MIT licence
- No geo-blocking
- No telemetry
- Contributors credited
- Free forever
- Additive changes wherever possible
