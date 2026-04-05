# Next.js

<!-- markdownlint-disable MD033 -->

<details>
<summary>What is the difference between <code>template.tsx</code> and <code>layout.tsx</code>?</summary>

Both are special files in the Next.js App Router that wrap child routes, but they differ in how they handle state and re-rendering.

**`layout.tsx`**

- **Persists across navigations** — the component instance is kept alive when the user navigates between sibling routes. State, effects, and DOM are preserved.
- Fetches data once and does not re-render on route changes within its scope.
- Ideal for persistent UI like navigation bars, sidebars, and shared chrome.

**`template.tsx`**

- **Re-mounts on every navigation** — a new instance of the component is created each time the user navigates to a route that uses it. State and effects are reset.
- Runs effects (`useEffect`) and re-fetches data on every navigation.
- Ideal for per-page enter/exit animations, logging page views, or resetting form state on navigation.

**How they work together**

```
layout.tsx        ← stays mounted
  template.tsx    ← re-mounts on navigation
    page.tsx
```

If both exist in the same route segment, the layout wraps the template, which wraps the page. You can use them together when you need some UI to persist (layout) while other UI resets on navigation (template).

**When to use which**

| Scenario | Use |
|---|---|
| Shared nav/sidebar that shouldn't re-render | `layout.tsx` |
| Enter/exit animations per page | `template.tsx` |
| Analytics `useEffect` that should fire on every navigation | `template.tsx` |
| Preserving scroll position or input state across routes | `layout.tsx` |

</details>
