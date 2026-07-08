# Contributing to Llux

Community guidelines

Contributions are welcome from people working in different languages, regions, disciplines, and technical environments.

---

## How to Contribute

### 1. Test the Tool
- Run `llux` on your hardware, especially low-RAM and older devices
- Report bugs with `llux doctor` diagnostics

### 2. Translate
- Add or improve keyword maps (`docs/keywords/*.toml`)
- Add or improve user string translations (`docs/locales/*.lang`)
- Translate error messages and documentation

### 3. Write an Adapter
- Support a new UI framework (React, Vue, Svelte, etc.)
- Write the adapter in Lua (no C required)
- Test with `llux test --adapter=...`
- Share via the registry

### 4. Add a Language Keyword Map
- Create `docs/keywords/your_lang.toml`
- Map every keyword to its equivalent in your language
- Test with `llux build --language=xx --keyword-map=...`

### 5. Write a Pipeline Script
- Create a Lua script that hooks into any stage
- Use `llux build --script=...`

### 6. Improve Documentation
- Fix typos, clarify explanations, add examples
- Website docs live in `guide.how/`, `reference.what/`, `philosophy.why/`, `community.who/`, and `roadmap.when/`
- Core implementation docs live with the compiler/toolchain source

### 7. Report Issues
- Use GitHub Issues
- Include your environment, steps to reproduce, and error messages

---

## Contribution Process

1. **Fork** the repository
2. **Create a branch** for your change
3. **Make your changes**
4. **Test** your changes locally
5. **Submit a pull request** with a clear description

---

## Code of Conduct

We are committed to fostering a welcoming, inclusive, and harassment‑free community.

- Be respectful and empathetic
- Focus on constructive feedback
- Celebrate contributions, not just code

---

## Recognition

Every contributor is credited in `llux --version`.

If you'd like to be credited, ensure your name is in the `CONTRIBUTORS` file or your pull request description.

---

## Questions?

Open a GitHub Discussion or issue — we're here to help.

Thank you for making Llux better for everyone.
