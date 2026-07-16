# Llux Platform & Runtime Reference

**Status:** Active draft  

This page records the current platform direction. Earlier drafts emphasised direct native/Nuklear output; the active plan starts with a zero-dependency `dump` UI engine and grows toward additional engines and hosts.

## Compiler Model

Llux is implemented as a local compiler toolchain:

```text
source -> lexer -> parser -> AST -> C codegen -> local compiler -> output
```

Compiler detection should prefer the best available local option among TCC, Clang, GCC, and Zig, while keeping the project offline-first and self-contained.

## UI Engine Policy

The generated code should call an abstract `ui_*` interface. The selected UI engine provides the implementation.

| Engine | Purpose | Dependencies | Status |
| :--- | :--- | :--- | :--- |
| `dump` | Print the UI tree to stdout. | None | Phase 0 |
| `tty` | Full console UI. | ncurses or equivalent | Planned |
| `nuklear` | Desktop GUI. | GLFW or platform backend | Planned |
| `json` | Machine-readable UI output. | None | Planned |

The default is `dump` because it validates the full parser, code generation, and build pipeline without adding graphical dependencies.

## Build Targets

| Target | Mode | Purpose | Dependencies |
| :--- | :--- | :--- | :--- |
| `native-binary` | Default | OS-level execution (`.so`/`.dylib`/`.dll` + `.h`) | TCC/GCC/Clang |
| `html-static` | Export | Documentation, design review, PDF generation | None |
| `html-dynamic` | Export | Interactive prototypes, user testing | None (self-contained JS) |
| `react` | Export | React component library | Planned |
| `swiftui` | Export | SwiftUI source | Planned |
| `qt-qml` | Export | Qt/QML source | Planned |
| `embedded-firmware` | Export | Bare-metal microcontroller targets | Planned |

The default target is `native-binary`. HTML exports are optional — they exist for documentation, prototyping, and sharing, not as the primary runtime.

## Integration Targets under consideration

| Target | Purpose | Status |
| :--- | :--- | :--- |
| `core-wasm` | Portable logic/runtime. | Planned |
| `browser-js` | Browser shell. | Planned |
| `tauri-desktop` | Desktop shell. | Planned |
| `python-service` | Backend/service integration. | Planned |
| `static-asset` | Layout-only output. | Planned |

## Import / Export Architecture

The compiler uses a canonical AST as its intermediate representation. Importers translate foreign source formats into this AST; exporters translate the AST into target formats.

| Direction | Formats | Status |
| :--- | :--- | :--- |
| Import | SwiftUI, React/JSX, HTML, Qt/QML, XAML | Planned |
| Export | Native (C), html-static, html-dynamic, React, SwiftUI, Qt/QML | Planned |

The import/export system is designed to be **pluggable** — new formats can be added without modifying the core compiler. This keeps the core lean, offline, and dependency-free while enabling broad ecosystem compatibility.

## Runtime Direction

The planned runtime model is a host-neutral workspace where components communicate through declared capabilities instead of direct coupling.

Lifecycle:

1. create
2. initialise
3. execute
4. suspend
5. resume
6. terminate
7. recover

## WCPS

WCPS is the planned universal worker protocol. It uses JSON payloads over deterministic channels:

| Channel | Purpose |
| :--- | :--- |
| `STA` | State |
| `PRG` | Progress |
| `DAT` | Data |
| `DON` | Done |
| `ERR` | Error |
| `LOG` | Log |
| `PON` | Ping/pong or liveness |

## Import / Transduction Sources

Importers remain planned design work. They should preserve structure, state, and actions where possible while dropping framework-specific implementation detail.

| Source | Status | Intended output |
| :--- | :--- | :--- |
| HTML | Planned | `.llux` / `.llux.md` |
| React / JSX | Planned | `.llux` / `.llux.md` |
| SwiftUI | Planned | `.llux` / `.llux.md` |
| XAML | Planned | `.llux` / `.llux.md` |

## Versioning Rule

Changes should be additive wherever possible. If a feature must be deprecated, public docs should mark it clearly and preserve older context outside the launch-facing pages.
