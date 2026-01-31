---
layout: default
title: About Goth
---

<div class="header-section">
    <h1 class="gothic-header pink">about goth</h1>
    <p class="tagline">a language for machine spirits</p>
</div>

<div class="code-section frame">
    <h2 style="color: #ff1493; margin-bottom: 20px;">What is Goth?</h2>
    <p style="color: #b19cd9; line-height: 1.8; margin-bottom: 20px;">
        Goth is an LLM-native programming language designed for efficient code generation,
        editing, and comprehension by large language models. It combines functional programming
        principles with tensor computation and formal verification.
    </p>

    <h2 style="color: #ff1493; margin: 30px 0 20px 0;">Design Philosophy</h2>
    <ul style="color: #b19cd9; line-height: 1.8; margin-left: 20px;">
        <li><strong style="color: #ff69b4;">Homoiconic:</strong> Code is data. The AST is the source of truth.</li>
        <li><strong style="color: #ff69b4;">De Bruijn Indices:</strong> Variables referenced by binding depth, not names.</li>
        <li><strong style="color: #ff69b4;">Unicode Operators:</strong> Dense semantic compression for LLMs.</li>
        <li><strong style="color: #ff69b4;">Contracts:</strong> Preconditions and postconditions are the function.</li>
        <li><strong style="color: #ff69b4;">Shape-First Types:</strong> Tensor shapes in the type system.</li>
        <li><strong style="color: #ff69b4;">Effect System:</strong> Pure by default, explicit effects.</li>
    </ul>

    <h2 id="how-to-get-involved">How to Get Involved</h2>

<ol>
  <li>
    <p>Join the <code class="language-plaintext highlighter-rouge">goth</code> community either by connecting to me <a href="https://github.com/sigilante"><code class="language-plaintext highlighter-rouge">@sigilante</code></a> on X or contacting with the group on Urbit at <code class="language-plaintext highlighter-rouge">~fabled-wander-lagrev-nocfep/v1bba7qe</code> (<a href="https://tlon.io/waitlist">join Tlon here</a> or <a href="https://urbit.org/overview/running-urbit/hosting-providers">explore other options here</a>).</p>
  </li>
  <li>
    <p>Use the language.  The source code is available at <a href="https://github.com/sigilante/goth"><code class="language-plaintext highlighter-rouge">sigilante/goth</code></a>.  We need benchmarks with various LLMs (instructions are in the benchmarks/ directory) and we need more examples of programs written in the language.  (We’re particularly interested in examples that show off the language’s strengths in areas like type-level reasoning and semantic compression.)</p>
  </li>
  <li>
    <p>Start your own working group or community permissionlessly. <code class="language-plaintext highlighter-rouge">goth</code> is like Elm or Julia: it’s an open-source project available under the MIT License.</p>
  </li>
  <li>
    <p>There is a <a href="https://bags.fm/BJM8YzhZ6Mu2iccB1RVhHiEGFoU76ivYfAU5nRyKBAGS"><code class="language-plaintext highlighter-rouge">$GOTH</code> ticker on bags.fm</a>.  This is an experimental meme coin which I did not create or launch. Someone designated me as the fee recipient, so I receive 1% of trading volume. I do not endorse, recommend, or promote this token. Claiming fees ≠ endorsement. <code class="language-plaintext highlighter-rouge">$GOTH</code> is a highly speculative instrument with no connection to the goth language project, no roadmap, and no utility. This is not financial advice and I’m not a financial advisor. Memecoins are extremely risky, as most lose nearly all value. I’m claiming these fees out of curiosity about the platform’s model, not because I believe this token has value. Do not buy this expecting to support the goth project:  there are better ways to contribute if that’s your goal (see the above).</p>
  </li>
</ol>

    <h2 style="color: #ff1493; margin: 30px 0 20px 0;">Example</h2>
    <pre class="code-example"><span class="comment"># Matrix normalization with contracts</span>
<span class="keyword">╭─</span> <span class="function">normalize</span> : <span class="type">[n]F</span> <span class="operator">→</span> <span class="type">[n]F</span>
<span class="keyword">│</span>  <span class="operator">⊢</span> len <span class="var">₀</span> <span class="operator">&gt;</span> <span class="number">0</span>
<span class="keyword">│</span>  <span class="operator">⊨</span> abs(norm <span class="var">₀</span> <span class="operator">-</span> sqrt(len <span class="var">₀</span>)) <span class="operator">&lt;</span> <span class="number">0.0001</span>
<span class="keyword">╰─</span> <span class="keyword">let</span> arr <span class="operator">←</span> <span class="var">₀</span> ;
       μ <span class="operator">←</span> <span class="operator">Σ</span> arr <span class="operator">/</span> len arr ;
       σ <span class="operator">←</span> <span class="operator">√</span>(<span class="operator">Σ</span> ((arr <span class="operator">↦</span> (<span class="keyword">λ→</span> <span class="var">₀</span> <span class="operator">-</span> μ)) <span class="operator">↦</span> (<span class="keyword">λ→</span> <span class="var">₀</span> <span class="operator">×</span> <span class="var">₀</span>)) <span class="operator">/</span> len arr)
   <span class="keyword">in</span> (arr <span class="operator">↦</span> (<span class="keyword">λ→</span> <span class="var">₀</span> <span class="operator">-</span> μ)) <span class="operator">↦</span> (<span class="keyword">λ→</span> <span class="var">₀</span> <span class="operator">/</span> σ)</pre>

    <h2 style="color: #ff1493; margin: 30px 0 20px 0;">Status</h2>
    <p style="color: #b19cd9; line-height: 1.8; margin-bottom: 20px;">
        <strong style="color: #ff69b4;">✅ Implemented:</strong> Full interpreter, parser, runtime contracts<br>
        <strong style="color: #ff69b4;">🔲 In Progress:</strong> Type checker, static analysis<br>
        <strong style="color: #ff69b4;">🔲 Planned:</strong> Native compilation (MLIR → LLVM)
    </p>
</div>
