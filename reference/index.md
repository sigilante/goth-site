---
title: Language Reference
---

# Language Reference

Goth v0.2.0 — complete syntax and semantics for the interpreted implementation.

## Contents

1. [Literals](literals/) — integers, floats, booleans, characters, strings
2. [Variables and Bindings](variables/) — de Bruijn indices, let bindings, recursive bindings
3. [Functions](functions/) — lambdas, declarations, application, partial application
4. [Operators](operators/) — arithmetic, comparison, logical, tensor, composition
5. [Data Structures](data-structures/) — arrays, tuples, records, variants
6. [Pattern Matching](pattern-matching/) — match expressions, all pattern forms
7. [Types](types/) — primitives, tensors, functions, polymorphism, uncertainty, effects
8. [Contracts](contracts/) — preconditions, postconditions, runtime checking
9. [Control Flow](control-flow/) — if/then/else, match, recursion
10. [Primitives](primitives/) — built-in functions: math, I/O, conversions, linear algebra
11. [Advanced Features](advanced/) — do-notation, casts, modules, REPL

## Notation

Throughout this reference:

- **Unicode** syntax is shown first, with **ASCII** alternatives noted
- Code blocks use `goth` syntax
- `₀`, `₁`, `₂` are de Bruijn indices (see [Variables](variables/))
- Type signatures use `→` for functions and `[n]` for tensor shapes
