Tags: [[Ember]]

# Ember Language — v1 Specification (Draft)

**Purpose:** Ember is a small, security-minded language designed to run on a custom hand-rolled compiler and VM. v1 focuses on a C-flavored surface while keeping the grammar simple enough to implement by hand. Security features (capability-gated I/O, gas metering, tainting) live in the runtime/VM and are **not** part of the v1 grammar.

**Contract Note:** This document is design-level. Core implementations (lexer, parser, type checker, IR, VM, GC) must be written by hand.

## 1. Source Files & Encoding

- File extension: `.em`
- Encoding: UTF-8 (ASCII identifiers in v1)
- Newlines: `\n` (other forms normalized by the lexer)

## 2. Lexical Structure

- **Whitespace:** spaces, tabs, newlines — ignored except as separators.
- **Comments:**
  - Line: `// ...` to end of line
  - Block: `/* ... */` (no nesting in v1)
- **Identifiers:** `[A-Za-z_][A-Za-z0-9_]*` (case-sensitive)
- **Keywords (reserved):**

```
fn let return if else while true false null
```

(May add: `print len` as built-ins, not keywords.)

- **Literals:**
- Integer (decimal): `0|[1-9][0-9]*`
- String: `"..."` with escapes `\" \\ \n \t \r`
- Bool: `true | false`
- Null: `null`
- **Operators & Punctuators:**

```
( ) { } [ ] , ; :
= == != < <= > >= + - * / % ! && ||
```

## 3. Tokens (Abstract)

```
IDENT, INT_LIT, STRING_LIT, BOOL_LIT(true/false), NULL_LIT
LPAREN RPAREN LBRACE RBRACE LBRACK RBRACK COMMA SEMI COLON
ASSIGN EQ NE LT LE GT GE PLUS MINUS STAR SLASH PERCENT BANG
ANDAND OROR
KEY_FN KEY_LET KEY_RETURN KEY_IF KEY_ELSE KEY_WHILE KEY_TRUE KEY_FALSE KEY_NULL
EOF
```

## 4. Operator Precedence & Associativity (high → low)

1. **Postfix**: call `f(a,b)`, index `a[i]` (left-assoc, chains allowed)
2. **Unary**: `!`, unary `-` (right-assoc)
3. **Multiplicative**: `* / %` (left-assoc)
4. **Additive**: `+ -` (left-assoc)
5. **Relational**: `< <= > >=` (left-assoc)
6. **Equality**: `== !=` (left-assoc)
7. **Logical AND**: `&&` (short-circuit)
8. **Logical OR**: `||` (short-circuit)
9. **Assignment**: statement-level only in v1 (`let name = expr;`)

## 5. Grammar (EBNF-ish)

### 5.1 Program & Declarations

```
program ::= (fnDecl | stmt)* EOF

fnDecl ::= "fn" IDENT "(" params? ")" block
params ::= IDENT ("," IDENT)*
block ::= "{" stmt* "}"
```

### 5.2 Statements

```
stmt ::= letDecl | exprStmt | returnStmt | ifStmt | whileStmt

letDecl ::= "let" IDENT "=" expr ";"
exprStmt ::= expr ";"
returnStmt ::= "return" expr? ";"

ifStmt ::= "if" "(" expr ")" block ("else" block)?
whileStmt ::= "while" "(" expr ")" block
```

---

_(Optional v1.1: assignment and index-set statements; see §10 Deferrals.)_

### 5.3 Expressions (Pratt/precedence)

---

## 6. Static Semantics (v1)

- **Types:** `Int`, `Bool`, `String`, `Null`, `Array<T>`, `Fn(T1,...,Tn)->T`
  - v1 omits `Float`; add later if needed.
- **Type Inference:** local inference for `let` bindings (monomorphic).
- **Function Types:** parameter count fixed; return type inferred from consistent `return` paths; if no `return`, type is `Null`.
- **Arrays:** literals must be homogeneous; `a[i]` requires `i : Int`; bounds checked at runtime.
- **Calls:** callee must be `Fn`; arity must match.
- **Name Resolution:** lexical (block) scope; shadowing allowed; functions introduce new scopes.

## 7. Runtime Model (Overview, not grammar)

- **Evaluation:** strict, left-to-right.
- **Short-circuit:** `&&`, `||` must short-circuit.
- **Built-ins (predeclared identifiers):**
  - `print(x) -> Null`
  - `len(x: String|Array<T>) -> Int`
- **Security posture (impl level):**
  - v1 grammar is neutral; **I/O requires capabilities** provided by the host VM. No ambient authority.
  - Gas metering/tainting are VM concerns added post-v1.

## 8. Diagnostics & Error Handling

- **Lexing Errors:** unexpected character, unterminated string/comment (report position).
- **Parsing Errors:** expected token X, got Y. Recovery: synchronize on `;` and `}`.
- **Type Errors:** unknown identifier; type mismatch; non-callable used as function; non-indexable used with `[]`; arity mismatch; heterogeneous array literal.
- **Runtime Traps (VM):** divide-by-zero, out-of-bounds, null deref (if introduced later).

## 9. Minimal Conformance Programs (Goldens)

**hello.em**

```ember
fn main() {
  let x = 5;
  print(x + 3);
}
```

**fib.em**

```
fn fib(n) {
	if (n <= 1) { return n; }
	return fib(n-1) + fib(n-2);
}
fn main() { print(fib(6)); }
```

---

# References

- [How to Build a new programming language](https://pgrandinetti.github.io/compilers/page/how-to-build-a-new-programming-language/)
