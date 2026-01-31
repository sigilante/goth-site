---
layout: default
title: Keywords Reference
permalink: /docs/keywords/
---

<div class="header-section">
    <h1 class="gothic-header pink">keywords</h1>
    <p class="tagline">reserved words and operators</p>
</div>

<div class="code-section frame">
    <h2 style="color: #ff1493; margin-bottom: 20px;">Control Flow</h2>
    <pre class="code-example"><span class="keyword">if</span> <span class="comment">condition</span> <span class="keyword">then</span> <span class="comment">expression</span> <span class="keyword">else</span> <span class="comment">expression</span>

<span class="keyword">match</span> <span class="comment">expression</span>
  <span class="comment">pattern</span> <span class="operator">→</span> <span class="comment">result</span>
  <span class="comment">pattern</span> <span class="operator">→</span> <span class="comment">result</span></pre>

    <h2 style="color: #ff1493; margin: 30px 0 20px 0;">Bindings</h2>
    <pre class="code-example"><span class="keyword">let</span> <span class="var">x</span> <span class="operator">←</span> <span class="number">5</span> <span class="keyword">in</span> <span class="comment">expression</span>

<span class="keyword">let rec</span> <span class="function">factorial</span> <span class="operator">←</span> <span class="keyword">λ→</span> <span class="comment">...</span></pre>

    <h2 style="color: #ff1493; margin: 30px 0 20px 0;">Functions</h2>
    <pre class="code-example"><span class="keyword">λ→</span> <span class="comment">body</span>                  <span class="comment"># lambda</span>
<span class="keyword">╭─</span> <span class="function">name</span> : <span class="type">Type</span>       <span class="comment"># function declaration</span>
<span class="keyword">│</span>  <span class="operator">⊢</span> <span class="comment">precondition</span>     <span class="comment"># contract</span>
<span class="keyword">│</span>  <span class="operator">⊨</span> <span class="comment">postcondition</span>
<span class="keyword">╰─</span> <span class="comment">body</span></pre>

    <h2 style="color: #ff1493; margin: 30px 0 20px 0;">Operators</h2>
    <pre class="code-example"><span class="operator">→</span>   <span class="comment">function arrow</span>
<span class="operator">←</span>   <span class="comment">binding</span>
<span class="operator">⊢</span>   <span class="comment">precondition (turnstile)</span>
<span class="operator">⊨</span>   <span class="comment">postcondition (models)</span>
<span class="operator">↦</span>   <span class="comment">map</span>
<span class="operator">▸</span>   <span class="comment">filter</span>
<span class="operator">⊗</span>   <span class="comment">zip/product</span>
<span class="operator">⊕</span>   <span class="comment">concat/sum</span>
<span class="operator">∘</span>   <span class="comment">compose</span>
<span class="operator">Σ</span>   <span class="comment">sum reduction</span>
<span class="operator">Π</span>   <span class="comment">product reduction</span>
<span class="operator">√</span>   <span class="comment">square root</span></pre>
</div>
