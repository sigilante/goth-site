---
title: Advanced Features
---

# Advanced Features

## Do-Notation

Chained operations on tensors:

```goth
do [1, 2, 3]
  ↦ λ→ ₀ × 2
  ▸ λ→ ₀ > 3
end
# Result: [4, 6]
```

**With let bindings:**

```goth
do [1, 2, 3, 4, 5]
  let x ← ₀ × 2
  ↦ λ→ ₀ + 1
end
```

**Inline operators:**

```goth
do [10, 20, 30]
  + 5
  × 2
end
# Result: [30, 50, 70]
```

## Cast Expressions

| Form | Syntax | Returns |
|------|--------|---------|
| Static | `expr as Type` | `Type` |
| Force | `expr as! Type` | `Type` |
| Try | `expr as? Type` | `Option<Type>` |

```goth
5 as! F                      # Force cast to Float
x as? String                 # Try cast, returns Option
```

## Modules

Each `.goth` file is a module. Import with `use`:

```goth
use "prelude.goth"
use "../stdlib/option.goth"
```

The `use` declaration takes a relative path and inlines all declarations into the current namespace.

### Standard Library Modules

| Module | Description |
|--------|-------------|
| `prelude.goth` | Core combinators (`id`, `const`, `flip`, `compose`) |
| `list.goth` | List/array operations |
| `math.goth` | Math functions with uncertainty propagation |
| `option.goth` | Generic Option (`some`, `none`, `mapOpt`, `flatMapOpt`) |
| `result.goth` | Generic Result (`ok`, `err`, `mapRes`, `flatMapRes`) |
| `string.goth` | String manipulation |
| `tui.goth` | Terminal UI (ANSI escapes, cursor, raw mode) |
| `crypto.goth` | SHA-256, SHA-1, MD5, HMAC, PBKDF2 |
| `random.goth` | Seeded PRNG (xorshift64) with state-passing |

## Random Number Generation

The `random.goth` module returns `⟨value, nextSeed⟩` tuples for explicit state threading:

```goth
use "stdlib/random.goth"

╭─ main : ℤ → [n]F64
╰─ let seed = entropy ⟨⟩
   in let ⟨vals, _⟩ = randFloats ₁ seed
   in vals
```

| Function | Signature |
|----------|-----------|
| `entropy` | `() → I64` |
| `randFloat` | `I64 → ⟨F64, I64⟩` |
| `randFloatRange` | `F64 → F64 → I64 → ⟨F64, I64⟩` |
| `randInt` | `I64 → I64 → I64 → ⟨I64, I64⟩` |
| `randBool` | `F64 → I64 → ⟨Bool, I64⟩` |
| `randNormal` | `I64 → ⟨F64, I64⟩` |
| `randGaussian` | `F64 → F64 → I64 → ⟨F64, I64⟩` |
| `randFloats` | `I64 → I64 → ⟨[n]F64, I64⟩` |
| `randInts` | `I64 → I64 → I64 → I64 → ⟨[n]I64, I64⟩` |
| `randNormals` | `I64 → I64 → ⟨[n]F64, I64⟩` |

## REPL

Start the REPL with `goth` (no arguments).

| Command | Short | Action |
|---------|-------|--------|
| `:help` | `:h`, `:?` | Show commands |
| `:type expr` | `:t` | Infer type |
| `:ast expr` | | Show parse tree |
| `:load file` | `:l` | Load and execute file |
| `:clear` | `:c` | Clear environment |
| `:quit` | `:q` | Exit |

Multi-line input continues automatically when delimiters are unbalanced or the line ends with an operator.

## CLI

```sh
goth                         # Start REPL
goth program.goth            # Run file
goth program.goth 5 10       # Run with arguments
goth -e 'Σ [1, 2, 3]'       # Evaluate expression
goth -c program.goth         # Type check only
goth --to-json program.goth  # Emit JSON AST
goth --from-json ast.json    # Run from JSON AST
```
