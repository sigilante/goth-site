---
title: "an experiment in applied philosophy"
date: 2026-01-31
author: Sigilante
---

`goth` is an experimental language designed for LLM reasoning patterns and human legibility.

The design criteria emphasize what LLMs are good at while avoiding what hurts their context and accuracy.  These things are favorable for current state-of-the-art coding LLMs:

- Pattern completion over structural templates
- Reasoning about explicit dataflow
- Type-level constraint satisfaction
- Compositional/algebraic thinking
- Dense semantic compression (token economy, efficient compression)

These things are "hard" in some sense for LLMs, since they have sliding finite context windows for memories rather than human-like deep recall.

- Boilerplate (imports, class scaffolding, semicolons) wastes tokens
- Implicit state and side effects requires simulating execution
- Distant syntactic dependencies, like matching braces 200 lines apart
- Naming inconsistencies, like `getString`, `get_string`, `GetString`
- Separation of spec from implementation

I had a great working session with Claude on this.  What we devised has echoes of [APL](https://en.wikipedia.org/wiki/APL_%28programming_language%29) and [Plankalkül](https://en.wikipedia.org/wiki/Plankalk%C3%BCl).  (Plankalkül is a strange duck:  in some way, it's the first programming language, having been devised by Konrad Zuse in the late 1930s for his machine.  It featured a two-dimensional syntax and only had a primitive data type of a single bit.)

Some other desiderata for the language, based on my aesthetic preferences:

1. Homoiconic.  Code is data.
2. Concatenative.  Stack-based computation.  (At this point, it's like a Forth-y Lisp-y APL.)
3. Shape-first types.  Types are tensor shapes + algebraic constraints.  `[3 4] → [4 5] → [3 5]`  is a type signature.
4. Spec–implementation unification.  There are not separate test files.  The contracts are the function.  Pre- and post-conditions generate tests automatically.
5. Unicode operators.  Single glyphs describe common operations.  An IDE can convert digraphs to glyphs seamlessly (following Mathematica).  Think of `∘` compose, `⊛` apply, `⊗` product, `⊕` sum, `↦` map, `⤇` bind, `⊢` assert/precondition, `⊨` satisfies/postcondition.  Operator overloading should be supported for language extension.
6. Explicit effects.  The language is pure by default.  Effects are capabilities passed in for I/O, mutation, randomness handled in types.
7. Structural not textual.  The AST is the primary representation.  Syntax is a serialization format rather than the canonical source of truth.

Efficient semantic compression takes place along three axes:

1. Elision, what can be inferred.  Implicit is better than explicit when inference can take place trivially.  Effects are pure unless annotated.  Arguments are positionally marked with de Bruijn indices rather than by names.
2. Factoring, shared structure (write-once code).  The AST is a DAG, not a tree.  Common subexpressions get names or indices once.  If multiple references occur we reference rather than redefining.  Macros can quote and unquote.
3. Density, more meaning per glyph.  In fact, we can even have expansions while still preserving semantic atoms.  `⊛Σ` is a single unit (a catamorphism)

With all that in hand, we set out together to build a new language.  The initial design went surprisingly fast with Claude Code:  within 24 hours we had a working interpreter for the language.  There was a premature attempt to build an LLVM compiler, `gothic`, which has been explicitly pended until `goth` is itself more settled.

## How to Get Involved

1. Join the `goth` community either by connecting to me [`@sigilante`](https://github.com/sigilante) on X or contacting with the group on Urbit at `~fabled-wander-lagrev-nocfep/v1bba7qe` ([join Tlon here](https://tlon.io/waitlist) or [explore other options here](https://urbit.org/overview/running-urbit/hosting-providers)).

2. Use the language.  The source code is available at [`sigilante/goth`](https://github.com/sigilante/goth).  We need benchmarks with various LLMs (instructions are in the benchmarks/ directory) and we need more examples of programs written in the language.  (We're particularly interested in examples that show off the language's strengths in areas like type-level reasoning and semantic compression.)

3. There is a [`$GOTH` ticker on bags.fm](https://bags.fm/BJM8YzhZ6Mu2iccB1RVhHiEGFoU76ivYfAU5nRyKBAGS).  This is an experimental meme coin which I did not create or launch. Someone designated me as the fee recipient, so I receive 1% of trading volume. I do not endorse, recommend, or promote this token. Claiming fees ≠ endorsement. `$GOTH` is a highly speculative instrument with no connection to the goth language project, no roadmap, and no utility. This is not financial advice and I'm not a financial advisor. Memecoins are extremely risky, as most lose nearly all value. I'm claiming these fees out of curiosity about the platform's model, not because I believe this token has value. Do not buy this expecting to support the goth project:  there are better ways to contribute if that's your goal (see the above).
