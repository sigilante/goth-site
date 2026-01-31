---
title: Functions
---

# Functions

## Lambda Expressions

**Single argument:**

```goth
λ→ ₀ + 1              # Increment
λ→ ₀ × ₀              # Square
λ→ if ₀ > 0 then ₀ else -₀   # Absolute value
```

**Multiple arguments (curried):**

```goth
λ→ λ→ ₀ + ₁           # Two arguments: add
λ→ λ→ λ→ ₀ + ₁ + ₂    # Three arguments: sum
```

**Multi-arg shorthand:**

```goth
λ³→ ₀ + ₁ + ₂         # Three-argument lambda
λ⁴→ ₀ × ₁ × ₂ × ₃     # Four-argument lambda
```

ASCII: `\->` for `λ→`

## Function Declarations

Declarations use box-drawing syntax:

```goth
╭─ square : ℤ → ℤ
╰─ ₀ × ₀
```

| Symbol | ASCII | Purpose |
|--------|-------|---------|
| `╭─` | `/-` | Function header |
| `│` | `\|` | Contract lines |
| `╰─` | `\-` | Function body |

**With contracts:**

```goth
╭─ safe_div : F → F → F
│  ⊢ ₀ ≠ 0
│  ⊨ abs(₀ × ₁ - ₂) < 0.0001
╰─ ₁ / ₀
```

**Example — z-score normalization:**

```goth
╭─ normalize : [n]F → [n]F
│  ⊢ len ₀ > 0
╰─ let arr ← ₀ ;
       μ ← sum arr / len arr ;
       σ ← √(sum ((arr ↦ (λ→ ₀ - μ)) ↦ (λ→ ₀ × ₀)) / len arr)
   in (arr ↦ (λ→ ₀ - μ)) ↦ (λ→ ₀ / σ)
```

## Function Application

```goth
(λ→ ₀ + 1) 5          # Result: 6
(λ→ λ→ ₀ + ₁) 3 4    # Result: 7
```

## Partial Application

All functions are curried. Applying fewer arguments than needed returns a partial application:

```goth
let add = λ→ λ→ ₀ + ₁ in
let add5 = add 5 in
add5 10
# Result: 15
```

## Recursive Functions

Functions can call themselves by name:

```goth
╭─ factorial : ℤ → ℤ
╰─ if ₀ ≤ 1 then 1 else ₀ × factorial (₀ - 1)
```
