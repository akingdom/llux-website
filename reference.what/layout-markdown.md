# Llux Layout Markdown Specification

**Home**: [https://github.com/akingdom/llux-layout-markdown](https://github.com/akingdom/llux-layout-markdown)

**Author**: Andrew Kingdom on behalf of the Llux community

**Version**: 1.0 Draft 1

**Status**: Draft specification. Standardization and reference implementation work are planned.

---

*This specification is written in the language it describes.*

::: grid cols-2 gap-6
  ::: main

## Abstract

Llux Layout Markdown is a meta-extension to CommonMark.

It adds two capabilities that Markdown lacks:

- **Meaning** — semantic roles, language tags, identifiers, metadata links, intent comments
- **Layout** — grids, flex containers, pages, sections, sidebars, figures, UI components

Both are provided through the same familiar `:::` fence pattern.

```
::: flex gap-4
  Left
  Right
:::
```

The `:::` delimiter is familiar from admonitions (`:::info` in MkDocs, Obsidian). Code blocks use triple backticks—a separate convention. Every CommonMark document remains valid. Every Llux document remains readable in any Markdown renderer. You only use `:::` when you need meaning or layout.

**You already know 80% of it. The other 20% solves problems you've been solving with hacks.**

---

## Audience

| User | Need |
|------|------|
| **Writers** | Footnotes, columns, pagination |
| **Designers** | Layouts sketched in plain text |
| **Developers** | Version-controlled, AI‑friendly prototypes |
| **Governments** | Standardised, accessible, multilingual documentation |
| **Educators** | Inclusive, interoperable learning materials |
| **Enterprises** | Documents that AI can understand |
| **Anyone** | Layout and meaning in plain text, without leaving Markdown |

---

## Design Goals

1. **Minimalism** — Add only what is necessary for meaning and layout.
2. **Determinism** — No hidden state. No implicit behaviour. What you write is what renders.
3. **Accessibility** — Heading hierarchy, alt text, table headers are mandatory.
4. **Interoperability** — Every CommonMark document is valid. Works with existing tools.
5. **Zero hidden state** — No directives that "persist until changed." Every container is explicit.
6. **Backward compatibility** — Existing Markdown documents work unchanged.

---

## Non‑Goals

Llux is not:

- A replacement for HTML
- A styling language (CSS remains the styling layer)
- A scripting language (no logic, conditionals, loops)
- A rendering engine (rendering is implementation-defined)
- A full UI framework (interactive components are extensions)
- A semantic markup language for complex documents (LaTeX/DocBook are better suited)

---

## Compatibility Notes

| System | Relationship to Llux |
|--------|---------------------|
| **CommonMark** | Llux is a superset. All CommonMark documents are valid. |
| **Pandoc Fenced Divs** | Similar concept; different syntax (`:::` vs `:::div`). Pandoc uses `::: {.class}`; Llux uses `::: type attributes`. |
| **MyST Directives** | MyST uses `:::` with colon-separated namespaces. Llux uses a similar visual pattern. |
| **Obsidian Admonitions** | Obsidian uses `:::info`. Llux uses the same `:::` opening, but requires a type (`:::flex`, `:::grid`). Plain `:::` with no type is invalid. |
| **VitePress/MkDocs** | Both already support `:::` admonitions. Llux extends this pattern to layout. |

---

## Core Syntax

### Container Pattern

All layout containers use the same pattern:

```markdown
::: [type] [attributes]
  content
:::
```

**Syntax Requirements**:

- There MUST be a space between `:::` and the type.
- `:::flex` (without space) is **invalid**.
- This matches code fences (```` ```python ````).

**Colon count**: A container is opened by `:::` or more colons (`::::`, `:::::`, etc.). The exact number carries **no semantic meaning**—only the presence of at least three consecutive colons matters. This allows intuitive nesting without a formal hierarchy.

### Parsing Decision

The parser looks at the first non-whitespace character after `:::`:

| First Character | Interpretation | Behaviour |
|-----------------|----------------|----------|
| Letter (a-z) | Container | Push frame |
| `!` | Intent comment | No frame |
| `[` | Metadata key or key-value | No frame |
| Anything else | Invalid | Error |

### Container Frames

Each `:::` opening pushes a frame onto the stack. Each `:::` closing pops the most recent frame.

```markdown
::: flex             ← Frame 1 (flex)
  ::: grid cols-2    ← Frame 2 (grid)
    Card A
    Card B
  :::                ← Pop Frame 2 (grid closes)
:::                  ← Pop Frame 1 (flex closes)
```

### Comments

```markdown
::: ! This is an intent comment. It will not be rendered.
```

Comments begin with `::: !` followed by text. There MUST be a space after `:::` and before `!`. Comments are single-line only.

### Metadata Keys and Key-Value Pairs

```markdown
::: [timing]                    ← Key only (label/definition)
::: [duration](3.5s)            ← Key-value pair
```

**Rules**:

- `::: [label]` → Stores `label` as metadata on the parent container (no value).
- `::: [label](value)` → Stores `label: value` as metadata on the parent container.
- The `value` can be any token (string, number, path, URL, JSON, etc.).
- If the value contains `)` or other special characters, it should be encoded.

**Use Cases**:

- Timing: `::: [duration](3.5s)`
- Schedule: `::: [schedule](daily@9am)`
- Type: `::: [event]`
- Status: `::: [status](pending)`
- Schema: `::: [schema](person-schema.json)`
- Config: `::: [config]({"key":"value"})`

---

## Document Metadata

### The `---` Block

Document metadata is delimited by `---` at the top of the document.

**Rules**:

- MUST be the first block in the document.
- MUST have an identifier (optional, defaults to YAML).
- MUST close with `---`.
- Whitespace after `---` is optional and consumed.

**Identifiers**:

| Identifier | Format | Example |
|------------|--------|---------|
| `--- yaml` | YAML | `title: My Document` |
| `--- json` | JSON | `{"title": "My Document"}` |
| `--- toml` | TOML | `title = "My Document"` |
| `---` | Defaults to YAML | `title: My Document` |

**Example**:

```yaml
--- yaml
title: Llux Layout Markdown Specification
author: Andrew Kingdom
lang: en
design:
  colors:
    primary: "#3B82F6"
---
```

### Position Rule

`---` is metadata **only** at the top of the document. Anywhere else, it is a thematic break.

```yaml
--- yaml
title: My Document
---

# Content

---          # Thematic break (not metadata)

More content.
```

---

## Layout Containers

### Flex

```markdown
::: flex gap-4
  ::: flex-1
  First column
  :::
  ::: flex-1
  Second column
  :::
:::
```

### Grid

```markdown
::: grid cols-3 gap-2
  Card A
  Card B
  Card C
:::
```

**Implicit items**: If you omit nested `:::` for items, each **top-level block element** (paragraph, heading, list, code block, blockquote) becomes a separate item.

```markdown
::: flex gap-4
  This is an implicit item (paragraph).
  # This is an implicit item (heading).
  - This is an implicit item (list).
:::
```

### Nesting

Containers nest naturally. Each `:::` opens a scope; the matching `:::` closes it.

```markdown
::: grid cols-2
  ::: flex gap-2
    Item 1
    Item 2
  :::
  ::: flex gap-2
    Item 3
    Item 4
  :::
:::
```

### Attribute Parsing

When parsing `::: type [attributes]`:

- Tokens starting with `#` → ID (only first applies)
- Tokens starting with `.` → CSS class (all accumulate)
- Tokens containing `=` → key-value attribute (last wins)
- Other tokens → utility classes (last wins)

**Example**:

```markdown
::: card #user-profile .shadow-lg bg-muted p-4 lang="en"
```

- Type: `card`
- ID: `user-profile`
- Classes: `shadow-lg`, `bg-muted`, `p-4`
- Attributes: `{ lang: "en" }`

**Whitespace in attributes**: Quoted values (`lang="en-US"`) may contain spaces. Unquoted values cannot.

### Empty Containers

```markdown
::: spacer
:::
```

Empty containers are valid. They render as empty elements.

---

## Page and Flow Layouts

### Page Boundaries

```markdown
::: page new
# Chapter 2
:::
```

Additional attributes:

```markdown
::: page new number=3 orientation=landscape
```

**Containment**: `page` can contain any layout container. Layout containers (`flex`, `grid`, `sidebar`) **cannot** contain `page`. If `page` appears inside a layout container, it breaks out.

### Chapters and Sections

```markdown
::: chapter introduction
# Chapter 1: Introduction
:::

::: section background
## Background
:::
```

Semantic markers for table of contents and navigation.

### Sidebars and Callouts

```markdown
::: sidebar width=1/3 bg-muted p-4
This is a sidebar note.
:::

::: callout type=warning
This is a warning callout.
:::
```

---

## UI Components

UI components use the same `:::` fence pattern:

```markdown
::: card title="User Profile" shadow hover-scale
  This is card content.
:::
```

**Mixed content**: Cards may contain text and explicit items. Text before the first explicit item becomes an implicit item.

**Interactive components** (buttons, tabs, accordions) are **extensions** (see Appendix J). They are not part of the core specification.

---

## Typography and Semantics

### Headings

Standard Markdown headings (`#`, `##`, `###`) are preserved. **Heading hierarchy is required** (WCAG 2.1 Success Criterion 1.3.1).

```markdown
# Chapter 1
## Section 1.1
### Subsection
```

### Footnotes

```markdown
This is a sentence with a footnote.[^1]

[^1]: This is the footnote text.
```

By default: bottom of page (PDF) or end of document (HTML). Override with:

```markdown
::: page new footnotes="bottom"
```

### Tables

```markdown
| Name | Age | Role |
|------|-----|------|
| Alice | 30 | Editor |
| Bob | 25 | Reviewer |

Caption: Team members
```

Caption appears **above** by default. Override with `caption-position="bottom"`.

### Inline Styling

```markdown
This text is [highlighted yellow]{bg-yellow-200} and [larger]{text-xl}.
```

**Specificity**: Inline styles override container-level utility classes, which override design tokens.

---

## Accessibility

Accessibility is **mandatory**.

### Validation Rules

| Rule | Description |
|------|-------------|
| Heading hierarchy | No skipping levels |
| Image alt text | All images must have alt text |
| Table headers | All tables must have headers |
| Layout order | Must follow document order |
| ID uniqueness | All IDs must be unique |
| Custom type | May be used without declaration (warning) |
| Empty type | No plain `:::` without a type |
| UTF-8 validity | Invalid UTF-8 sequences error |

### Validation

Validation is **mandatory** and **non-optional**. If a document fails validation, the renderer MUST produce a clear error message with line number, and MUST NOT render.

```markdown
Error: Heading level skipped (line 23)
  Section 6.1 requires that heading hierarchy is logical.
  Found: ### Subsection (line 23)
  Expected: ## Section or higher.
```

A `--force` flag MAY be provided for emergency use, strongly discouraged.

---

## Multi-Language Support

### Language Attributes

```markdown
::: grid cols-2 gap-4
  ::: lang-en
  This is the English text.
  :::
  ::: lang-fr
  Ceci est le texte français.
  :::
:::
```

### Bidirectional Text

```markdown
::: lang-ar dir-rtl
النص العربي
:::
```

### Use Case: NATO STANAGs

```markdown
::: page
::: grid cols-2 gap-4
  ::: lang-en role-main
  [English text]
  :::
  ::: lang-fr role-translation
  [French text]
  :::
:::
:::
```

---

## Design Tokens

Defined in YAML frontmatter:

```yaml
---
design:
  colors:
    primary: "#3B82F6"
    background: "#F9FAFB"
    muted: "#F3F4F6"
  fonts:
    heading: "Inter, sans-serif"
    body: "Merriweather, serif"
  spacing:
    default: "1.5rem"
    gap: "1rem"
---
```

---

## Architecture

### Components

::: flex gap-4
  ::: flex-1 bg-muted p-4 rounded
    **1. Parser**
    Reads Markdown; emits an AST with layout nodes.
  :::
  ::: flex-1 bg-muted p-4 rounded
    **2. Transformer**
    Applies design tokens; validates accessibility.
  :::
  ::: flex-1 bg-muted p-4 rounded
    **3. Renderer**
    Generates HTML, PDF, PNG, or SVG.
  :::
:::

### Compatibility

- **CommonMark**: Every CommonMark document is valid.
- **Markdown-it**: Plugin planned.
- **Pandoc**: Reader/writer planned.
- **Obsidian**: Community plugin planned.
- **VS Code**: Extension planned.

---

## Appendix A: Extensibility Methodology

### Core + Custom Contract

Core types: `page`, `chapter`, `section`, `flex`, `grid`, `item`, `sidebar`, `callout`, `card`, `figure`.

Any other type is **custom**. Custom types may be used without declaration, producing a **warning**.

```markdown
Warning: Undeclared custom type 'video' (line 12)
  Consider adding 'video' to 'extensions' in frontmatter.
  Using 'video' as a generic container.
```

### Vendor Namespacing

```markdown
::: acme/video src="..." :::
::: oss/slideshow interval="3" :::
```

Namespaces registered in a **Git‑based registry**. Open to all.

### The `use` Directive

```markdown
::: use video, slideshow :::
```

### Renderer Behaviour

- **Strict mode** (print/PDF): Unknown types error.
- **Loose mode** (prototyping): Unknown types fall back to `div` with `data-type`.

---

## Appendix B: Technical Specification (Parser Rules)

### Lexical Grammar

```
container = opening, content, closing
opening   = <line_start>, ":::", whitespace, type, [whitespace, attributes], <line_end>
closing   = <line_start>, ":::", [whitespace], <line_end>
type      = [a-zA-Z][a-zA-Z0-9\-]* (with optional namespace: [a-z]+"/")
comment   = <line_start>, ":::", whitespace, "!", [whitespace, text], <line_end>
key       = <line_start>, ":::", whitespace, "[", text, "]", <line_end>
keyvalue  = <line_start>, ":::", whitespace, "[", text, "]", "(", text, ")", <line_end>
```

**Unicode Safety**: Parser looks only for ASCII colons and whitespace. All other content passes through.

**Line Start**: Container opens with `:::` at line start, after up to three spaces of indentation.

**Precedence**:

- Code blocks use triple backticks (```` ``` ````). No lexical overlap.
- Thematic breaks are `---` or `***` on their own line. `---` followed by text is literal.
- Admonitions use `:::` but require a type. Plain `:::` with no type is invalid.

### Parsing Algorithm

1. Read line.
2. If line matches `^[ ]{0,3}:::$` (closing):
   - If inside container, close it.
   - Else, error.
3. If line matches `^[ ]{0,3}::: +[a-zA-Z]` (opening):
   - Extract type.
   - If type not core and not declared in `extensions`, warn (loose) or error (strict).
   - Push container frame onto stack.
4. If line matches `^[ ]{0,3}::: +!` (comment):
   - Consume remainder as comment.
5. If line matches `^[ ]{0,3}::: +\[` (key/key-value):
   - Parse `[label]` or `[label](value)`.
6. Else:
   - If inside container, append to content buffer.
   - Else, treat as standard Markdown block.

### Container Frame Structure

```
frame = {
  type: string,
  attributes: object,
  content: string,
  line_start: number,
  metadata: object   // Stores comments, keys, key-values attached to this container
}
```

### Regular Expressions (Unicode-Safe)

```
Opening: ^[ ]{0,3}:::[ \t]+([a-zA-Z][a-zA-Z0-9\-]*(?:\/[a-zA-Z][a-zA-Z0-9\-]*)?)
Closing: ^[ ]{0,3}:::[ \t]*$
Comment: ^[ ]{0,3}::: +!
Key:     ^[ ]{0,3}::: +\[
```

---

## Appendix C: ID Strategy

### Explicit ID

```markdown
::: page #executive-summary
```

### Automatic Fallback

1. First heading inside
2. Sanitised first few words
3. Counter (`container-1`)

### Cross-Referencing

```markdown
See the [executive summary](#executive-summary).
```

### Role Attributes

Follow WAI-ARIA 1.2. Custom roles prefixed with `x-`.

| Container | Default Role |
|-----------|--------------|
| `flex`, `grid` | `group` |
| `sidebar` | `complementary` |
| `callout` | `note` |
| `card` | `article` |
| `figure` | `figure` |
| `page`, `chapter`, `section` | `region` |

---

## Appendix D: Keyboard Accessibility

The colon (`:`) is universally accessible:

| Layout | `:` Key | Ease |
|--------|---------|------|
| US QWERTY | `Shift` + `;` | 🟢 |
| UK QWERTY | `Shift` + `;` | 🟢 |
| German QWERTZ | `Shift` + `.` | 🟢 |
| **French AZERTY** | **Direct key** | 🟢 **Easiest** |
| Spanish | `Shift` + `.` | 🟢 |
| Nordic | `Shift` + `.` | 🟢 |
| Japanese | `Shift` + `;` | 🟢 |

**No layout requires AltGr, dead keys, or other problematic mechanisms.**

---

## Appendix E: Utility Classes Reference

| Pattern | Purpose | Example |
|---------|---------|---------|
| `gap-{n}` | Gap between items | `gap-4` |
| `cols-{n}` | Grid columns | `cols-3` |
| `flex-{n}` | Flex grow factor | `flex-2` |
| `p-{n}` | Padding | `p-4` |
| `bg-{color}` | Background | `bg-muted` |
| `rounded` | Rounded corners | `rounded` |
| `text-{size}` | Text size | `text-xl` |
| `shadow` | Box shadow | `shadow` |
| `hover-scale` | Hover scale | `hover-scale` |
| `justify-{value}` | Flex justify | `justify-center` |
| `text-center` | Text alignment | `text-center` |
| `w-{n}` | Width | `w-full` |

---

## Appendix F: Full Directive Reference

| Directive | Purpose | Example |
|-----------|---------|---------|
| `---` | Document metadata | `--- yaml` |
| `::: flex` | Flex container | `::: flex gap-4` |
| `::: grid` | Grid container | `::: grid cols-3` |
| `::: page` | Page boundary | `::: page new` |
| `::: chapter` | Chapter marker | `::: chapter introduction` |
| `::: section` | Section marker | `::: section background` |
| `::: sidebar` | Sidebar | `::: sidebar width=1/3` |
| `::: callout` | Highlighted block | `::: callout type=warning` |
| `::: card` | Card component | `::: card title="Profile"` |
| `::: figure` | Figure | `::: figure src="..."` |
| `::: item` | Child item | `::: item flex-1` |
| `::: use` | Extension declaration | `::: use video, slideshow` |
| `::: !` | Intent comment | `::: ! TODO: Add figure` |
| `:::` | Metadata key | `::: [timing]` |
| `:::` | Metadata key-value | `::: [duration](3.5s)` |

---

## Appendix G: This Document as a Style Guide

This document demonstrates every feature it specifies:

| Feature | Location |
|---------|----------|
| `--- yaml` | Document metadata (frontmatter) |
| `::: grid cols-2` | Abstract and sidebar |
| `::: flex` | Architecture section |
| `::: page` | Page breaks between chapters |
| `::: chapter` | Major section markers |
| `::: section` | Sub-section containers |
| `::: sidebar` | At-a-glance summary |
| `:::` with `#` IDs | Every page has an ID |
| `lang` attributes | Multi-language section |
| Design tokens | Frontmatter |
| Utility classes | Throughout |
| Accessibility | Section 6 validates itself |
| Extensibility | Appendix A defines the mechanism |

**If you can read this, you can write it.**

---

## Appendix H: Licence and Governance

### Specification Licence

The specification text follows the Llux documentation/specification terms. See [`../LICENCE.md`](../LICENCE.md).

### Reference Implementation Licence

Reference implementation code is intended to use the MIT licence unless a file states otherwise.

### Governance

The Llux Layout Markdown specification is governed by the **Llux community**—developers, users, and contributors to the Llux programming language project.

1. **Open contribution**: Anyone may propose changes.
2. **Public review**: All significant changes undergo review.
3. **Stakeholder input**: Input from all users, including outside the Llux ecosystem.
4. **Formal standardization**: evaluate appropriate standards paths after implementation experience.

No single entity controls the specification. It belongs to the community.

### Disclaimer

This specification is provided "as is", without warranty of any kind.

---

## Appendix I: Relationship to the Llux Programming Language

This specification originated within the Llux programming language project and is fully implemented in the Llux standard library. However, the specification is **independent** and can be implemented in any language.

The Llux implementation provides:

- Native parsing and rendering
- Template integration
- Compile-time validation
- Accessibility checking

**The specification stands alone and is not dependent on Llux.**

---

## Appendix J: UI Components (Extension)

This appendix defines optional UI component extensions. These are not part of the core specification.

### Component Declaration

```markdown
::: button variant="primary" size="lg"
  Click Me
:::
```

### Component Types

| Component | Purpose | Example |
|-----------|---------|---------|
| `button` | Clickable button | `::: button variant="primary"` |
| `input` | Text input | `::: input type="text"` |
| `select` | Dropdown | `::: select options="Option 1, Option 2"` |
| `tabs` | Tabbed interface | `::: tabs` |
| `accordion` | Expandable sections | `::: accordion` |
| `form` | Form container | `::: form action="/submit"` |
| `checkbox` | Checkbox | `::: checkbox label="Accept"` |
| `radio` | Radio group | `::: radio group="options"` |

### Component Attributes

| Attribute | Purpose | Example |
|-----------|---------|---------|
| `variant` | Visual style | `variant="primary"` |
| `size` | Size | `size="lg"` |
| `disabled` | Disabled state | `disabled` |
| `loading` | Loading state | `loading` |
| `onclick` | Click handler | `onclick="submit()"` |
| `type` | Input type | `type="email"` |
| `placeholder` | Input placeholder | `placeholder="Enter email"` |
| `options` | Select options | `options="Option 1, Option 2"` |

### Render Behaviour

Implementations MAY render components as:

- Static HTML
- Interactive HTML (with JavaScript)
- Wireframe placeholder
- Documentation/prose

### Relationship to Core

UI components are **extensions**. Implementations that support them MUST:

- Use the same `:::` fence pattern
- Use the same attribute parsing
- Be backward-compatible

Implementations that do not support UI components SHOULD:

- Render them as unstyled text (graceful degradation)
- Not throw errors (warnings acceptable)

---

## End of Specification
