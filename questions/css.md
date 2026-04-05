# CSS

<details>
<summary>Flexbox vs Grid — when to use which</summary>

**Flexbox** — **1D** layout (row OR column). Content-driven — items size themselves.
**Grid** — **2D** layout (rows AND columns). Layout-driven — you define the grid, items fill it.

```text
Flexbox:  [ item ][ item ][ item ]     → one axis
Grid:     [ item ][ item ][ item ]     → rows AND columns
          [ item ][ item ][ item ]
```

| | Flexbox | Grid |
|---|---|---|
| Axis | One (row or column) | Two (rows and columns) |
| Sizing | Content-out (items decide) | Layout-in (grid decides) |
| Best for | Navbars, buttons, centering, inline layouts | Page layouts, card grids, dashboards |
| Alignment | `justify-content`, `align-items` | Same + `grid-template-areas` |

</details>

<details>
<summary>Flexbox cheatsheet</summary>

- **Container properties:**

```css
.container {
  display: flex;
  flex-direction: row;          /* row | row-reverse | column | column-reverse */
  justify-content: center;      /* main axis: flex-start | center | flex-end | space-between | space-around | space-evenly */
  align-items: center;          /* cross axis: flex-start | center | flex-end | stretch | baseline */
  flex-wrap: wrap;              /* nowrap | wrap | wrap-reverse */
  gap: 16px;                    /* shorthand for row-gap and column-gap */
}
```

- **Item properties:**

```css
.item {
  flex: 1;                      /* shorthand for flex-grow: 1, flex-shrink: 1, flex-basis: 0% */
  align-self: flex-end;         /* override align-items for this item */
  order: 2;                     /* change visual order without changing HTML */
}
```

- **Common patterns:**

```css
/* Center anything */
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Navbar — logo left, links right */
.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Push last item to the right */
.item:last-child {
  margin-left: auto;
}
```

</details>

<details>
<summary>Grid cheatsheet</summary>

- **Container properties:**

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;          /* 3 columns, middle is twice as wide */
  grid-template-rows: auto 1fr auto;            /* header, main (fills space), footer */
  gap: 16px;
}
```

- **Common patterns:**

```css
/* Responsive card grid — auto-fill as many 250px columns as fit */
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 16px;
}

/* Classic page layout with named areas */
.page {
  display: grid;
  grid-template-areas:
    "header  header  header"
    "sidebar content aside"
    "footer  footer  footer";
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.content { grid-area: content; }
.footer  { grid-area: footer; }
```

- **Item placement:**

```css
.item {
  grid-column: 1 / 3;          /* span from column line 1 to 3 */
  grid-row: 1 / 2;             /* span from row line 1 to 2 */
  /* or shorthand */
  grid-column: span 2;         /* span 2 columns from current position */
}
```

- **`auto-fill` vs `auto-fit`:**
  - `auto-fill` — creates as many tracks as fit, even if empty
  - `auto-fit` — same, but **collapses empty tracks** so items stretch to fill the space

</details>
