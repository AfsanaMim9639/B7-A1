<div align="center">

<svg width="100%" height="8" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <linearGradient id="neon-top" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#ff00ff">
        <animate attributeName="stop-color" values="#ff00ff;#00ffff;#ff00ff;#00ff88;#ff00ff" dur="3s" repeatCount="indefinite"/>
      </stop>
      <stop offset="50%" stop-color="#00ffff">
        <animate attributeName="stop-color" values="#00ffff;#ff00ff;#00ff88;#ff00ff;#00ffff" dur="3s" repeatCount="indefinite"/>
      </stop>
      <stop offset="100%" stop-color="#00ff88">
        <animate attributeName="stop-color" values="#00ff88;#ff00ff;#00ffff;#ff00ff;#00ff88" dur="3s" repeatCount="indefinite"/>
      </stop>
    </linearGradient>
  </defs>
  <rect width="100%" height="8" rx="4" fill="url(#neon-top)"/>
</svg>

# `any` is a Trap — Here's Why `unknown` is Your Real Friend

<svg width="100%" height="8" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <linearGradient id="neon-sub" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#00ff88">
        <animate attributeName="stop-color" values="#00ff88;#ff00ff;#00ffff;#ff00ff;#00ff88" dur="3s" repeatCount="indefinite"/>
      </stop>
      <stop offset="50%" stop-color="#ff00ff">
        <animate attributeName="stop-color" values="#ff00ff;#00ffff;#ff00ff;#00ff88;#ff00ff" dur="3s" repeatCount="indefinite"/>
      </stop>
      <stop offset="100%" stop-color="#00ffff">
        <animate attributeName="stop-color" values="#00ffff;#ff00ff;#00ff88;#ff00ff;#00ffff" dur="3s" repeatCount="indefinite"/>
      </stop>
    </linearGradient>
  </defs>
  <rect width="100%" height="8" rx="4" fill="url(#neon-sub)"/>
</svg>

</div>

<br/>

When I first started learning TypeScript, seeing `any` felt like a relief. No red squiggles, no compiler yelling at me, everything just… worked. But after a while, I realized — it wasn't a feature. It was me telling TypeScript to look the other way while I wrote potentially broken code.

---

## So What Does `any` Actually Do?

Simply put — the moment you use `any`, TypeScript goes completely silent. It stops checking. It trusts you blindly, even when you're wrong.

<div align="center">

<svg width="720" height="220" xmlns="http://www.w3.org/2000/svg" style="border-radius:12px">
  <defs>
    <linearGradient id="bg1" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#0f0f1a"/>
      <stop offset="100%" stop-color="#1a1028"/>
    </linearGradient>
    <filter id="glow1">
      <feGaussianBlur stdDeviation="2" result="blur"/>
      <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>
    <!-- animated neon border -->
    <linearGradient id="ng1" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" stop-color="#ff00ff">
        <animate attributeName="stop-color" values="#ff00ff;#00ffff;#00ff88;#ff00ff" dur="2.5s" repeatCount="indefinite"/>
      </stop>
      <stop offset="100%" stop-color="#00ffff">
        <animate attributeName="stop-color" values="#00ffff;#00ff88;#ff00ff;#00ffff" dur="2.5s" repeatCount="indefinite"/>
      </stop>
    </linearGradient>
  </defs>
  <rect width="720" height="220" rx="12" fill="url(#bg1)"/>
  <rect width="718" height="218" x="1" y="1" rx="12" fill="none" stroke="url(#ng1)" stroke-width="2"/>
  <!-- header bar -->
  <rect width="720" height="36" rx="12" fill="#1e1e2e"/>
  <rect width="720" height="12" y="24" fill="#1e1e2e"/>
  <circle cx="18" cy="18" r="6" fill="#ff5f57"/>
  <circle cx="36" cy="18" r="6" fill="#ffbd2e"/>
  <circle cx="54" cy="18" r="6" fill="#28ca41"/>
  <text x="360" y="22" text-anchor="middle" fill="#555" font-family="monospace" font-size="11">any — the silent killer</text>
  <!-- code lines -->
  <text x="24" y="62" font-family="monospace" font-size="13" fill="#c084fc">function </text>
  <text x="102" y="62" font-family="monospace" font-size="13" fill="#60a5fa">processData</text>
  <text x="200" y="62" font-family="monospace" font-size="13" fill="#e2e8f0">(data: </text>
  <text x="254" y="62" font-family="monospace" font-size="13" fill="#f87171">any</text>
  <text x="278" y="62" font-family="monospace" font-size="13" fill="#e2e8f0">) {</text>

  <text x="44" y="90" font-family="monospace" font-size="13" fill="#94a3b8">data</text>
  <text x="76" y="90" font-family="monospace" font-size="13" fill="#e2e8f0">.user.profile.name.</text>
  <text x="298" y="90" font-family="monospace" font-size="13" fill="#60a5fa">toUpperCase</text>
  <text x="390" y="90" font-family="monospace" font-size="13" fill="#e2e8f0">();</text>
  <text x="430" y="90" font-family="monospace" font-size="12" fill="#22c55e">// compiler: 👍</text>

  <text x="44" y="118" font-family="monospace" font-size="13" fill="#94a3b8">data</text>
  <text x="76" y="118" font-family="monospace" font-size="13" fill="#e2e8f0">.</text>
  <text x="84" y="118" font-family="monospace" font-size="13" fill="#60a5fa">thisDoesntExist</text>
  <text x="210" y="118" font-family="monospace" font-size="13" fill="#e2e8f0">();</text>
  <text x="430" y="118" font-family="monospace" font-size="12" fill="#22c55e">// compiler: 👍</text>

  <text x="44" y="146" font-family="monospace" font-size="13" fill="#94a3b8">data</text>
  <text x="76" y="146" font-family="monospace" font-size="13" fill="#e2e8f0"> + </text>
  <text x="100" y="146" font-family="monospace" font-size="13" fill="#fb923c">9999</text>
  <text x="136" y="146" font-family="monospace" font-size="13" fill="#e2e8f0">;</text>
  <text x="430" y="146" font-family="monospace" font-size="12" fill="#22c55e">// compiler: 👍</text>

  <text x="24" y="174" font-family="monospace" font-size="13" fill="#e2e8f0">}</text>

  <text x="24" y="204" font-family="monospace" font-size="11" fill="#f87171">// No errors at compile time. Everything explodes at runtime.</text>
