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
| `√`, `sqrt` | `F64 → F64` (or `ℂ → ℂ`) |
| `exp` | `F64 → F64` (or `ℂ → ℂ`) |
| `ln` | `F64 → F64` (or `ℂ → ℂ`) |
| `log10` | `F64 → F64` |
| `log2` | `F64 → F64` |
| `sin`, `cos`, `tan` | `F64 → F64` (sin/cos also `ℂ → ℂ`) |
| `asin`, `acos`, `atan` | `F64 → F64` |
| `sinh`, `cosh`, `tanh` | `F64 → F64` |
| `floor`, `ceil`, `round` | `F64 → F64` |
| `abs` | Numeric → Numeric (ℂ/ℍ → F: modulus) |
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

## Matrix Utilities

| Name | Signature | Description |
|------|-----------|-------------|
| `trace`, `tr` | `[n n]F64 → F64` | Sum of diagonal elements |
| `det` | `[n n]F64 → F64` | Determinant (LU decomposition) |
| `inv` | `[n n]F64 → [n n]F64` | Matrix inverse (errors on singular) |
| `diag` | `[n]F64 → [n n]F64` | Diagonal vector → diagonal matrix |
| `diag` | `[n n]F64 → [n]F64` | Square matrix → diagonal vector |
| `eye` | `ℤ → [n n]F64` | Identity matrix of size n |

## Linear System Solvers

| Name | Signature | Description |
|------|-----------|-------------|
| `solve` | `[n n]F64 → [n]F64 → [n]F64` | Solve Ax = b (LU, default) |
| `solveWith` | `[n n]F64 → [n]F64 → String → [n]F64` | Solve with method choice |

`solveWith` accepts a method string: `"lu"` (Doolittle with partial pivoting) or `"qr"` (Householder reflections). QR also handles overdetermined (least-squares) systems:

```goth
solve [[2,1],[5,3]] [4,7]               # [5, -6]
solveWith [[1,1],[1,2],[1,3]] [1,2,2] "qr"  # least squares
```

## Complex and Quaternion

| Name | Signature | Description |
|------|-----------|-------------|
| `re` | `ℂ → F` | Real part (`re(3+4𝕚) = 3`) |
| `im` | `ℂ → F` | Imaginary part (`im(3+4𝕚) = 4`) |
| `conj` | `ℂ → ℂ` | Conjugate (`conj(3+4𝕚) = 3-4𝕚`) |
| `arg` | `ℂ → F` | Argument in radians (`arg(𝕚) = π/2`) |

For quaternions, `im` returns a 3-tuple `⟨i, j, k⟩` and `conj` negates all imaginary components.

All standard math functions extend to complex arguments:

```goth
exp(π𝕚)                    # ≈ -1 (Euler's identity)
sin(𝕚)                     # 0 + sinh(1)𝕚
sqrt(-4)                   # 2𝕚
ln(𝕚)                      # π𝕚/2
```

Arithmetic operators (`+`, `-`, `×`, `/`, `^`) work with complex and quaternion operands. Types auto-promote: `ℤ → F → ℂ → ℍ`.

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
