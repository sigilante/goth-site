---
title: Data Structures
---

# Data Structures

## Arrays and Tensors

**Literals:**

```goth
[1, 2, 3, 4, 5]
[3.14, 2.71, 1.41]
[[1, 2], [3, 4]]          # 2D
```

**Array fill syntax:**

```goth
[3 4 ; 0]
# 3×4 array filled with 0: [[0,0,0,0], [0,0,0,0], [0,0,0,0]]
```

**Indexing** (bracket must be adjacent, no space):

```goth
let arr = [10, 20, 30, 40] in arr[2]    # 30
let m = [[1, 2, 3], [4, 5, 6]] in m[1, 2]  # 6
```

> With a space, `f [1,2]` is function application (passing `[1,2]` to `f`), not indexing.

**Operations:**

```goth
len [1, 2, 3, 4]              # 4
shape [[1, 2], [3, 4]]        # [2, 2]
reverse [1, 2, 3]             # [3, 2, 1]
```

## Tuples

```goth
⟨1, 2⟩                        # Unicode
(1, 2)                        # ASCII
⟨3.14, 2.71, 1.41⟩
⟨⊤, 5, "hello"⟩               # Heterogeneous
```

**Access by index:**

```goth
let pair = ⟨10, 20⟩ in pair.0    # 10
let triple = ⟨1, 2, 3⟩ in triple.2  # 3
```

**Destructuring:**

```goth
let (x, y) = ⟨5, 10⟩ in x + y    # 15
```

## Records

Named fields in tuple-like syntax:

```goth
⟨x: 10, y: 20⟩
⟨name: "Alice", age: 30, active: ⊤⟩
```

**Field access:**

```goth
let point = ⟨x: 5.0, y: 10.0⟩ in point.x    # 5.0
```

**Greek letters in field names:**

```goth
let stats = ⟨μ: 10.0, σ: 2.0, σ²: 4.0, n: 100⟩ in stats.σ²
# Result: 4.0
```

## Variants (Sum Types)

```goth
⟨Left 5⟩
⟨Right "error"⟩
⟨Some 42⟩
⟨None⟩
```

**Pattern matching on variants:**

```goth
match ⟨Some 42⟩
  ⟨None⟩ → 0
  ⟨Some x⟩ → x
# Result: 42
```

**Enum declarations:**

```goth
enum Option α where Some α | None
enum Either α β where Left α | Right β
```