</svg>

</div>

The worst part? `any` doesn't stay in one place. Once you use it somewhere, it starts spreading — through function returns, variable assignments, down the call chain. Slowly, silently, it hollows out your type safety. You don't even notice until something breaks in production.

---

## Why `unknown` is the Right Choice

`unknown` can hold any value too — just like `any`. But here's the difference: it won't let you *use* that value until you prove what it actually is. TypeScript won't budge.

<div align="center">

<svg width="720" height="260" xmlns="http://www.w3.org/2000/svg" style="border-radius:12px">
  <defs>
    <linearGradient id="bg2" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#0f1a0f"/>
      <stop offset="100%" stop-color="#0f1a1a"/>
    </linearGradient>
    <linearGradient id="ng2" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" stop-color="#00ff88">
        <animate attributeName="stop-color" values="#00ff88;#00ffff;#ff00ff;#00ff88" dur="2.5s" repeatCount="indefinite"/>
      </stop>
      <stop offset="100%" stop-color="#00ffff">
        <animate attributeName="stop-color" values="#00ffff;#ff00ff;#00ff88;#00ffff" dur="2.5s" repeatCount="indefinite"/>
      </stop>
    </linearGradient>
  </defs>
  <rect width="720" height="260" rx="12" fill="url(#bg2)"/>
  <rect width="718" height="258" x="1" y="1" rx="12" fill="none" stroke="url(#ng2)" stroke-width="2"/>
  <rect width="720" height="36" rx="12" fill="#1a2e1a"/>
  <rect width="720" height="12" y="24" fill="#1a2e1a"/>
  <circle cx="18" cy="18" r="6" fill="#ff5f57"/>
  <circle cx="36" cy="18" r="6" fill="#ffbd2e"/>
  <circle cx="54" cy="18" r="6" fill="#28ca41"/>
  <text x="360" y="22" text-anchor="middle" fill="#555" font-family="monospace" font-size="11">unknown — forced to prove it</text>

  <text x="24" y="62" font-family="monospace" font-size="13" fill="#c084fc">let </text>
  <text x="50" y="62" font-family="monospace" font-size="13" fill="#e2e8f0">response: </text>
  <text x="134" y="62" font-family="monospace" font-size="13" fill="#34d399">unknown</text>
  <text x="204" y="62" font-family="monospace" font-size="13" fill="#e2e8f0"> = </text>
  <text x="228" y="62" font-family="monospace" font-size="13" fill="#60a5fa">fetch</text>
  <text x="264" y="62" font-family="monospace" font-size="13" fill="#e2e8f0">("/api/data");</text>

  <text x="24" y="94" font-family="monospace" font-size="13" fill="#94a3b8">response</text>
  <text x="96" y="94" font-family="monospace" font-size="13" fill="#e2e8f0">.name;</text>
  <text x="310" y="94" font-family="monospace" font-size="12" fill="#f87171">// ❌ Error — prove it first</text>

  <text x="24" y="122" font-family="monospace" font-size="13" fill="#94a3b8">response</text>
  <text x="96" y="122" font-family="monospace" font-size="13" fill="#e2e8f0">.</text>
  <text x="104" y="122" font-family="monospace" font-size="13" fill="#60a5fa">toUpperCase</text>
  <text x="200" y="122" font-family="monospace" font-size="13" fill="#e2e8f0">();</text>
  <text x="310" y="122" font-family="monospace" font-size="12" fill="#f87171">// ❌ Error — TypeScript won't budge</text>

  <!-- divider -->
  <line x1="24" y1="140" x2="696" y2="140" stroke="#2a3a2a" stroke-width="1"/>
  <text x="24" y="162" font-family="monospace" font-size="12" fill="#4b5563">// But once you prove it, everything works fine ✓</text>

  <text x="24" y="188" font-family="monospace" font-size="13" fill="#c084fc">if </text>
  <text x="44" y="188" font-family="monospace" font-size="13" fill="#e2e8f0">(</text>
  <text x="52" y="188" font-family="monospace" font-size="13" fill="#c084fc">typeof </text>
  <text x="110" y="188" font-family="monospace" font-size="13" fill="#94a3b8">response</text>
  <text x="182" y="188" font-family="monospace" font-size="13" fill="#e2e8f0"> === </text>
  <text x="218" y="188" font-family="monospace" font-size="13" fill="#fbbf24">"string"</text>
  <text x="290" y="188" font-family="monospace" font-size="13" fill="#e2e8f0">) {</text>

  <text x="44" y="216" font-family="monospace" font-size="13" fill="#94a3b8">response</text>
  <text x="116" y="216" font-family="monospace" font-size="13" fill="#e2e8f0">.</text>
  <text x="124" y="216" font-family="monospace" font-size="13" fill="#60a5fa">toUpperCase</text>
  <text x="220" y="216" font-family="monospace" font-size="13" fill="#e2e8f0">();</text>
  <text x="310" y="216" font-family="monospace" font-size="12" fill="#22c55e">// ✅ Safe now</text>

  <text x="24" y="244" font-family="monospace" font-size="13" fill="#e2e8f0">}</text>
