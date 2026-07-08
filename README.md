# Llux

**Domain:** [llux.org](https://llux.org)  
**Status:** Pre-release documentation

Llux is a UI-to-binary language and toolchain for describing interfaces in plain, explicit source and compiling them into local software. It is being designed from the recurring pain points and strengths of existing UI systems: declarative UI, native toolkits, browser-based front ends, low-level portability, documentation formats, and multilingual developer workflows.

It is designed for designers, built for developers, and structured so AI systems can read, transform, explain, and generate it reliably.

> UI -> binary. Plain names. Kind errors. Offline-first.

The aim is not to replace one framework with another layer of ceremony. Llux is intended to make interface logic, layout intent, build output, and error feedback legible enough that more people can participate in software creation without giving up the control expected by experienced engineers.

This repository is the public documentation and website workspace for Llux. It is being organised to the standard expected of a serious programming-language project: clear first steps, accurate references, explicit status labels, and a credible path from first example to production-quality work.

---

## Current Project Shape

| Path | Purpose |
| :--- | :--- |
| [`guide.how/`](guide.how/) | Tutorials and task-oriented guides. |
| [`reference.what/`](reference.what/) | Language, platform, ecosystem, and layout references. |
| [`philosophy.why/`](philosophy.why/) | Working philosophy and human-centred design material. |
| [`community.who/`](community.who/) | Contributing, governance, and community process. |
| [`roadmap.when/`](roadmap.when/) | Roadmap and project status. |

---

## Start Here

- New to Llux: read [`guide.how/quickstart.md`](guide.how/quickstart.md).
- Want the language model: read [`reference.what/language.md`](reference.what/language.md).
- Want the project direction: read [`roadmap.when/index.md`](roadmap.when/index.md).
- Want the values: read [`philosophy.why/index.md`](philosophy.why/index.md).
- Want to help: read [`community.who/contributing.md`](community.who/contributing.md).
- Want licensing terms: read [`LICENCE.md`](LICENCE.md).

---

## Current Scope

The core toolchain currently exposes a `llux` CLI and a C-based compiler layout. Basic examples, keyword and localisation docs, and build scripts exist in the implementation workspace.

The active language direction is:

```llux
app state {
    count = 0
}

bind double = app.count * 2

action Increment(amount = 1) {
    app.count += amount
}

view RootView {
    Panel {
        Label { text: "Count: " + app.count }
        Button { label: "+1"; action: Increment(1) }
    }
}
```

The first stabilisation target is a local compiler pipeline with the zero-dependency `dump` UI engine. Translators for SwiftUI, Qt/QML, HTML, React, and other UI systems are planned work, not yet shipped functionality.

The public project name is **Llux**.

---

## Who This Is For

Llux should be of interest to:

- UI engineers who like declarative systems but want clearer build artefacts and fewer runtime assumptions.
- Native and embedded developers who want interface code without a browser stack.
- SwiftUI, Qt/QML, GTK, React, and HTML practitioners interested in translation paths between UI descriptions.
- Documentation, Markdown, and structured-authoring communities interested in layout and intent expressed in plain text.
- Localisation contributors who want programming tools that do not assume English-first source code.
- Educators and tool builders who care about readable examples, kind diagnostics, and offline access.

---

## Licence

The Llux implementation is intended to use the MIT licence. The website, specifications, research, and explanatory documentation use separate documentation terms so the authoritative language material remains clear and controlled. See [`LICENCE.md`](LICENCE.md).
