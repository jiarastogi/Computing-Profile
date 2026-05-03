# Semantic Audit: `index.html`

## What it does well

- **`<main>` is present** (line 19) — good start, this tells screen readers and search engines where the main content begins.
- **Heading order is sensible**: one `<h1>` (line 24), then `<h2>`s for each section (lines 37, 53, 63). No skipped levels.
- **`alt` text is descriptive** on the profile image (line 30).
- **`lang="en"`, `charset`, and `viewport`** meta tags are all set in the `<head>` — these often get forgotten by beginners.
- **Clear top-to-bottom reading order**: nav → intro → past → future → comments → footer.

## What's missing or weak

### 1. No `<nav>` for the navigation menu (lines 10–17)

```html
<div class="header">
    <div class="container menu">
        <a ...>Home Page</a>
        ...
    </div>
</div>
```

This is a list of site links — it should be wrapped in `<nav>`. The outer wrapper should be `<header>`, not `<div class="header">`.

### 2. No `<header>` element

You use `<div class="header">`. The class name even tells you what the right tag would be.

### 3. No `<footer>` element (lines 70–77)

Same issue — `<div class="footer">` should be `<footer>`. Browsers and assistive tech recognise `<footer>` automatically; a div with a class doesn't carry that meaning.

### 4. The "Comments" block is *outside* `<main>` (lines 61–68)

`</main>` closes on line 59, but the Comments section that follows is clearly main content too. Either move it inside `<main>`, or if you intended it as supplementary, it could be `<aside>` — but really, it belongs inside `<main>`.

### 5. Three content blocks are plain `<div>`s (lines 20, 35, 51)

Each `<div class="...-block">` wraps a self-contained chunk with its own heading. These are textbook `<section>` candidates:

```html
<section class="white-block">
    <div class="container">
        <h2>My Past</h2>
        ...
    </div>
</section>
```

### 6. Minor issues

- Line 30: the `title` attribute duplicates the `alt`. `title` shows a tooltip on hover and is generally redundant when `alt` is good — you can drop it.
- Line 30: no `width`/`height` attributes on the image — adding these helps the browser reserve space and prevents layout jumping while the page loads.
- Line 12: `class="header_current"` marks the current page visually, but for accessibility you should also add `aria-current="page"` on that link.
- Line 26: `<b>Bachelor of AI</b>` — `<b>` is purely visual. If you mean *this is important*, `<strong>` is the semantic choice. (If you just want bold styling with no extra meaning, `<b>` is technically fine.)

## Structure overview

| Current | Should be |
|---|---|
| `<div class="header">` | `<header>` |
| `<div class="container menu">` (links) | `<nav>` |
| `<div class="main-block">`, `<div class="white-block">`, `<div class="grey-block">` | `<section>` |
| `<div class="footer">` | `<footer>` |
| Comments block outside `<main>` | move inside `<main>` |

CSS keeps working unchanged because your selectors (`.header`, `.footer`, `.white-block`) target classes, not tag names. So swapping `<div class="footer">` → `<footer class="footer">` is safe.

## Rating: **6 / 10**

You've got the bones right — `<main>`, good heading hierarchy, alt text, lang attribute. But the page leans on `<div>` for elements that have purpose-built semantic tags (`<header>`, `<nav>`, `<footer>`, `<section>`), and the Comments section escapes `<main>` by accident. Fixing those five things would push this to a solid 9.