</svg>

</div>

Bottom line — `any` says *"I don't know, just deal with it."* `unknown` says *"I don't know, but I'm not moving until we figure it out."*

---

## Type Narrowing — How You Prove It

Type narrowing is just you showing TypeScript what a value actually is, inside a conditional block. TypeScript watches your checks and adjusts what it knows — this is called **control flow analysis**. Here are the four main ways to do it.

---

### 1. `typeof` Guard — for primitives

<div align="center">

<svg width="720" height="180" xmlns="http://www.w3.org/2000/svg" style="border-radius:12px">
  <defs>
    <linearGradient id="bg3" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#0f0f1a"/>
      <stop offset="100%" stop-color="#1a1028"/>
    </linearGradient>
    <linearGradient id="ng3" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#c084fc">
        <animate attributeName="stop-color" values="#c084fc;#60a5fa;#34d399;#c084fc" dur="3s" repeatCount="indefinite"/>
      </stop>
      <stop offset="100%" stop-color="#60a5fa">
        <animate attributeName="stop-color" values="#60a5fa;#34d399;#c084fc;#60a5fa" dur="3s" repeatCount="indefinite"/>
      </stop>
    </linearGradient>
  </defs>
  <rect width="720" height="180" rx="12" fill="url(#bg3)"/>
  <rect width="718" height="178" x="1" y="1" rx="12" fill="none" stroke="url(#ng3)" stroke-width="2"/>
  <rect width="720" height="36" rx="12" fill="#1e1e2e"/>
  <rect width="720" height="12" y="24" fill="#1e1e2e"/>
  <circle cx="18" cy="18" r="6" fill="#ff5f57"/>
  <circle cx="36" cy="18" r="6" fill="#ffbd2e"/>
  <circle cx="54" cy="18" r="6" fill="#28ca41"/>
  <text x="360" y="22" text-anchor="middle" fill="#555" font-family="monospace" font-size="11">typeof guard</text>

  <text x="24" y="64" font-family="monospace" font-size="13" fill="#c084fc">function </text>
  <text x="102" y="64" font-family="monospace" font-size="13" fill="#60a5fa">greet</text>
  <text x="136" y="64" font-family="monospace" font-size="13" fill="#e2e8f0">(value: </text>
  <text x="200" y="64" font-family="monospace" font-size="13" fill="#34d399">unknown</text>
  <text x="270" y="64" font-family="monospace" font-size="13" fill="#e2e8f0">) {</text>

  <text x="44" y="92" font-family="monospace" font-size="13" fill="#c084fc">if </text>
  <text x="64" y="92" font-family="monospace" font-size="13" fill="#e2e8f0">(</text>
  <text x="72" y="92" font-family="monospace" font-size="13" fill="#c084fc">typeof </text>
  <text x="130" y="92" font-family="monospace" font-size="13" fill="#94a3b8">value</text>
  <text x="164" y="92" font-family="monospace" font-size="13" fill="#e2e8f0"> === </text>
  <text x="200" y="92" font-family="monospace" font-size="13" fill="#fbbf24">"string"</text>
  <text x="272" y="92" font-family="monospace" font-size="13" fill="#e2e8f0">) {</text>

  <text x="64" y="120" font-family="monospace" font-size="13" fill="#60a5fa">console</text>
  <text x="120" y="120" font-family="monospace" font-size="13" fill="#e2e8f0">.</text>
  <text x="128" y="120" font-family="monospace" font-size="13" fill="#60a5fa">log</text>
  <text x="154" y="120" font-family="monospace" font-size="13" fill="#e2e8f0">(</text>
  <text x="162" y="120" font-family="monospace" font-size="13" fill="#fbbf24">"Hello, "</text>
  <text x="234" y="120" font-family="monospace" font-size="13" fill="#e2e8f0"> + value.</text>
  <text x="306" y="120" font-family="monospace" font-size="13" fill="#60a5fa">toUpperCase</text>
  <text x="406" y="120" font-family="monospace" font-size="13" fill="#e2e8f0">());</text>
  <text x="450" y="120" font-family="monospace" font-size="12" fill="#22c55e">// ✅ string here</text>

  <text x="44" y="148" font-family="monospace" font-size="13" fill="#e2e8f0">}</text>
  <text x="24" y="170" font-family="monospace" font-size="13" fill="#e2e8f0">}</text>
