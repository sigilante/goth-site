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
