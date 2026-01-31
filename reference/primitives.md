---
title: Primitives
---

# Primitives Reference

## Sequence Generation

| Name | Signature | Description |
|------|-----------|-------------|
| `ι`, `iota` | `ℤ → [n]ℤ` | `[0, 1, ..., n-1]` |
| `range` | `ℤ → ℤ → [m]ℤ` | `[start, ..., end-1]` |

## Reductions

| Name | Signature | Description |
|------|-----------|-------------|
| `Σ`, `sum` | `[n]α → α` | Sum elements |
| `Π`, `prod` | `[n]α → α` | Product of elements |
| `len` | `[n]α → ℤ` | Array length |

## Transformations

| Name | Signature | Description |
|------|-----------|-------------|
| `↦` (map) | `[n]α → (α → β) → [n]β` | Apply to each |
| `▸` (filter) | `[n]α → (α → Bool) → [m]α` | Keep matching |
| `⌿`, `fold` | `(α → β → α) → α → [n]β → α` | Left fold |
| `reverse` | `[n]α → [n]α` | Reverse |
| `take` | `ℤ → [n]α → [m]α` | First k elements |
| `drop` | `ℤ → [n]α → [m]α` | Drop first k |
| `⊕`, `++` | `[n]α → [m]α → [p]α` | Concatenate |

## Math Functions

| Name | Signature |
|------|-----------|
| `√`, `sqrt` | `F64 → F64` |
| `exp` | `F64 → F64` |
| `ln` | `F64 → F64` |
| `log10` | `F64 → F64` |
| `log2` | `F64 → F64` |
| `sin`, `cos`, `tan` | `F64 → F64` |
| `asin`, `acos`, `atan` | `F64 → F64` |
| `sinh`, `cosh`, `tanh` | `F64 → F64` |
| `floor`, `ceil`, `round` | `F64 → F64` |
| `abs` | Numeric → Numeric |
| `Γ` | `F64 → F64` |

**Unicode alternatives:**

```goth
√16.0                  # sqrt(16.0)
⌊3.7⌋                  # floor(3.7)
⌈3.2⌉                  # ceil(3.2)
```

## Linear Algebra

| Name | Signature | Description |
|------|-----------|-------------|
| `·`, `dot` | `[n]F64 → [n]F64 → F64` | Dot product |
| `norm` | `[n]F64 → F64` | Euclidean norm |
| `matmul` | `[m n]F64 → [n p]F64 → [m p]F64` | Matrix multiply |
| `⍉`, `transpose` | `[m n]α → [n m]α` | Transpose |

## Type Conversions

| Name | Signature | Description |
|------|-----------|-------------|
| `toInt` | `α → ℤ` | Convert to integer |
| `toFloat` | `α → F64` | Convert to float |
| `toChar` | `ℤ → Char` | Integer to character |
| `toString` | `α → String` | Value to string |
| `parseInt` | `String → ℤ` | Parse integer |
| `parseFloat` | `String → F64` | Parse float |
| `chars` | `String → [n]Char` | String to characters |
| `fromChars` | `[n]Char → String` | Characters to string |

## String Operations

| Name | Signature | Description |
|------|-----------|-------------|
| `strConcat`, `⧺` | `String → String → String` | Concatenate |
| `++` | `String → String → String` | Concatenate (infix) |

## I/O

| Name | Signature | Description |
|------|-----------|-------------|
| `print` | `α → ()` | Print with newline |
| `readLine` | `() → String` | Read from stdin |
| `readFile` | `String → String` | Read file |
| `writeFile` | `String → String → ()` | Write to file |
| `⧏`, `readBytes` | `ℤ → String → [n]ℤ` | Read n bytes |
| `⧐`, `writeBytes` | `[n]ℤ → String → ()` | Write bytes |
| `▷` | `α → Stream/String → ()` | Write operator |
| `◁` | `String → String` | Read file |

`stdout` and `stderr` are built-in stream constants.

## Bitwise Operations

| Name | Signature | Description |
|------|-----------|-------------|
| `bitand` | `ℤ → ℤ → ℤ` | AND |
| `bitor` | `ℤ → ℤ → ℤ` | OR |
| `⊻`, `bitxor` | `ℤ → ℤ → ℤ` | XOR |
| `shl` | `ℤ → ℤ → ℤ` | Shift left (0..127) |
| `shr` | `ℤ → ℤ → ℤ` | Shift right (0..127) |