</svg>

</div>

---

### 2. `instanceof` Guard — for classes & errors

<div align="center">

<svg width="720" height="200" xmlns="http://www.w3.org/2000/svg" style="border-radius:12px">
  <defs>
    <linearGradient id="bg4" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#1a0f0f"/>
      <stop offset="100%" stop-color="#1a1028"/>
    </linearGradient>
    <linearGradient id="ng4" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#f87171">
        <animate attributeName="stop-color" values="#f87171;#fb923c;#fbbf24;#f87171" dur="3s" repeatCount="indefinite"/>
      </stop>
      <stop offset="100%" stop-color="#fb923c">
        <animate attributeName="stop-color" values="#fb923c;#fbbf24;#f87171;#fb923c" dur="3s" repeatCount="indefinite"/>
      </stop>
    </linearGradient>
  </defs>
  <rect width="720" height="200" rx="12" fill="url(#bg4)"/>
  <rect width="718" height="198" x="1" y="1" rx="12" fill="none" stroke="url(#ng4)" stroke-width="2"/>
  <rect width="720" height="36" rx="12" fill="#2e1e1e"/>
  <rect width="720" height="12" y="24" fill="#2e1e1e"/>
  <circle cx="18" cy="18" r="6" fill="#ff5f57"/>
  <circle cx="36" cy="18" r="6" fill="#ffbd2e"/>
  <circle cx="54" cy="18" r="6" fill="#28ca41"/>
  <text x="360" y="22" text-anchor="middle" fill="#555" font-family="monospace" font-size="11">instanceof guard</text>

  <text x="24" y="64" font-family="monospace" font-size="13" fill="#c084fc">try </text>
  <text x="56" y="64" font-family="monospace" font-size="13" fill="#e2e8f0">{</text>
  <text x="80" y="64" font-family="monospace" font-size="12" fill="#4b5563">// risky operation</text>

  <text x="24" y="92" font-family="monospace" font-size="13" fill="#e2e8f0">} </text>
  <text x="40" y="92" font-family="monospace" font-size="13" fill="#c084fc">catch </text>
  <text x="92" y="92" font-family="monospace" font-size="13" fill="#e2e8f0">(err: </text>
  <text x="138" y="92" font-family="monospace" font-size="13" fill="#34d399">unknown</text>
  <text x="208" y="92" font-family="monospace" font-size="13" fill="#e2e8f0">) {</text>

  <text x="44" y="120" font-family="monospace" font-size="13" fill="#c084fc">if </text>
  <text x="64" y="120" font-family="monospace" font-size="13" fill="#e2e8f0">(err </text>
  <text x="96" y="120" font-family="monospace" font-size="13" fill="#c084fc">instanceof </text>
  <text x="190" y="120" font-family="monospace" font-size="13" fill="#34d399">Error</text>
  <text x="226" y="120" font-family="monospace" font-size="13" fill="#e2e8f0">) {</text>

  <text x="64" y="148" font-family="monospace" font-size="13" fill="#60a5fa">console</text>
  <text x="120" y="148" font-family="monospace" font-size="13" fill="#e2e8f0">.</text>
  <text x="128" y="148" font-family="monospace" font-size="13" fill="#60a5fa">log</text>
  <text x="154" y="148" font-family="monospace" font-size="13" fill="#e2e8f0">(err.</text>
  <text x="186" y="148" font-family="monospace" font-size="13" fill="#94a3b8">message</text>
  <text x="250" y="148" font-family="monospace" font-size="13" fill="#e2e8f0">);</text>
  <text x="310" y="148" font-family="monospace" font-size="12" fill="#22c55e">// ✅ err is Error here</text>

  <text x="44" y="176" font-family="monospace" font-size="13" fill="#e2e8f0">}</text>
  <text x="24" y="196" font-family="monospace" font-size="13" fill="#e2e8f0">}</text>
</svg>

</div>

This one is especially important for `catch` blocks. TypeScript 4+ makes `catch (err: unknown)` the safe default — and `instanceof Error` is how you handle it properly.

