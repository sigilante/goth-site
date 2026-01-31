---
title: Variables and Bindings
---

# Variables and Bindings

## De Bruijn Indices

Goth uses **de Bruijn indices** for variable references. Variables are accessed by their binding depth, eliminating shadowing ambiguity.

| Syntax | Meaning |
|--------|---------|
| `₀` or `_0` | Most recently bound variable |
| `₁` or `_1` | Second most recent |
| `₂` or `_2` | Third most recent |

```goth
λ→ ₀              # identity: returns its argument
λ→ λ→ ₀ + ₁      # add: ₀ is inner arg, ₁ is outer arg
```

In multi-argument declarations, `₀` is the **last** (most recently bound) argument:

```goth
╭─ sub : ℤ → ℤ → ℤ
╰─ ₁ - ₀            # ₁ = first arg, ₀ = second arg (sub 10 3 = 7)
```

Let bindings shift indices:

```goth
╭─ example : ℤ → ℤ
╰─ let x = ₀ × 2 in    # ₀ = argument
   let y = ₀ + 1 in    # ₀ = x, ₁ = argument
   ₀ + ₁               # ₀ = y, ₁ = x, ₂ = argument
```

## Let Bindings

**Simple let:**

```goth
let x = 5 in x × x
# Result: 25
```

**Sequential bindings (with semicolons):**

```goth
let x ← 5 ;
    y ← x × 2 ;
    z ← y + 1
in x + y + z
# Result: 26
```

Both `=` and `←` work identically for bindings.

**With type annotation:**

```goth
let x : F = 5.0 in x × 2
let v : [3]F64 = [1.0, 2.0, 3.0] in v
```

## Recursive Bindings

`let rec` enables self-referencing and mutually recursive definitions:

```goth
let rec factorial ← λ→ match ₀
              0 → 1
              n → n × factorial(n - 1)
in factorial 5
# Result: 120
```

**Mutual recursion:**

```goth
let rec even ← λ→ match ₀
                0 → ⊤
                n → odd(n - 1) ;
        odd ← λ→ match ₀
                0 → ⊥
                n → even(n - 1)
in even 10
# Result: ⊤
```
