# Dev Log

## [2025-09-07] Status Update: Right before lexer work begins

**Resource(s):**

- [How to Build a new programming language](https://pgrandinetti.github.io/compilers/page/how-to-build-a-new-programming-language/)
  _Set the background for the project by describing the type of work involved and the pieces that make up a language and a compiler._
- [EBNF Logic and Basics](https://ics.uci.edu/~pattis/ICS-33/lectures/ebnf.pdf)
  _Research article and guide describing EBNF, it's origin, and application into developing the grammar of a language. Implemented into [[spec_v1.md]]_
- [ZigLang Grammar Sheet](https://ziglang.org/documentation/master/#Grammar)
  _Another programmer's grammar sheet used as a rough reference as to what a grammar sheet should look like._
  **Problem:** Grammar defining was tedious. AI helped with automating the process or defining syntax to model other low level languages (ex. rust or c).
  **Takeaways:**
- General: Planning is 90% of programming. The last 10 is implementation. Documenting and Research eased the learning and writing process.
- Technical: The value of most languages isn't their appearance of user experience. It is the details put into the backend (ex. rust is meant for low level and high speed development, java for cross platform capabilities).
  **Changes:**
- Developed version 1.0 of the specs (grammar of language) as seen in `docs/` folder.
  **Tests:**
- List new/updated tests; what invariant they check
  **Next:**
- Today: complete research of lexer and complete it's development; push first github repo entry.

---

# Template:

## [YYYY-MM-DD] Short title (e.g., “Lexer: string escapes crash”)

**Resource(s):** link(s) or “AI: prompt summary”
**Problem:** one sentence
**Takeaways:** 2–4 bullets
**Changes:** files/functions; brief rationale
**Tests:** list new/updated tests; what invariant they check
**Next:** 1–2 bullets (what I’ll do tomorrow)
