[![Llux illustration](media/llux-bg-8c6a08a3c58b.png)](media/llux-bg-8c6a08a3c58b.png)

Llux is a tool for independent creators.

It turns your interface ideas into native software that runs anywhere—without platform lock-in, hidden dependencies, or surprises.

You describe the intent. Llux compiles it to a binary. You own it.

---

Every interactive system—whether a smart-home dashboard, a CNC machine HMI, or a museum installation—follows the same pattern: **Surface ↔ Transit ↔ Engine**. Llux compiles the Surface and the Transit rules. You bring the Engine.

**No platform lock-in. No hidden dependencies. No surprises.**

---

## Current Project

**Status:** Pre-release documentation + pre-release early-to-mid alpha

**Documentation:** [llux.org](https://llux.org) 

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

> As Llux is *in early development*, the present focus is on building the central technical supports needed for upcoming design matters.

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

- Independent creators, entrepreneurs, and solo founders who want to build software that runs anywhere, without being tied to a single platform or ecosystem.
- UI engineers who like declarative systems but want clearer build artefacts and fewer runtime assumptions.
- Native and embedded developers who want interface code without a browser stack.
- SwiftUI, Qt/QML, GTK, React, and HTML practitioners interested in translation paths between UI descriptions.
- Documentation, Markdown, and structured-authoring communities interested in layout and intent expressed in plain text.
- Localisation contributors who want programming tools that do not assume English-first source code.
- Educators and tool builders who care about readable examples, kind diagnostics, and offline access.

---

## Licence

The Llux implementation is intended to use the MIT licence. The website, specifications, research, and explanatory documentation use separate documentation terms so the authoritative language material remains clear and controlled. See [`LICENCE.md`](LICENCE.md).