---

### 3. `in` Guard — check if a property exists

<div align="center">

<svg width="720" height="160" xmlns="http://www.w3.org/2000/svg" style="border-radius:12px">
  <defs>
    <linearGradient id="bg5" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#0a1a10"/>
      <stop offset="100%" stop-color="#0f1a1a"/>
    </linearGradient>
    <linearGradient id="ng5" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#34d399">
        <animate attributeName="stop-color" values="#34d399;#60a5fa;#c084fc;#34d399" dur="3s" repeatCount="indefinite"/>
      </stop>
      <stop offset="100%" stop-color="#60a5fa">
        <animate attributeName="stop-color" values="#60a5fa;#c084fc;#34d399;#60a5fa" dur="3s" repeatCount="indefinite"/>
      </stop>
    </linearGradient>
  </defs>
  <rect width="720" height="160" rx="12" fill="url(#bg5)"/>
  <rect width="718" height="158" x="1" y="1" rx="12" fill="none" stroke="url(#ng5)" stroke-width="2"/>
  <rect width="720" height="36" rx="12" fill="#1a2e1e"/>
  <rect width="720" height="12" y="24" fill="#1a2e1e"/>
  <circle cx="18" cy="18" r="6" fill="#ff5f57"/>
  <circle cx="36" cy="18" r="6" fill="#ffbd2e"/>
  <circle cx="54" cy="18" r="6" fill="#28ca41"/>
  <text x="360" y="22" text-anchor="middle" fill="#555" font-family="monospace" font-size="11">in guard</text>

  <text x="24" y="64" font-family="monospace" font-size="13" fill="#c084fc">if </text>
  <text x="44" y="64" font-family="monospace" font-size="13" fill="#e2e8f0">(</text>
  <text x="52" y="64" font-family="monospace" font-size="13" fill="#fbbf24">"email"</text>
  <text x="116" y="64" font-family="monospace" font-size="13" fill="#c084fc"> in </text>
  <text x="148" y="64" font-family="monospace" font-size="13" fill="#94a3b8">user</text>
  <text x="180" y="64" font-family="monospace" font-size="13" fill="#e2e8f0">) {</text>

  <text x="44" y="92" font-family="monospace" font-size="13" fill="#60a5fa">console</text>
  <text x="100" y="92" font-family="monospace" font-size="13" fill="#e2e8f0">.</text>
  <text x="108" y="92" font-family="monospace" font-size="13" fill="#60a5fa">log</text>
  <text x="134" y="92" font-family="monospace" font-size="13" fill="#e2e8f0">(user.</text>
  <text x="174" y="92" font-family="monospace" font-size="13" fill="#94a3b8">email</text>
  <text x="214" y="92" font-family="monospace" font-size="13" fill="#e2e8f0">);</text>
  <text x="310" y="92" font-family="monospace" font-size="12" fill="#22c55e">// ✅ property exists, safe to use</text>

  <text x="24" y="120" font-family="monospace" font-size="13" fill="#e2e8f0">}</text>
  <text x="24" y="148" font-family="monospace" font-size="12" fill="#4b5563">// Great for discriminating union types too</text>
</svg>

</div>

---

### 4. Custom Type Guard — the most powerful one

This is where things get really clean. You write a function once, reuse it everywhere. The magic is in the return type: `val is User`.

<div align="center">

