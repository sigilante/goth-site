---
title: Types
---

# Type System

## Primitive Types

| Type | Description |
|------|-------------|
| `ℤ` | Integer (i128 at runtime) |
| `ℕ` | Natural number (i128 at runtime) |
| `I64`, `I32`, `I128` | Signed integers (all i128 at runtime) |
| `U64`, `U32`, `U128` | Unsigned integers (all i128 at runtime) |
| `F64`, `F32` | Floating point |
| `F` | Generic float (resolves to F64) |
| `Bool` | Boolean |
| `Char` | Unicode character |
| `String` | UTF-8 string |
| `()` | Unit type |

All integer types are stored as **i128** at runtime. The type distinctions exist for documentation and type checking. The standard library primarily uses `ℤ`, `F`, and `Bool`.

## Function Types

```goth
F → F                        # Float to Float
ℤ → ℤ → ℤ                   # Curried two-argument
(ℤ, ℤ) → ℤ                  # Uncurried pair
(F → F) → F → F             # Higher-order
```

Unicode arrow: `→` / ASCII: `->`

## Tensor Types

**Fixed dimensions:**

```goth
[3]F                         # Vector of 3 floats
[3 4]F64                     # 3×4 matrix
[2 3 4]ℤ                    # 2×3×4 tensor
```

**Shape variables:**

```goth
[n]F                         # Vector of n floats
[n m]F                       # n×m matrix
[n n]F                       # Square matrix
```

Shape checking catches dimension mismatches:

```goth
╭─ double : [n]ℤ → [n]ℤ
╰─ ₀ ↦ (λ→ ₀ × 2)          # OK: preserves shape
```

## Tuple and Record Types

```goth
⟨ℤ, F⟩                       # Pair
⟨x: F, y: F⟩                 # Record
```

## Variant Types

```goth
⟨Left α | Right β⟩           # Either
⟨Some α | None⟩              # Option
⟨Ok α | Err String⟩          # Result
```

## Polymorphic Types

Type variables are lowercase names:

```goth
α → α                        # Polymorphic identity
(α → β) → [n]α → [n]β       # Map signature
```

**Universal quantification:**

```goth
∀α. α → α                    # Identity
∀α β. α → β → α              # Const
∀n α. [n]α → ℤ               # Length
```

ASCII: `forall α. α → α`

## Option Types

```goth
F?                           # Optional float
[n]ℤ?                        # Optional vector
```

## Uncertain Types

**Value with uncertainty:**

```goth
F ± F                        # Float with uncertainty
10.5 ± 0.3                  # Concrete uncertain value
```

Uncertainty propagates automatically through arithmetic:

| Operation | Propagation |
|-----------|-------------|
| `(a±δa) + (b±δb)` | δ = √(δa² + δb²) |
| `(a±δa) × (b±δb)` | δ = \|a×b\| × √((δa/a)² + (δb/b)²) |
| `√(x±δx)` | δ = δx / (2√x) |
| `sin(x±δx)` | δ = \|cos(x)\| × δx |
| `exp(x±δx)` | δ = exp(x) × δx |
| `ln(x±δx)` | δ = δx / \|x\| |

Supported functions: `+`, `-`, `×`, `/`, `^`, `√`, `exp`, `ln`, `log10`, `log2`, `sin`, `cos`, `tan`, `asin`, `acos`, `atan`, `sinh`, `cosh`, `tanh`, `abs`, `floor`, `ceil`, `round`, `Γ`.

## Interval Types

```goth
F⊢[0..1]                     # Float in [0, 1]
ℤ⊢[1..100]                   # Integer in [1, 100]
```

## Refinement Types

```goth
{x : F | x > 0}              # Positive floats
{x : ℤ | x mod 2 = 0}        # Even integers
{arr : [n]F | n > 0}         # Non-empty arrays
```

> Refinement predicates are parsed but not solved at compile time.

## Effect Types

> Effect annotations are parsed and stored in the AST but **not enforced**. They serve as documentation.

```goth
□                            # Pure (no effects)
◇io                          # I/O effects
◇mut                         # Mutable state
◇exn                         # Exceptions
```

```goth
╭─ greet : () → ()
│  ◇io
╰─ print "Hello!"
```

## Type Ascription

```goth
5 : ℤ                        # Annotate literal
[1, 2, 3] : [3]ℤ            # Annotate array
let x : F = 5.0 in x × 2   # Annotate binding
```
