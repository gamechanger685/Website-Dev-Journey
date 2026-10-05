# Body Element

HTML `<body>` element ka complete deep dive.

## Files
- `minimal.html` — Sirf basic body example
- `index.html` — Complete demo with live body info, dimensions, theme toggle
- `professional.html` — Real-world body structure (skip link, header, main, footer)
- `notes.md` — Complete deep notes with 25 interview questions
- `README.md` — Yeh file

## Topics Covered
1. Why body exists
2. Modern vs obsolete attributes
3. Default browser styling (8px margin)
4. Body events (DOMContentLoaded vs load)
5. document.body vs document.documentElement
6. Dimensions (client vs scroll vs offset)
7. Best practice structure (2026)
8. Semantic HTML5 tags
9. SEO impact
10. Accessibility (landmark roles, skip links)
11. Browser rendering (critical path)
12. 10 gotchas
13. 25 interview questions
14. Real-world patterns
15. Modern considerations (dark mode, view transitions)

## Key Learnings
- **Ek page = ek body** (multiple ignore)
- **Sab visible content** body ke andar
- **Default 8px margin** — CSS reset se hatao
- **Semantic structure:** skip → header → main → footer → scripts
- **Skip link pehla** — accessibility ke liye
- **`<main>` sirf ek** per page
- **Scripts end mein** ya defer
- **DOMContentLoaded** vs **load** ka farq
- **document.body** ≠ **document.documentElement**
- **Purane attributes** (bgcolor, text) obsolete

## Body Structure Best Practice
```html
<body>
  <a href="#main" class="skip-link">Skip</a>
  <header><nav>...</nav></header>
  <main id="main">
    <article>...</article>
    <aside>...</aside>
  </main>
  <footer>...</footer>
  <script src="app.js" defer></script>
</body>