<svg width="720" height="230" xmlns="http://www.w3.org/2000/svg" style="border-radius:12px">
  <defs>
    <linearGradient id="bg6" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#0f0f1a"/>
      <stop offset="100%" stop-color="#1a1028"/>
    </linearGradient>
    <linearGradient id="ng6" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" stop-color="#ff00ff">
        <animate attributeName="stop-color" values="#ff00ff;#00ffff;#fbbf24;#ff00ff" dur="2s" repeatCount="indefinite"/>
      </stop>
      <stop offset="100%" stop-color="#00ffff">
        <animate attributeName="stop-color" values="#00ffff;#fbbf24;#ff00ff;#00ffff" dur="2s" repeatCount="indefinite"/>
      </stop>
    </linearGradient>
  </defs>
  <rect width="720" height="230" rx="12" fill="url(#bg6)"/>
  <rect width="718" height="228" x="1" y="1" rx="12" fill="none" stroke="url(#ng6)" stroke-width="2"/>
  <rect width="720" height="36" rx="12" fill="#1e1e2e"/>
  <rect width="720" height="12" y="24" fill="#1e1e2e"/>
  <circle cx="18" cy="18" r="6" fill="#ff5f57"/>
  <circle cx="36" cy="18" r="6" fill="#ffbd2e"/>
  <circle cx="54" cy="18" r="6" fill="#28ca41"/>
  <text x="360" y="22" text-anchor="middle" fill="#555" font-family="monospace" font-size="11">custom type guard</text>

  <text x="24" y="64" font-family="monospace" font-size="13" fill="#c084fc">function </text>
  <text x="102" y="64" font-family="monospace" font-size="13" fill="#60a5fa">isUser</text>
  <text x="144" y="64" font-family="monospace" font-size="13" fill="#e2e8f0">(val: </text>
  <text x="188" y="64" font-family="monospace" font-size="13" fill="#34d399">unknown</text>
  <text x="258" y="64" font-family="monospace" font-size="13" fill="#e2e8f0">): val </text>
  <text x="308" y="64" font-family="monospace" font-size="13" fill="#c084fc">is </text>
  <text x="330" y="64" font-family="monospace" font-size="13" fill="#34d399">User</text>
  <text x="362" y="64" font-family="monospace" font-size="13" fill="#e2e8f0"> {</text>

  <text x="44" y="92" font-family="monospace" font-size="13" fill="#c084fc">return </text>
  <text x="98" y="92" font-family="monospace" font-size="13" fill="#e2e8f0">(</text>

  <text x="64" y="118" font-family="monospace" font-size="13" fill="#c084fc">typeof </text>
  <text x="122" y="118" font-family="monospace" font-size="13" fill="#94a3b8">val</text>
  <text x="146" y="118" font-family="monospace" font-size="13" fill="#e2e8f0"> === </text>
  <text x="182" y="118" font-family="monospace" font-size="13" fill="#fbbf24">"object"</text>
  <text x="254" y="118" font-family="monospace" font-size="13" fill="#e2e8f0"> &&</text>
  <text x="284" y="118" font-family="monospace" font-size="13" fill="#94a3b8"> val</text>
  <text x="316" y="118" font-family="monospace" font-size="13" fill="#e2e8f0"> !== </text>
  <text x="360" y="118" font-family="monospace" font-size="13" fill="#c084fc">null</text>
  <text x="392" y="118" font-family="monospace" font-size="13" fill="#e2e8f0"> &&</text>

  <text x="64" y="146" font-family="monospace" font-size="13" fill="#fbbf24">"id"</text>
  <text x="96" y="146" font-family="monospace" font-size="13" fill="#c084fc"> in </text>
  <text x="128" y="146" font-family="monospace" font-size="13" fill="#94a3b8">val</text>
  <text x="152" y="146" font-family="monospace" font-size="13" fill="#e2e8f0"> &&</text>
  <text x="180" y="146" font-family="monospace" font-size="13" fill="#fbbf24"> "email"</text>
  <text x="254" y="146" font-family="monospace" font-size="13" fill="#c084fc"> in </text>
  <text x="286" y="146" font-family="monospace" font-size="13" fill="#94a3b8">val</text>

  <text x="44" y="174" font-family="monospace" font-size="13" fill="#e2e8f0">);</text>

  <text x="24" y="202" font-family="monospace" font-size="13" fill="#e2e8f0">}</text>
  <text x="24" y="222" font-family="monospace" font-size="12" fill="#4b5563">// If this returns true → TypeScript knows val is User, everywhere you call it</text>
</svg>

</div>

---

## Putting It All Together — Safe API Response Parsing

Here's a real-world example — fetching user data from an API, handling it safely from start to finish.

<div align="center">

