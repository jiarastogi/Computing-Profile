# Refactor notes for `index.html`

The refactored markup lives in `index-refactor.html`. This file explains *what* changed and *why*, so you can read through the reasoning without scrolling past code.

## Changes applied

1. `<div class="header">` → `<header class="header">`
2. Inner menu div → `<nav>` containing a `<ul>` with each link in its own `<li>`
3. `<div class="main-block">`, `<div class="white-block">`, `<div class="grey-block">` → `<section>`
4. The hero section was renamed from `class="main-block" id="main"` → `class="hero" id="hero"` — see "Why rename main → hero" below
5. Comments block moved *inside* `<main>` (it was outside before)
6. `<div class="footer">` → `<footer class="footer">`
7. Removed the duplicate `title` attribute on the profile image
8. Added `aria-current="page"` to the current nav link
9. `<b>Bachelor of AI</b>` → `<strong>Bachelor of AI</strong>`

## Why the nav uses `<ul>` and `<li>`

A navigation menu is, semantically, *a list of links*. Wrapping each link in `<li>` inside a `<ul>` tells screen readers "there are 4 items in this list", which lets a user skip through them or jump past the list entirely. Without the list markup, assistive tech just sees four loose links with no grouping.

It's also a long-standing convention — most accessibility guides (WAI-ARIA Authoring Practices, WebAIM) recommend the `<nav> > <ul> > <li> > <a>` pattern for site navigation.

## Why rename "main" → "hero"

The big banner section at the top of a page is conventionally called a **hero** in web design — it's the eye-catching introduction with a background image, big heading, and short pitch. Naming it `class="hero"` makes that role obvious from the HTML, whereas `class="main-block"` was generic and easily confused with the `<main>` element (different concept entirely — `<main>` is the page's main content region, the hero is just one section inside it).

The id was renamed too (`id="main"` → `id="hero"`) so the CSS hook matches the new name.

## CSS changes in `websystems.css`

Two additions were made, and **nothing was removed** — the other three pages still use `.main-block`, `#past`, `#future`, `#comments`, and the existing `.menu` rule, so all of those are left exactly as they were.

### 1. New `.hero` and `#hero` rules

A new `.hero` rule was added that mirrors the existing `.main-block` rule (same padding, same white text, same background sizing). And a new `#hero` rule was added that uses the same `flowers.jpg` background that `#main` did. The result: the home page hero looks identical to before, but it's now driven by `hero`-named selectors that match the renamed HTML.

### 2. Two new lines inside `.menu`

The `.menu` class moved from a `<div>` onto the new `<ul>`. Browsers add two default styles to `<ul>` that needed to be cancelled:

- `list-style: none;` — removes the bullet points
- `padding-left: 0;` — removes the default left indent

These two lines are safe additions for the other pages too. Their menus are still `<div class="container menu">`, and `<div>` elements have no list bullets and no default left padding, so the new rules are CSS no-ops on those pages until they get refactored as well.

## New "My Projects" section

A new section was added between **My Past** and **My Future**, showcasing four GitHub projects in a 2×2 grid. The placement is deliberate — Past explains where I came from, Projects shows what I've built so far, Future explains where I'm going. The grid sits inside a `<section class="white-block" id="projects">` so it reuses the existing white-block styling.

### Why each card is an `<article>`

Each project card is wrapped in `<article>`, not `<div>`. An `<article>` represents *self-contained, independently distributable content* — a project description fits exactly: it has its own heading, its own copy, and would still make sense if you copied just that card to another page or a feed reader. The `<div class="project-header">` inside each article is a plain layout wrapper for the title + badge row, so `<div>` is correct there (no semantic meaning beyond "lay these two things out side by side").

### CSS additions in `websystems.css`

A new `/*Project Cards*/` block was appended to the bottom of the stylesheet with these classes:

- `.projects-grid` — two-column grid (`grid-template-columns: 1fr 1fr` means "two equal columns")
- `.project-card` — white card with a soft light-blue border and a subtle shadow, reusing the existing palette
- `.project-header` — flexbox row that puts the title on the left and the "Public" badge on the right
- `.badge` — pill-shaped tag using the existing `#D2E2F1` / `#3b6ea5` palette
- `.project-lang` + `.lang-dot` — the small coloured circle next to each language name, with `.lang-php`, `.lang-html`, `.lang-python` providing the GitHub-style language colours

Nothing existing was removed; all new styles sit at the end of the file and do not affect any other page.

## Note on inner `<div>`s

The inner `<div class="container">`, `<div class="half">`, and the unnamed wrapper `<div>` around the `<h1>` are all kept as plain `<div>`s. That's correct — these exist purely for layout (centring, two-column flex, grouping for CSS). HTML5 has no semantic tag for "this is a layout wrapper", so `<div>` is the right choice for those.

The rule of thumb: use a semantic tag when the element has *meaning* (it's a header, a section, a navigation block). Use `<div>` when the element exists *only* to give CSS something to hook onto.
