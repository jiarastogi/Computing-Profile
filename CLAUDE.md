# Computing-Profile
A personal portfolio site about my computing journey — past experiences, future aspirations, and a page to describe the design thinking behind the site.

I'm a beginner with HTML and CSS, so please explain things simply and avoid introducing new tools or concepts unless I ask.

## Tech stack
- **HTML** — plain, hand-written. Pages: `index.html`, `past.html`, `future.html`, `comments.html`.
- **CSS** — a single stylesheet, `websystems.css`. No frameworks (no Bootstrap, Tailwind, etc.).
- **Images** — stored in the `images/` folder, referenced from CSS and HTML.
- **No build step, no JavaScript, no dependencies.** Open any `.html` file in a browser and it just works.

## Style goals
- **Colour palette** (already used in `websystems.css`):
  - Navy `#243A5E` — headers, headings
  - Light blue `#D2E2F1` — soft backgrounds, accents
  - Medium blue `#3b6ea5` — links, CTAs, table accents
  - Dark grey `#2b2b2b` — body text and footer
  - White `#FFFFFF` — clean backgrounds
- **Typography** — Gill Sans stack, 150% line height, comfortable to read.
- **Layout** — content sits in a centred 70%-wide container; sections alternate white/light-blue blocks; hero sections use a navy gradient over a background image so white text stays readable.
- **Consistent and simple** — reuse existing classes (`.container`, `.grey-block`, `.white-block`, `.half`, `.cta`) instead of inventing new ones where possible.
- **Accessible** — readable contrast, descriptive `alt` text on images, sensible heading order.

## How I'd like Claude Code to help
1. **Explain before changing.** When I ask about HTML/CSS in this project, walk me through what the existing code does in beginner terms before suggesting edits. Point me to the file and line so I can follow along.
2. **Keep edits minimal and consistent.** Reuse the existing colour palette, classes, and patterns in `websystems.css`. Don't introduce frameworks, preprocessors (Sass/Less), JavaScript, or build tools unless I explicitly ask.
3. **Catch beginner mistakes early.** Flag broken/inconsistent things as you notice them — duplicate IDs, missing `alt` attributes, mismatched tags, links pointing to files that don't exist, or styles that won't behave well on smaller screens — and explain why they matter.