<svg width="720" height="370" xmlns="http://www.w3.org/2000/svg" style="border-radius:12px">
  <defs>
    <linearGradient id="bg7" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#0f1018"/>
      <stop offset="100%" stop-color="#18100f"/>
    </linearGradient>
    <linearGradient id="ng7" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" stop-color="#ff00ff">
        <animate attributeName="stop-color" values="#ff00ff;#00ffff;#00ff88;#fbbf24;#ff00ff" dur="3s" repeatCount="indefinite"/>
      </stop>
      <stop offset="50%" stop-color="#00ffff">
        <animate attributeName="stop-color" values="#00ffff;#00ff88;#fbbf24;#ff00ff;#00ffff" dur="3s" repeatCount="indefinite"/>
      </stop>
      <stop offset="100%" stop-color="#00ff88">
        <animate attributeName="stop-color" values="#00ff88;#fbbf24;#ff00ff;#00ffff;#00ff88" dur="3s" repeatCount="indefinite"/>
      </stop>
    </linearGradient>
  </defs>
  <rect width="720" height="370" rx="12" fill="url(#bg7)"/>
  <rect width="718" height="368" x="1" y="1" rx="12" fill="none" stroke="url(#ng7)" stroke-width="2.5"/>
  <rect width="720" height="36" rx="12" fill="#1e1a2e"/>
  <rect width="720" height="12" y="24" fill="#1e1a2e"/>
  <circle cx="18" cy="18" r="6" fill="#ff5f57"/>
  <circle cx="36" cy="18" r="6" fill="#ffbd2e"/>
  <circle cx="54" cy="18" r="6" fill="#28ca41"/>
  <text x="360" y="22" text-anchor="middle" fill="#555" font-family="monospace" font-size="11">real-world safe API parsing</text>

  <!-- interface -->
  <text x="24" y="62" font-family="monospace" font-size="13" fill="#c084fc">interface </text>
  <text x="96" y="62" font-family="monospace" font-size="13" fill="#34d399">User</text>
  <text x="124" y="62" font-family="monospace" font-size="13" fill="#e2e8f0"> { id: </text>
  <text x="182" y="62" font-family="monospace" font-size="13" fill="#34d399">number</text>
  <text x="240" y="62" font-family="monospace" font-size="13" fill="#e2e8f0">; name: </text>
  <text x="302" y="62" font-family="monospace" font-size="13" fill="#34d399">string</text>
  <text x="352" y="62" font-family="monospace" font-size="13" fill="#e2e8f0">; email: </text>
  <text x="416" y="62" font-family="monospace" font-size="13" fill="#34d399">string</text>
  <text x="466" y="62" font-family="monospace" font-size="13" fill="#e2e8f0">; }</text>

  <line x1="24" y1="78" x2="696" y2="78" stroke="#2a2a3a" stroke-width="1"/>

  <!-- type guard -->
  <text x="24" y="100" font-family="monospace" font-size="13" fill="#c084fc">function </text>
  <text x="102" y="100" font-family="monospace" font-size="13" fill="#60a5fa">isUser</text>
  <text x="144" y="100" font-family="monospace" font-size="13" fill="#e2e8f0">(val: </text>
  <text x="188" y="100" font-family="monospace" font-size="13" fill="#34d399">unknown</text>
  <text x="258" y="100" font-family="monospace" font-size="13" fill="#e2e8f0">): val </text>
  <text x="308" y="100" font-family="monospace" font-size="13" fill="#c084fc">is </text>
  <text x="330" y="100" font-family="monospace" font-size="13" fill="#34d399">User</text>
  <text x="362" y="100" font-family="monospace" font-size="13" fill="#e2e8f0"> {</text>

  <text x="44" y="126" font-family="monospace" font-size="13" fill="#c084fc">return </text>
  <text x="98" y="126" font-family="monospace" font-size="13" fill="#c084fc">typeof </text>
  <text x="156" y="126" font-family="monospace" font-size="13" fill="#94a3b8">val</text>
  <text x="180" y="126" font-family="monospace" font-size="13" fill="#e2e8f0"> === </text>
  <text x="216" y="126" font-family="monospace" font-size="13" fill="#fbbf24">"object"</text>
  <text x="288" y="126" font-family="monospace" font-size="13" fill="#e2e8f0"> && val !== </text>
  <text x="390" y="126" font-family="monospace" font-size="13" fill="#c084fc">null</text>

  <text x="108" y="152" font-family="monospace" font-size="13" fill="#e2e8f0">&amp;&amp; </text>
  <text x="136" y="152" font-family="monospace" font-size="13" fill="#fbbf24">"id"</text>
  <text x="168" y="152" font-family="monospace" font-size="13" fill="#c084fc"> in </text>
  <text x="200" y="152" font-family="monospace" font-size="13" fill="#94a3b8">val</text>
  <text x="224" y="152" font-family="monospace" font-size="13" fill="#e2e8f0"> &amp;&amp; </text>
  <text x="260" y="152" font-family="monospace" font-size="13" fill="#fbbf24">"name"</text>
  <text x="314" y="152" font-family="monospace" font-size="13" fill="#c084fc"> in </text>
  <text x="346" y="152" font-family="monospace" font-size="13" fill="#94a3b8">val</text>
  <text x="370" y="152" font-family="monospace" font-size="13" fill="#e2e8f0"> &amp;&amp; </text>
  <text x="406" y="152" font-family="monospace" font-size="13" fill="#fbbf24">"email"</text>
  <text x="466" y="152" font-family="monospace" font-size="13" fill="#c084fc"> in </text>
  <text x="498" y="152" font-family="monospace" font-size="13" fill="#94a3b8">val</text>
  <text x="522" y="152" font-family="monospace" font-size="13" fill="#e2e8f0">;</text>

  <text x="24" y="174" font-family="monospace" font-size="13" fill="#e2e8f0">}</text>

  <line x1="24" y1="188" x2="696" y2="188" stroke="#2a2a3a" stroke-width="1"/>

  <!-- async function -->
  <text x="24" y="210" font-family="monospace" font-size="13" fill="#c084fc">async function </text>
  <text x="138" y="210" font-family="monospace" font-size="13" fill="#60a5fa">getUser</text>
  <text x="192" y="210" font-family="monospace" font-size="13" fill="#e2e8f0">(id: </text>
  <text x="228" y="210" font-family="monospace" font-size="13" fill="#34d399">number</text>
  <text x="286" y="210" font-family="monospace" font-size="13" fill="#e2e8f0">): </text>
  <text x="310" y="210" font-family="monospace" font-size="13" fill="#34d399">Promise</text>
  <text x="366" y="210" font-family="monospace" font-size="13" fill="#e2e8f0">&lt;</text>
  <text x="378" y="210" font-family="monospace" font-size="13" fill="#34d399">User</text>
  <text x="410" y="210" font-family="monospace" font-size="13" fill="#e2e8f0">&gt; {</text>

  <text x="44" y="236" font-family="monospace" font-size="13" fill="#c084fc">const </text>
  <text x="90" y="236" font-family="monospace" font-size="13" fill="#94a3b8">res</text>
  <text x="114" y="236" font-family="monospace" font-size="13" fill="#e2e8f0">  = </text>
  <text x="142" y="236" font-family="monospace" font-size="13" fill="#c084fc">await </text>
  <text x="192" y="236" font-family="monospace" font-size="13" fill="#60a5fa">fetch</text>
  <text x="228" y="236" font-family="monospace" font-size="13" fill="#e2e8f0">(`/api/users/${id}`);</text>

  <text x="44" y="262" font-family="monospace" font-size="13" fill="#c084fc">const </text>
  <text x="90" y="262" font-family="monospace" font-size="13" fill="#94a3b8">data</text>
  <text x="122" y="262" font-family="monospace" font-size="13" fill="#e2e8f0">: </text>
  <text x="134" y="262" font-family="monospace" font-size="13" fill="#34d399">unknown</text>
  <text x="204" y="262" font-family="monospace" font-size="13" fill="#e2e8f0"> = </text>
  <text x="228" y="262" font-family="monospace" font-size="13" fill="#c084fc">await </text>
  <text x="278" y="262" font-family="monospace" font-size="13" fill="#94a3b8">res</text>
  <text x="302" y="262" font-family="monospace" font-size="13" fill="#e2e8f0">.</text>
  <text x="310" y="262" font-family="monospace" font-size="13" fill="#60a5fa">json</text>
  <text x="342" y="262" font-family="monospace" font-size="13" fill="#e2e8f0">();</text>
  <text x="400" y="262" font-family="monospace" font-size="12" fill="#4b5563">// unknown, not any</text>

  <text x="44" y="290" font-family="monospace" font-size="13" fill="#c084fc">if </text>
  <text x="64" y="290" font-family="monospace" font-size="13" fill="#e2e8f0">(!</text>
  <text x="80" y="290" font-family="monospace" font-size="13" fill="#60a5fa">isUser</text>
  <text x="120" y="290" font-family="monospace" font-size="13" fill="#e2e8f0">(data)) </text>
  <text x="180" y="290" font-family="monospace" font-size="13" fill="#c084fc">throw new </text>
  <text x="256" y="290" font-family="monospace" font-size="13" fill="#34d399">Error</text>
  <text x="292" y="290" font-family="monospace" font-size="13" fill="#e2e8f0">(</text>
  <text x="300" y="290" font-family="monospace" font-size="13" fill="#fbbf24">"Unexpected shape"</text>
  <text x="438" y="290" font-family="monospace" font-size="13" fill="#e2e8f0">);</text>

  <text x="44" y="318" font-family="monospace" font-size="13" fill="#c084fc">return </text>
  <text x="98" y="318" font-family="monospace" font-size="13" fill="#94a3b8">data</text>
  <text x="130" y="318" font-family="monospace" font-size="13" fill="#e2e8f0">;</text>
  <text x="310" y="318" font-family="monospace" font-size="12" fill="#22c55e">// ✅ TypeScript is certain — this is User</text>

  <text x="24" y="350" font-family="monospace" font-size="13" fill="#e2e8f0">}</text>
