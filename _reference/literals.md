---
title: Literals
---

# Literals

## Integers

```goth
42
-17
0
1_000_000
```

All integer types are stored as **i128** at runtime. The type distinctions (`I64`, `I32`, `ℤ`, `ℕ`) exist for documentation and type checking but share the same runtime representation.

## Floats

```goth
3.14
-0.5
2.0
1.5e-10
```

## Booleans

| Unicode | ASCII |
|---------|-------|
| `⊤` | `true` |
| `⊥` | `false` |

## Characters

```goth
'a'
'π'
'∀'
'\n'     # Newline
```

## Strings

```goth
"hello world"
"Goth supports Unicode: αβγ"
"Escape sequences: \n \t \\"
```

Strings are internally represented as character tensors.

### Escape Sequences

| Escape | Character |
|--------|-----------|
| `\n` | Newline |
| `\t` | Tab |
| `\\` | Backslash |
| `\"` | Double quote |
| `\r` | Carriage return |

## Imaginary Literals

Complex and quaternion imaginary units use `𝕚`, `𝕛`, `𝕜` (blackboard bold) or ASCII `i`, `j`, `k` suffixed to a number:

```goth
4𝕚                    # Complex: 0 + 4𝕚
3.14𝕚                 # Complex: 0 + 3.14𝕚
2𝕛                    # Quaternion: 0 + 0𝕚 + 2𝕛 + 0𝕜
5𝕜                    # Quaternion: 0 + 0𝕚 + 0𝕛 + 5𝕜
```

ASCII fallback (digit-prefixed only):

```goth
4i                    # Same as 4𝕚
2j                    # Same as 2𝕛
3k                    # Same as 3𝕜
```

Standalone Unicode imaginary units default to coefficient 1:

```goth
𝕚                     # Same as 1𝕚
𝕛                     # Same as 1𝕛
𝕜                     # Same as 1𝕜
```

Build complex numbers with arithmetic:

```goth
3 + 4𝕚                # Complex(3, 4)
1 + 2𝕚 + 3𝕛 + 4𝕜    # Quaternion(1, 2, 3, 4)
```

> Bare `i`, `j`, `k` without a leading digit remain ordinary identifiers.

## Unit

```goth
()
⟨⟩
```

## Arrays

```goth
[1, 2, 3]
[[1, 2], [3, 4]]
[3 4 ; 0]           # 3×4 array filled with 0
```

See [Data Structures](../data-structures/) for full details.
