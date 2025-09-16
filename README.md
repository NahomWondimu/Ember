# Ember 🔥
_A hand-rolled, security-minded language and toolchain project_

## Overview
Ember is a small programming language and runtime that I’m building entirely **from scratch** to maximize learning and depth for future systems programming and interview prep.

Phase 1 focuses on creating all the core compiler and runtime components by hand:

- Lexer / tokenizer
- Pratt or recursive-descent parser + AST
- Monomorphic type checker
- IR + bytecode format and emitter
- VM runtime with an initial mark-sweep garbage collector

The goal is to understand every line deeply — enough to be able to rebuild the system from memory within 24 hours.

---

## Design Goals
- **Security-minded**: capability-gated I/O, gas metering, and taint tracking (VM-level, not part of grammar yet).
- **Transparency**: all decisions logged in `devlog.md`, all grammar/spec in `spec_v1.md`.
- **No shortcuts**: AI may explain, critique, or generate tests, but not implement core systems.

---

## Language Snapshot (v1 Spec)
- C-flavored surface syntax, hand-written grammar
- Core features:
  - Functions (`fn`)
  - Variables (`let`)
  - Conditionals (`if/else`)
  - Loops (`while`)
  - Basic types: `Int`, `Bool`, `String`, `Null`, `Array<T>`
- Built-ins: `print(x)`, `len(x)`
- Example:

```ember
fn main() {
  let x = 5;
  print(x + 3);
}
```

---

## Development Process
- **Contract:** documented in [`docs/contract.md`](./docs/contract.md), defining strict self-rules for learning and attribution.
- **Dev Log:** updates in [`docs/devlog.md`](./docs/devlog.md) track resources, problems, takeaways, changes, and next steps.
- **Spec:** language definition lives in [`docs/spec_v1.md`](./docs/spec_v1.md).

---

## Current Status
- ✅ Grammar v1 complete (`spec_v1.md`)
- 🚧 Lexer development in progress
- 📝 Next: finish lexer, start parser

---

## Learning Principles
Before committing code:
- Can I explain every line and invariant?
- Can I rebuild it from scratch in 24 hours?
- Is it tested (unit/property/fuzz)?

---

## References
- [How to Build a New Programming Language](https://pgrandinetti.github.io/compilers/page/how-to-build-a-new-programming-language/)
- [EBNF Basics](https://ics.uci.edu/~pattis/ICS-33/lectures/ebnf.pdf)
- [Zig Language Grammar](https://ziglang.org/documentation/master/#Grammar)
