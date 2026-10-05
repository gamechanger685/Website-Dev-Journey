# HTML Headings h1-h6

HTML heading elements ka complete deep dive.

## Files
- `minimal.html` — Basic heading example
- `index.html` — Complete demo with live hierarchy checker
- `professional.html` — Real-world blog post with proper hierarchy
- `notes.md` — Complete deep notes with 25 interview questions
- `README.md` — Yeh file

## Topics Covered
1. Why headings exist
2. 6 levels (h1-h6)
3. Default browser sizes
4. Heading hierarchy
5. SEO impact (Google ranking)
6. Accessibility (screen reader navigation)
7. Attributes (modern + obsolete)
8. Anchor linking
9. Live hierarchy checker
10. Common mistakes
11. Real-world patterns (blog, docs, portfolio)
12. Modern considerations (2026)

## Key Learnings
- **Ek H1 per page** — page ka main topic
- **Logical hierarchy** — H1 → H2 → H3 (skip nahi)
- **Semantic, not style** — size CSS se, structure heading se
- **Descriptive text** — "Intro" nahi, "Intro to HTML" better
- **Keywords naturally** — stuff mat karo
- **Screen readers** — H key se navigate
- **Google** — H1 important ranking factor
- **Anchor linking** — `id` attribute se TOC banao
- **Obsolete attributes** — align, bgcolor

## Quick Reference
| Tag |  Size  |         Use Case        |
|-----|--------|-------------------------|
| h1  | 2em    | Page title (1 per page) |
| h2  | 1.5em  | Major sections          |
| h3  | 1.17em | Subsections             |
| h4  | 1em    | Sub-subsections         |
| h5  | 0.83em | Deep levels             |
| h6  | 0.67em | Deepest                  |

## Correct Hierarchy
```html
<h1>Page Title</h1>
<h2>Section 1</h2>
  <h3>Subsection 1.1</h3>
  <h3>Subsection 1.2</h3>
<h2>Section 2</h2>
  <h3>Subsection 2.1</h3>