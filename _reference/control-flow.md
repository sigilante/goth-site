---
title: Control Flow
---

# Control Flow

## If-Then-Else

```goth
if condition then true_branch else false_branch
```

```goth
if 5 > 3 then "yes" else "no"    # "yes"
```

**Nested:**

```goth
if x < 0 then "negative"
else if x = 0 then "zero"
else "positive"
```

**As expression:**

```goth
let abs = λ→ if ₀ < 0 then -₀ else ₀ in abs(-5)
# Result: 5
```

## Match

See [Pattern Matching](../pattern-matching/) for full coverage.

```goth
match ₀
  0 → 1
  n → n × factorial(n - 1)
```

## Recursion

**Direct recursion:**

```goth
╭─ factorial : ℤ → ℤ
╰─ if ₀ ≤ 1 then 1 else ₀ × factorial (₀ - 1)
```

**Tail recursion with accumulator:**

```goth
╭─ factAcc : I64 → I64 → I64
╰─ if ₁ < 2 then ₀
   else factAcc (₁ - 1) (₁ × ₀)

╭─ main : I64 → I64
╰─ factAcc ₀ 1
```

**Mutual recursion:**

```goth
let rec even = λ→ match ₀
                0 → ⊤
                n → odd(n - 1) ;
        odd = λ→ match ₀
                0 → ⊥
                n → even(n - 1)
in even 10
```
