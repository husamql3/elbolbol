# CLAUDE.md

## Project

Frontend interview study notes — migrated from Notion to GitHub-flavored Markdown.

## Structure

- `questions/` — topic files: `js.md`, `react.md`, `ts.md`
- Each question uses `<details><summary>` for expand/collapse
- Answers go inside `<details>` after a blank line (enables markdown rendering)

## Markdown rules

- **Inside `<summary>` tags**: use `<code>` HTML tags, NOT backticks — markdown is not processed inside HTML tags
- **Inside `<details>` body** (after `</summary>` + blank line): normal markdown works — use backticks, tables, code blocks freely
- Escape angle brackets in `<summary>` when they appear in type params: `&lt;T&gt;` not `<T>`
- Code blocks use `jsx` or `javascript` language hints

## When adding new questions

```html
<details>
<summary>Question with <code>inline code</code> here</summary>

Answer in **normal markdown** with `backticks`, tables, code blocks, etc.

</details>
```
