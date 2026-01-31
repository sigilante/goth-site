---
title: Contracts
---

# Contracts

Goth supports runtime-checked preconditions and postconditions on function declarations.

## Preconditions (`⊢`)

Checked **before** the function body executes:

```goth
╭─ sqrt_safe : F → F
│  ⊢ ₀ ≥ 0
╰─ √₀
```

In preconditions, `₀` is the last argument, `₁` the second-to-last, etc.

Unicode: `⊢` / ASCII: `|-`

**Multiple preconditions:**

```goth
╭─ divide : F → F → F
│  ⊢ ₀ ≠ 0
│  ⊢ abs ₁ < 1000
╰─ ₁ / ₀
```

## Postconditions (`⊨`)

Checked **after** the function body executes:

```goth
╭─ double : F → F
│  ⊨ ₀ = ₁ × 2
╰─ ₀ × 2
```

In postconditions, `₀` is the **result**, `₁` is the first argument (shifted), etc.

Unicode: `⊨` / ASCII: `|=`

## Contract Violations

Violations produce runtime errors:

```goth
╭─ positive_only : F → F
│  ⊢ ₀ > 0
╰─ ₀

positive_only(-5)
# Error: Precondition violated: precondition #1 failed
```

## Examples

**Safe division** ([`div_safe.goth`](https://github.com/sigilante/goth/blob/master/examples/contracts/div_safe.goth)):

```goth
╭─ divSafe : I64 → I64 → I64
│  ⊢ ₀ ≠ 0
╰─ ₁ / ₀
```

**Factorial with bounds** ([`factorial_contract.goth`](https://github.com/sigilante/goth/blob/master/examples/contracts/factorial_contract.goth)):

```goth
╭─ factorial : F → F
│  ⊢ ₀ ≥ 0
│  ⊨ ₀ ≥ 1
╰─ if ₀ < 1 then 1 else ₀ × factorial(₀ - 1)
```

**Safe square root** ([`sqrt_safe.goth`](https://github.com/sigilante/goth/blob/master/examples/contracts/sqrt_safe.goth)):

```goth
╭─ sqrtSafe : F64 → F64
│  ⊢ ₀ >= 0.0
╰─ √₀
```
