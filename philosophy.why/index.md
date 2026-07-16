# Llux Philosophy

## Working Philosophy (For Every User)

This is the mindset you should expect from every interaction with Llux — the compiler, the errors, the documentation, and the community.

### The Covenant

> **Be your own help: plain names, kind errors, clear intention.**

- **Plain names:** Keywords use everyday words: `state`, `action`, `view`, `bind`. Specialized terms are introduced only when they carry useful precision.
- **Kind errors:** Every error message teaches, supports, and offers a path forward. The compiler is a teacher, not a judge.
- **Clear intention:** The code you write says what you mean. The compiler helps you say it clearly.

### Kind Errors

Errors are not punishments. They are guidance.

```
error[E0003]: missing state name
  --> start.llux:13:7
   |
13 | state {
   |       ^
   |
   = help: try adding a name after `state`
   = example: state count = 0
```

Every error diagnoses the problem, teaches the concept, suggests a fix, and points to the location.

### Plain Names & Multilingual Support

The language is designed to reduce unnecessary symbolic overhead. Keywords can map to human languages such as Greek, Arabic, Hindi, and Spanish. See the [Multilingual guide](../guide.how/multilingual.md).

---

## Design Philosophy (For Language Designers & The Inquisitive)

This section covers the theoretical underpinnings and high-level architectural choices.

### Research Background

The [`HCO7 paper`](hco7.md) originated in the research work behind Llux. It proposes seven operations for Human-Centred Systems: Establish, Place, Find, Traverse, Reconfigure, Identify, and Signal.

HCO7 is included here because it explains part of the conceptual model behind Llux. It is not required reading for using the language, and it should be treated as a research framework for future human-centred system design rather than as a language specification.

### Sovereignty Compass

Every feature is evaluated against these principles:

| Principle | Question | Implementation |
| :--- | :--- | :--- |
| **Agency** | Does this reduce or expand developer choice? | Escape hatches, expert mode |
| **Asymmetry** | Does this work for Global South and North equally? | Offline, 4GB RAM, no geo-blocking |
| **Reciprocity** | Does this take without giving back? | Open source, free, contributors credited |

### Abstraction Layers

```
Human Intent (natural language, sketches, wireframes)
    │
    ▼
Llux Design (intent parser + registry matcher)
    │
    ▼
.llux (formal UI description)
    │
    ▼
Libllux (compiler, renderer, services)
    │
    ▼
Binary (native, WASM, library)
```

Each layer is a distinct entry point for different personas (designers, product managers, developers).

---

## AI as a Transition Compass

Llux is designed for creative exploration. The AI does not write your app for you — it watches, learns, and guides you so your prototype never becomes a dead-end.

The CLI provides a set of AI‑assisted commands that act as a **Transition Compass**:

| Command | What it does |
| :--- | :--- |
| `llux diagnose` | Scans your `.llux.md` and `.llux` files, detects patterns, and flags potential scaling issues. |
| `llux suggest` | Lists available recipes based on the diagnosis. |
| `llux apply <recipe>` | Applies the selected recipe (with a dry-run preview). |
| `llux explain <recipe>` | Generates a plain‑language explanation of the recipe, why it matters, and what it changes. |
| `llux watch` | Runs the AI Observer continuously in the background, offering suggestions as you work. |

### How the AI Helps Across Domains

| Domain | AI Role |
| :--- | :--- |
| **Creative / Solo Artist** | Generates rich mock data, suggests layout patterns, offers pre-built engine integrations (MQTT, SQLite, etc.). |
| **Enterprise / Team** | Detects contract drift, suggests performance throttling, generates developer handoff packages. |
| **Safety‑Critical** | Acts as a safety auditor — flags overlapping touch targets, validates constraints, enforces strict typing. |

The AI is not a black box. Every suggestion is accompanied by an explanation, and every recipe can be reviewed before it is applied.

(Aside: integration with AI of your choice is the ideal intent.)

---

## Related

- **Governance (12 Directives):** [`../community.who/governance.md`](../community.who/governance.md)
- **HCO7 Research Paper:** [`hco7.md`](hco7.md)
- **Formal References:** [`../reference.what/`](../reference.what/)