</svg>

</div>

Notice how `res.json()` is typed as `unknown`, not `any`. We don't know what the API returns. Then `isUser` does the verification — if the shape is wrong, we throw. If it's right, TypeScript is fully confident from that point on.

That's safe. That's readable. Anyone on your team can look at it and immediately understand what's happening.

---

## One Thing to Remember

`any` means *"I give up."* `unknown` means *"I'm being careful."*

Anytime data comes from outside your control — an API, `JSON.parse()`, user input, a third-party library — reach for `unknown` first. Then narrow it down. It takes a little more thought upfront, but it saves you from the kind of runtime bugs that only show up at 2am in production.

Trust me on this one.

---

<div align="center">

<svg width="100%" height="8" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <linearGradient id="neon-footer" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#ff00ff">
        <animate attributeName="stop-color" values="#ff00ff;#00ffff;#00ff88;#fbbf24;#ff00ff" dur="3s" repeatCount="indefinite"/>
      </stop>
      <stop offset="50%" stop-color="#00ffff">
        <animate attributeName="stop-color" values="#00ffff;#00ff88;#fbbf24;#ff00ff;#00ffff" dur="3s" repeatCount="indefinite"/>
      </stop>
      <stop offset="100%" stop-color="#00ff88">
        <animate attributeName="stop-color" values="#00ff88;#fbbf24;#ff00ff;#00ffff;#00ff88" dur="3s" repeatCount="indefinite"/>
      </stop>
    </linearGradient>
  </defs>
  <rect width="100%" height="8" rx="4" fill="url(#neon-footer)"/>
</svg>

*Part of the TypeScript Deep Dive series.*

</div>