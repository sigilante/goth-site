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
