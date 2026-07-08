# Quick Start

**Status:** Pre-release. The core toolchain is under active development; the public quick-start flow is still being stabilised.

## Build the Tool

The intended source build flow is:

```bash
cd llux
./scripts/build.sh
```

The build should produce a local `llux` binary.

## Try an Example

The first public example should use the current language direction: `bind`, `action`, and `view RootView`.

## Intended Workflow

```bash
llux new my-app
cd my-app
llux build
llux run
```

The intended entrypoint is `start.llux`, and the intended root view name is `RootView`.

The command names are the public direction.
