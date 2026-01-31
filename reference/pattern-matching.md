---
title: Pattern Matching
---

# Pattern Matching

## Match Expression

```goth
match expr
  pattern₁ → result₁
  pattern₂ → result₂
  _        → default
```

## Pattern Forms

### Literals

```goth
match 5
  0 → "zero"
  1 → "one"
  5 → "five"
  _ → "other"
# Result: "five"
```

### Variables

```goth
match 42
  x → x × 2
# Result: 84
```

### Wildcards

```goth
match anything
  _ → "default"
```

### Tuples

```goth
match ⟨10, 20⟩
  (0, 0) → "origin"
  (x, 0) → "x-axis"
  (0, y) → "y-axis"
  (x, y) → "general"
```

### Arrays

```goth
match [1, 2, 3]
  []        → "empty"
  [x]       → "single"
  [x, y]    → "pair"
  [x, y, z] → "triple"
  _         → "many"
```

### Array Split (Head/Tail)

```goth
match [1, 2, 3, 4, 5]
  [head | tail] → head     # 1

match [1, 2, 3, 4]
  [x, y | rest] → x + y    # 3
```

### Variants

```goth
match ⟨Left "error"⟩
  ⟨Left msg⟩  → "Error: " ++ msg
  ⟨Right val⟩ → "Success"
```

### Records

```goth
match ⟨x: 5, y: 10⟩
  ⟨x: 0, y: 0⟩ → "origin"
  ⟨x, y⟩       → x + y
```

## Examples

**Fibonacci:**

```goth
╭─ fib : ℤ → ℤ
╰─ match ₀
     0 → 0
     1 → 1
     n → fib(n - 1) + fib(n - 2)
```

**Safe head:**

```goth
╭─ safe_head : [n]α → α?
╰─ match ₀
     []         → ⟨None⟩
     [x | rest] → ⟨Some x⟩
```

**Unwrap with default:**

```goth
╭─ unwrap_or : α? → α → α
╰─ match ₀
     ⟨None⟩   → ₁
     ⟨Some x⟩ → x
```
