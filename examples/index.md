---
title: Examples
---

# Examples

All examples run under the Goth interpreter. Source files are in the [`examples/`](https://github.com/sigilante/goth/tree/master/examples) directory.

```sh
goth examples/basic/square.goth 7          # Run with argument
goth examples/recursion/gcd.goth 12 8      # Multiple arguments
goth -e 'Σ [1, 2, 3, 4, 5]'               # Inline expression
```

---

## Basic

Elementary single-function programs. Each takes one integer and returns a result.

**Square** ([`square.goth`](https://github.com/sigilante/goth/blob/master/examples/basic/square.goth)):

```goth
╭─ main : I64 → I64
╰─ ₀ × ₀
```

```sh
$ goth examples/basic/square.goth 7
49
```

| File | Description | Example |
|------|-------------|---------|
| [`identity.goth`](https://github.com/sigilante/goth/blob/master/examples/basic/identity.goth) | Returns argument unchanged | `5 → 5` |
| [`add_one.goth`](https://github.com/sigilante/goth/blob/master/examples/basic/add_one.goth) | Adds one | `5 → 6` |
| [`double.goth`](https://github.com/sigilante/goth/blob/master/examples/basic/double.goth) | Doubles the input | `5 → 10` |
| [`square.goth`](https://github.com/sigilante/goth/blob/master/examples/basic/square.goth) | Squares the input | `5 → 25` |
| [`abs.goth`](https://github.com/sigilante/goth/blob/master/examples/basic/abs.goth) | Absolute value | `-3 → 3` |
| [`sign.goth`](https://github.com/sigilante/goth/blob/master/examples/basic/sign.goth) | Sign function (-1, 0, or 1) | `5 → 1` |
| [`is_even.goth`](https://github.com/sigilante/goth/blob/master/examples/basic/is_even.goth) | Evenness check | `4 → ⊤` |
| [`is_positive.goth`](https://github.com/sigilante/goth/blob/master/examples/basic/is_positive.goth) | Positivity check | `5 → ⊤` |
| [`max_two.goth`](https://github.com/sigilante/goth/blob/master/examples/basic/max_two.goth) | Maximum of two | `3 7 → 7` |
| [`min_two.goth`](https://github.com/sigilante/goth/blob/master/examples/basic/min_two.goth) | Minimum of two | `3 7 → 3` |

---

## Recursion

Classic recursive algorithms.

**Factorial** ([`factorial.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/factorial.goth)):

```goth
╭─ main : I64 → I64
╰─ if ₀ < 1 then 1
   else ₀ × main (₀ - 1)
```

```sh
$ goth examples/recursion/factorial.goth 5
120
```

**Fibonacci** ([`fibonacci.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/fibonacci.goth)):

```goth
╭─ main : I64 → I64
╰─ if ₀ < 2 then ₀
   else main (₀ - 1) + main (₀ - 2)
```

**GCD** ([`gcd.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/gcd.goth)) — two-argument Euclidean algorithm:

```goth
╭─ main : I64 → I64 → I64
╰─ if ₀ = 0 then ₁
   else main ₀ (₁ % ₀)
```

```sh
$ goth examples/recursion/gcd.goth 12 8
4
```

| File | Description | Example |
|------|-------------|---------|
| [`factorial.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/factorial.goth) | n! | `5 → 120` |
| [`fibonacci.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/fibonacci.goth) | Fibonacci numbers | `10 → 55` |
| [`sum_to_n.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/sum_to_n.goth) | Triangular numbers | `5 → 15` |
| [`power.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/power.goth) | base^exp | `2 10 → 1024` |
| [`gcd.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/gcd.goth) | Euclidean GCD | `12 8 → 4` |
| [`lcm.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/lcm.goth) | Least common multiple | `4 6 → 12` |
| [`ackermann.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/ackermann.goth) | Ackermann function | `2 3 → 9` |
| [`sudan.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/sudan.goth) | Sudan function | `1 1 1 → 4` |
| [`collatz_len.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/collatz_len.goth) | Collatz sequence length | `7 → 16` |
| [`digit_sum.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/digit_sum.goth) | Sum of digits | `1234 → 10` |
| [`reverse_num.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/reverse_num.goth) | Reverse digits | `1234 → 4321` |
| [`hyperop.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/hyperop.goth) | Hyperoperation | `2 3 4 → 65536` |
| [`tak.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/tak.goth) | Takeuchi function | `7 4 2 → 4` |
| [`mccarthy91.goth`](https://github.com/sigilante/goth/blob/master/examples/recursion/mccarthy91.goth) | McCarthy 91 | `85 → 91` |

---

## Higher-Order Functions

Functions that take or return other functions.

**Pipeline** ([`pipeline.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/pipeline.goth)) — range, filter evens, map square, sum:

```goth
╭─ isEven : I64 → Bool
╰─ (₀ % 2) = 0

╭─ square : I64 → I64
╰─ ₀ × ₀

╭─ sumSqEven : I64 → I64 → I64
╰─ if ₁ > ₀ then 0
   else if isEven ₁
        then (square ₁) + sumSqEven (₁ + 1) ₀
        else sumSqEven (₁ + 1) ₀

╭─ main : I64 → I64
╰─ sumSqEven 1 ₀
```

```sh
$ goth examples/higher-order/pipeline.goth 6
56
```

**Map** ([`map_double.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/map_double.goth)):

```goth
╭─ double : I64 → I64
╰─ ₀ × 2

╭─ main : I64 → T
╰─ (range 1 (₀ + 1)) ↦ double
```

**Filter** ([`filter_positive.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/filter_positive.goth)):

```goth
╭─ isPositive : I64 → Bool
╰─ ₀ > 0

╭─ main : I64 → T
╰─ (range (0 - ₀) (₀ + 1)) ▸ isPositive
```

| File | Description | Example |
|------|-------------|---------|
| [`map_double.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/map_double.goth) | Double each element | `5 → [2,4,6,8,10]` |
| [`filter_positive.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/filter_positive.goth) | Keep positive numbers | `5 → [1,2,3,4,5]` |
| [`compose.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/compose.goth) | square(double(x)) | `5 → 100` |
| [`apply_twice.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/apply_twice.goth) | f(f(x)) | `5 → 20` |
| [`all_positive.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/all_positive.goth) | All elements positive? | `5 → ⊤` |
| [`any_negative.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/any_negative.goth) | Any element negative? | `5 → ⊤` |
| [`count_if.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/count_if.goth) | Count matching | `5 → 2` |
| [`fold_sum.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/fold_sum.goth) | Fold to sum | `5 → 15` |
| [`fold_product.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/fold_product.goth) | Fold to product | `5 → 120` |
| [`pipeline.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/pipeline.goth) | Chained operations | `6 → 56` |
| [`concat.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/concat.goth) | Array concatenation | `5 → [1..5,1..5]` |
| [`zip_sum.goth`](https://github.com/sigilante/goth/blob/master/examples/higher-order/zip_sum.goth) | Zip into pairs | `5 → [⟨1,0⟩ ...]` |

---

## Numeric

Numerical computing: series, special functions, iterative methods.

**Sum of squares** ([`sum_squares.goth`](https://github.com/sigilante/goth/blob/master/examples/numeric/sum_squares.goth)):

```goth
╭─ sumSq : I64 → I64 → I64
╰─ if ₀ > ₁ then 0
   else ₀ × ₀ + sumSq ₁ (₀ + 1)

╭─ main : I64 → I64
╰─ sumSq ₀ 1
```

**Pi via Leibniz series** ([`pi_leibniz.goth`](https://github.com/sigilante/goth/blob/master/examples/numeric/pi_leibniz.goth)):

```goth
╭─ leibnizTerm : I64 → F64
╰─ if (₀ % 2) = 0
   then 1.0 / toFloat (2 × ₀ + 1)
   else (0.0 - 1.0) / toFloat (2 × ₀ + 1)

╭─ leibnizSum : I64 → I64 → F64
╰─ if ₀ > ₁ then 0.0
   else leibnizTerm ₀ + leibnizSum ₁ (₀ + 1)

╭─ main : I64 → F64
╰─ 4.0 × leibnizSum ₀ 0
```

| File | Description | Example |
|------|-------------|---------|
| [`sum_squares.goth`](https://github.com/sigilante/goth/blob/master/examples/numeric/sum_squares.goth) | 1² + 2² + ... + n² | `5 → 55` |
| [`product_range.goth`](https://github.com/sigilante/goth/blob/master/examples/numeric/product_range.goth) | Product via `Π` | `5 → 120` |
| [`harmonic.goth`](https://github.com/sigilante/goth/blob/master/examples/numeric/harmonic.goth) | Harmonic number H(n) | `5 → 2.28...` |
| [`pi_leibniz.goth`](https://github.com/sigilante/goth/blob/master/examples/numeric/pi_leibniz.goth) | Pi via Leibniz series | `20 → 2.976...` |
| [`exp_taylor.goth`](https://github.com/sigilante/goth/blob/master/examples/numeric/exp_taylor.goth) | e^x via Taylor series | `5.0 → 148.41...` |
| [`sqrt_newton.goth`](https://github.com/sigilante/goth/blob/master/examples/numeric/sqrt_newton.goth) | √x via Newton-Raphson | `5.0 → 2.236...` |
| [`gamma_fact.goth`](https://github.com/sigilante/goth/blob/master/examples/numeric/gamma_fact.goth) | n! via Gamma | `5.0 → 120.0` |
| [`gamma_half.goth`](https://github.com/sigilante/goth/blob/master/examples/numeric/gamma_half.goth) | Gamma at half-integers | `5.0 → 24.0` |

---

## Algorithms

Classical algorithms in a functional style.

**Primality test** ([`isPrime.goth`](https://github.com/sigilante/goth/blob/master/examples/algorithms/isPrime.goth)):

```goth
╭─ hasDivisor : I64 → I64 → Bool
╰─ if ₁ × ₁ > ₀ then ⊥
   else if (₀ % ₁) = 0 then ⊤
   else hasDivisor (₁ + 1) ₀

╭─ isPrime : I64 → Bool
╰─ if ₀ < 2 then ⊥
   else ¬(hasDivisor 2 ₀)

╭─ main : I64 → Bool
╰─ isPrime ₀
```

```sh
$ goth examples/algorithms/isPrime.goth 7
⊤
```

| File | Description | Example |
|------|-------------|---------|
| [`isPrime.goth`](https://github.com/sigilante/goth/blob/master/examples/algorithms/isPrime.goth) | Primality test | `7 → ⊤` |
| [`count_primes.goth`](https://github.com/sigilante/goth/blob/master/examples/algorithms/count_primes.goth) | Count primes ≤ n | `10 → 4` |
| [`nth_prime.goth`](https://github.com/sigilante/goth/blob/master/examples/algorithms/nth_prime.goth) | Find nth prime | `5 → 11` |
| [`isqrt.goth`](https://github.com/sigilante/goth/blob/master/examples/algorithms/isqrt.goth) | Integer square root | `10 → 3` |
| [`binary_search.goth`](https://github.com/sigilante/goth/blob/master/examples/algorithms/binary_search.goth) | Binary search | `7 0 10 → 7` |
| [`modpow.goth`](https://github.com/sigilante/goth/blob/master/examples/algorithms/modpow.goth) | Modular exponentiation | `2 10 1000 → 24` |

---

## Contracts

Functions with runtime-checked preconditions and postconditions.

**Safe square root** ([`sqrt_safe.goth`](https://github.com/sigilante/goth/blob/master/examples/contracts/sqrt_safe.goth)):

```goth
╭─ sqrtSafe : F64 → F64
│  ⊢ ₀ >= 0.0
╰─ √₀

╭─ main : F64 → F64
╰─ sqrtSafe ₀
```

**Safe division** ([`div_safe.goth`](https://github.com/sigilante/goth/blob/master/examples/contracts/div_safe.goth)):

```goth
╭─ divSafe : I64 → I64 → I64
│  ⊢ ₀ ≠ 0
╰─ ₁ / ₀
```

| File | Description | Contract |
|------|-------------|----------|
| [`abs_post.goth`](https://github.com/sigilante/goth/blob/master/examples/contracts/abs_post.goth) | Absolute value | Post: result ≥ 0 |
| [`div_safe.goth`](https://github.com/sigilante/goth/blob/master/examples/contracts/div_safe.goth) | Safe division | Pre: divisor ≠ 0 |
| [`factorial_contract.goth`](https://github.com/sigilante/goth/blob/master/examples/contracts/factorial_contract.goth) | Factorial | Pre: n ≥ 0, Post: result ≥ 1 |
| [`log_safe.goth`](https://github.com/sigilante/goth/blob/master/examples/contracts/log_safe.goth) | Natural log | Pre: x > 0 |
| [`sqrt_safe.goth`](https://github.com/sigilante/goth/blob/master/examples/contracts/sqrt_safe.goth) | Square root | Pre: x ≥ 0 |

---

## Uncertainty

First-class uncertain values with automatic error propagation.

**Adding uncertain values** ([`add_uncertain.goth`](https://github.com/sigilante/goth/blob/master/examples/uncertainty/add_uncertain.goth)):

```goth
╭─ main : (F64 ± F64) → (F64 ± F64) → (F64 ± F64)
╰─ ₁ + ₀
```

```sh
$ goth examples/uncertainty/add_uncertain.goth "10.0±0.3" "20.0±0.4"
30 ± 0.5
```

**Chained propagation** ([`chained_uncertain.goth`](https://github.com/sigilante/goth/blob/master/examples/uncertainty/chained_uncertain.goth)) — `sin(√a + b)`:

```goth
╭─ main : (F64 ± F64) → (F64 ± F64) → (F64 ± F64)
╰─ sin (√₁ + ₀)
```

| File | Description | Example |
|------|-------------|---------|
| [`measure.goth`](https://github.com/sigilante/goth/blob/master/examples/uncertainty/measure.goth) | Return uncertain value | `"10.0±0.5" → 10 ± 0.5` |
| [`add_uncertain.goth`](https://github.com/sigilante/goth/blob/master/examples/uncertainty/add_uncertain.goth) | Addition with error propagation | `"10.0±0.3" "20.0±0.4" → 30 ± 0.5` |
| [`mul_uncertain.goth`](https://github.com/sigilante/goth/blob/master/examples/uncertainty/mul_uncertain.goth) | Multiplication with relative error | `"5.0±0.1" "3.0±0.2" → 15 ± 1.04...` |
| [`sqrt_uncertain.goth`](https://github.com/sigilante/goth/blob/master/examples/uncertainty/sqrt_uncertain.goth) | Square root propagation | `"9.0±0.3" → 3 ± 0.05` |
| [`sin_uncertain.goth`](https://github.com/sigilante/goth/blob/master/examples/uncertainty/sin_uncertain.goth) | Sine propagation | `"1.0±0.1" → 0.841... ± 0.054...` |
| [`chained_uncertain.goth`](https://github.com/sigilante/goth/blob/master/examples/uncertainty/chained_uncertain.goth) | Multi-step: sin(√a + b) | `"4.0±0.1" "1.0±0.05"` |

---

## Tail-Call Optimization

Paired naive vs. accumulator-based versions showing the tail recursion transformation.

**Naive factorial** ([`factorial_naive.goth`](https://github.com/sigilante/goth/blob/master/examples/tco/factorial_naive.goth)):

```goth
╭─ fact : I64 → I64
╰─ if ₀ < 2 then 1
   else ₀ × fact (₀ - 1)     # NOT tail recursive
```

**Tail-recursive factorial** ([`factorial_tco.goth`](https://github.com/sigilante/goth/blob/master/examples/tco/factorial_tco.goth)):

```goth
╭─ factAcc : I64 → I64 → I64
╰─ if ₁ < 2 then ₀
   else factAcc (₁ - 1) (₁ × ₀)    # IS tail recursive

╭─ main : I64 → I64
╰─ factAcc ₀ 1
```

| Pair | Naive | TCO |
|------|-------|-----|
| Factorial | [`factorial_naive.goth`](https://github.com/sigilante/goth/blob/master/examples/tco/factorial_naive.goth) | [`factorial_tco.goth`](https://github.com/sigilante/goth/blob/master/examples/tco/factorial_tco.goth) |
| Fibonacci | [`fibonacci_naive.goth`](https://github.com/sigilante/goth/blob/master/examples/tco/fibonacci_naive.goth) | [`fibonacci_tco.goth`](https://github.com/sigilante/goth/blob/master/examples/tco/fibonacci_tco.goth) |
| Sum 1..n | [`sum_naive.goth`](https://github.com/sigilante/goth/blob/master/examples/tco/sum_naive.goth) | [`sum_tco.goth`](https://github.com/sigilante/goth/blob/master/examples/tco/sum_tco.goth) |
| Collatz | [`collatz_naive.goth`](https://github.com/sigilante/goth/blob/master/examples/tco/collatz_naive.goth) | [`collatz_tco.goth`](https://github.com/sigilante/goth/blob/master/examples/tco/collatz_tco.goth) |
| List length | [`length_naive.goth`](https://github.com/sigilante/goth/blob/master/examples/tco/length_naive.goth) | [`length_tco.goth`](https://github.com/sigilante/goth/blob/master/examples/tco/length_tco.goth) |

---

## I/O

File and stream I/O using the `▷` (write) operator.

**Write to stdout** ([`write_stdout.goth`](https://github.com/sigilante/goth/blob/master/examples/io/write_stdout.goth)):

```goth
╭─ main : I64 → ()
╰─ "hello" ▷ stdout
```

| File | Description |
|------|-------------|
| [`write_stdout.goth`](https://github.com/sigilante/goth/blob/master/examples/io/write_stdout.goth) | Write to stdout (no newline) |
| [`write_stderr.goth`](https://github.com/sigilante/goth/blob/master/examples/io/write_stderr.goth) | Write to stderr |
| [`write_file.goth`](https://github.com/sigilante/goth/blob/master/examples/io/write_file.goth) | Write to file |

---

## Simulation

Numerical simulations producing SVG visualizations and CSV data.

**1D Heat Diffusion** ([`heat1d.goth`](https://github.com/sigilante/goth/blob/master/examples/simulation/heat1d.goth)) — explicit finite difference:

```goth
╭─ stencil : [n]F64 → I64 → F64
╰─ if ₀ = 0 then 0.0
   else if ₀ = 19 then 0.0
   else ₁[₀] + 0.4 × (₁[₀ - 1] + ₁[₀ + 1] - 2.0 × ₁[₀])

╭─ stepGrid : [n]F64 → [n]F64
╰─ let grid = ₀ in
   ι 20 ↦ (λ→ stencil grid ₀)

╭─ evolve : [n]F64 → I64 → [n]F64
╰─ if ₀ = 0 then ₁
   else evolve (stepGrid ₁) (₀ - 1)
```

```sh
$ goth examples/simulation/heat1d.goth 0
# Writes heat1d.svg
```

| File | Description | Output |
|------|-------------|--------|
| [`heat1d.goth`](https://github.com/sigilante/goth/blob/master/examples/simulation/heat1d.goth) | 1D heat diffusion | `heat1d.svg` |
| [`heat2d.goth`](https://github.com/sigilante/goth/blob/master/examples/simulation/heat2d.goth) | 2D heat diffusion | `heat2d.svg` |
| [`newton_raphson.goth`](https://github.com/sigilante/goth/blob/master/examples/simulation/newton_raphson.goth) | Newton-Raphson root finder | `newton.svg`, `newton.csv` |
| [`wave1d.goth`](https://github.com/sigilante/goth/blob/master/examples/simulation/wave1d.goth) | 1D wave equation | `wave1d.svg`, `wave1d.csv` |
| [`laplace2d.goth`](https://github.com/sigilante/goth/blob/master/examples/simulation/laplace2d.goth) | 2D Laplace (Jacobi) | `laplace2d.svg`, `laplace2d.csv` |
| [`power_iter.goth`](https://github.com/sigilante/goth/blob/master/examples/simulation/power_iter.goth) | Eigenvalue iteration | `power_iter.svg`, `power_iter.csv` |

---

## Random / Monte Carlo

Monte Carlo methods using the `random.goth` standard library.

**Monte Carlo integration** ([`mc_integrate.goth`](https://github.com/sigilante/goth/blob/master/examples/random/mc_integrate.goth)) — estimate ∫₀¹ e⁻ˣ² dx:

```goth
use "../../stdlib/random.goth"

╭─ main : I64 → F64
│ ⊢ ₀ > 0
│ ⊨ ₀ > 0.5 ∧ ₀ < 1.0
╰─ let n = ₀
   in let seed = entropy ⟨⟩
   in let ⟨total, _⟩ = ⌿ (λ→ λ→
        let acc = ₁
        in let ⟨x, s1⟩ = randFloat (acc.1)
        in let fx = exp (0.0 - x × x)
        in ⟨acc.0 + fx, s1⟩)
      ⟨0.0, seed⟩
      (ι n)
   in total / toFloat n
```

```sh
$ goth examples/random/mc_integrate.goth 10000
0.7468...
```

| File | Description | Example |
|------|-------------|---------|
| [`rand_floats.goth`](https://github.com/sigilante/goth/blob/master/examples/random/rand_floats.goth) | Generate random floats | `5 → [0.23, ...]` |
| [`buffon_pi.goth`](https://github.com/sigilante/goth/blob/master/examples/random/buffon_pi.goth) | Estimate π via Buffon's needle | `10000 → 3.14...` |
| [`mc_integrate.goth`](https://github.com/sigilante/goth/blob/master/examples/random/mc_integrate.goth) | Monte Carlo integration | `10000 → 0.746...` |
| [`mc_importance.goth`](https://github.com/sigilante/goth/blob/master/examples/random/mc_importance.goth) | Importance sampling | `10000 → 0.746...` |
| [`mc_antithetic.goth`](https://github.com/sigilante/goth/blob/master/examples/random/mc_antithetic.goth) | Antithetic variates | `10000 → ⟨0.74..., 0.74...⟩` |

---

## Crypto

Pure Goth implementations of cryptographic hash functions.

**SHA-256** ([`sha256.goth`](https://github.com/sigilante/goth/blob/master/examples/crypto/sha256.goth)):

```goth
use "../../stdlib/crypto.goth"

╭─ main : () → String
╰─ let _ = print (sha256 "")
   in let _ = print (sha256 "abc")
   in let _ = print (sha256 "hello")
   in sha256 "abcdbcdecdefdefgefghfghighijhijkijkljklmklmnlmnomnopnopq"
```

| File | Description |
|------|-------------|
| [`sha256.goth`](https://github.com/sigilante/goth/blob/master/examples/crypto/sha256.goth) | SHA-256 (NIST FIPS 180-4) |
| [`md5.goth`](https://github.com/sigilante/goth/blob/master/examples/crypto/md5.goth) | MD5 (RFC 1321) |
| [`blake3.goth`](https://github.com/sigilante/goth/blob/master/examples/crypto/blake3.goth) | BLAKE3 (single chunk) |
| [`base64.goth`](https://github.com/sigilante/goth/blob/master/examples/crypto/base64.goth) | Base64 encode/decode |
| [`hashfile.goth`](https://github.com/sigilante/goth/blob/master/examples/crypto/hashfile.goth) | Hash a file with SHA-256, MD5, BLAKE3 |

---

## Feature Coverage

| Feature | Example Categories |
|---------|-------------------|
| De Bruijn indices (`₀`, `₁`, `₂`) | All |
| Function declarations (`╭─`/`╰─`) | All |
| Lambda expressions (`λ→`) | higher-order, numeric, simulation |
| Map (`↦`) | higher-order, numeric, simulation |
| Filter (`▸`) | higher-order |
| Sum/Product (`Σ`/`Π`) | numeric, higher-order |
| Contracts (`⊢`/`⊨`) | contracts, random |
| Uncertainty (`±`) | uncertainty |
| I/O (`▷`, `◁`) | io, simulation, crypto |
| Modules (`use`) | simulation, random, crypto |
| Bitwise ops | crypto |
| PRNG / entropy | random |
