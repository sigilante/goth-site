---
title: Operators
---

# Operators

## Arithmetic

| Unicode | ASCII | Operation |
|---------|-------|-----------|
| `+` | `+` | Addition |
| `-` | `-` | Subtraction |
| `×` | `*` | Multiplication |
| `/` | `/` | Division |
| `%` | `%` | Modulo |
| `^` | `^` | Exponentiation |
| `±` | `+-` | Uncertainty |

```goth
5 + 3       # 8
6 × 7       # 42
2 ^ 10      # 1024
```

## Comparison

| Unicode | ASCII | Operation |
|---------|-------|-----------|
| `=` | `=` | Value equality |
| `≠` | `/=` or `!=` | Inequality |
| `<` | `<` | Less than |
| `>` | `>` | Greater than |
| `≤` | `<=` | Less or equal |
| `≥` | `>=` | Greater or equal |

**Three levels of equality:**

| Level | Unicode | ASCII | Semantics |
|-------|---------|-------|-----------|
| Value | `=` | `=` | Compare values |
| Structural | `≡` | `===` | Alpha-equivalent, ignoring sharing |
| Referential | `≣` | (reserved) | Same node in DAG |

## Logical

| Unicode | ASCII | Operation |
|---------|-------|-----------|
| `∧` | `&&` or `and` | And |
| `∨` | `\|\|` or `or` | Or |
| `¬` | `!` or `not` | Not |

## Tensor Operations

| Unicode | ASCII | Operation | Example |
|---------|-------|-----------|---------|
| `↦` | `-:` | Map | `[1,2,3] ↦ (λ→ ₀ × 2)` → `[2,4,6]` |
| `▸` | `\|>` | Filter | `[1,2,3,4] ▸ (λ→ ₀ > 2)` → `[3,4]` |
| `⤇` | `>>=` | Bind (flatmap) | `[1,2] ⤇ (λ→ [₀, ₀×2])` → `[1,2,2,4]` |
| `⌿` | `fold` | Fold/reduce | `⌿ (λ→ λ→ ₁ + ₀) 0 [1,2,3]` → `6` |
| `⍀` | `scan` | Prefix sums | `[1,2,3,4] ⍀` → `[1,3,6,10]` |
| `Σ` | `+/` or `sum` | Sum | `[1,2,3] Σ` → `6` |
| `Π` | `*/` or `prod` | Product | `[1,2,3] Π` → `6` |
| `⊕` | `++` | Concatenate | `[1,2] ⊕ [3,4]` → `[1,2,3,4]` |
| `⊗` | `zip` | Zip | `[1,2] ⊗ [3,4]` → `[⟨1,3⟩, ⟨2,4⟩]` |

## Function Composition

| Unicode | ASCII | Operation |
|---------|-------|-----------|
| `∘` | `.:` | Compose: `(f ∘ g) x` = `f (g x)` |

```goth
let f = λ→ ₀ + 1 in
let g = λ→ ₀ × 2 in
(f ∘ g) 5
# Result: 11
```

## I/O Operations

| Unicode | ASCII | Operation |
|---------|-------|-----------|
| `▷` | `>>` | Write to stream/file |
| `◁` | `<<` | Read from file |

```goth
"hello" ▷ stdout          # Write to stdout (no newline)
"error" ▷ stderr          # Write to stderr
"content" ▷ "/tmp/out"    # Write to file
◁ "/tmp/input.txt"        # Read file contents
```

## Bitwise

| Unicode | Name | Operation |
|---------|------|-----------|
| | `bitand` | Bitwise AND |
| | `bitor` | Bitwise OR |
| `⊻` | `bitxor` | Bitwise XOR |
| | `shl` | Shift left |
| | `shr` | Shift right |

All bitwise operations are curried: `ℤ → ℤ → ℤ`.

## Precedence (low to high)

1. Postfix reduction (`Σ`, `Π`, `⍀`)
2. Function application
3. Infix operators (`+`, `×`, etc.)
4. Field access (`.field`)
