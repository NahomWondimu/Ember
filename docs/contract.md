# Project Ember — Personal Development Contract (Phase 1)

**Purpose:** Build a small, security‑minded language and toolchain (lexer, parser, type checker, IR/bytecode, VM/GC) *by hand* to maximize learning and interview depth.

## 1) Core Rule
Everything I ship, I must **understand deeply** and be able to **rewrite from scratch** without external help.

## 2) Scope (Phase 1)
The following **must be original implementations** written by me:
- Lexer / tokenizer
- Parser (Pratt or recursive‑descent) + AST
- Type checker (v1 monomorphic)
- IR + bytecode format and emitter
- VM runtime + GC (initial mark‑sweep is fine)

> Phase 2 (optional, after Phase 1 works): I may compare or extend with ANTLR/lex/yacc/LLVM/JITs, clearly labeled as experiments.

## 3) AI Assistance (ChatGPT/Gemini/etc.)
**Allowed:**
- Concept explanations; error/diagnostic help
- Design critiques; invariants to test
- Test scaffolding, fuzz input generation, docs/diagrams
- Boilerplate (CLI args, logging, benchmarking harness)

**Not allowed:**
- Implementing any Phase‑1 core component above
- Architecture I cannot justify
- Pasting code I could not reproduce from scratch

## 4) Open Source (GitHub/Blogs/Code)
**Allowed:** Read for patterns; copy **small non‑core boilerplate** with attribution.
**Not allowed:** Copying significant logic (lexer/parser/type/IR/VM/GC) or forking a language and claiming progress.

## 5) Tutorials/Videos
**Allowed:** Watch for theory; pause and implement independently.
**Not allowed:** Line‑by‑line coding along; importing tutorial code for core systems.

## 6) Collaboration
Discuss concepts and request feedback. Do **not** accept code snippets > ~10 lines for core systems. If I do, I must rewrite them in my own words and tests.

## 7) Documentation & Transparency
Maintain `docs/spec_v1.md` and a `devlog.md` that records:
- Date, resource (link/name), problem, takeaway, changes made
- Tests added to prove understanding

## 8) Self‑Checks (before commit)
- Can I **explain every line** and the invariants?
- Could I **rebuild this** within 24 hours?
- Is it **tested** (unit/property/fuzz) and benchmarked if relevant?

## 9) Disclosure & Attribution
Credit external ideas/snippets in comments and `devlog.md`. If unsure, **over‑disclose**.

## 10) Enforcement
If I cannot re‑implement an AI‑influenced or copied piece within **24 hours**, I **revert** and rebuild it. No exceptions.

---
**Signature:** ____________________   **Date:** ____________
