# Title Tag

HTML `<title>` element ka complete deep dive.

## Files
- `minimal.html` — Sirf basic title example
- `index.html` — Complete demo with live character counter, tab preview, search preview
- `professional.html` — Real-world title patterns for every page type
- `notes.md` — Complete deep notes with 25 interview questions
- `README.md` — Yeh file

## Topics Covered
1. Why title tag exists — history
2. Syntax aur rules
3. 13 jagah jahan title dikhta hai
4. Character length by platform (Chrome, Google, Facebook, Twitter)
5. SEO impact — #1 on-page factor
6. Title formulas — 10 proven patterns
7. Unicode aur emoji support
8. Dynamic titles (React, Next.js, SPA)
9. Accessibility (screen readers, WCAG)
10. Browser internals — parsing
11. Edge cases aur gotchas (10)
12. Interview questions (25)
13. Common mistakes
14. Real-world examples (2026)
15. Testing workflow
16. Modern considerations (AI, voice search)

## Key Learnings
- **50-60 characters** = sweet spot
- **Primary keyword front** mein
- **Brand name aakhir** mein (`| Brand`)
- **Unique** har page par
- **Screen readers** sab se pehle title announce karte hain
- **Google ka #1** on-page SEO factor
- **SPA mein dynamic update** zaroori (React Helmet, Next.js metadata)
- **Character count** = visual (emoji 1 char hai, multiple bytes nahi)

## Title Formulas
| Pattern | Example |
|---|---|
| Keyword \| Brand | Full Stack Development \| Abu Bakar |
| How to [X] in [Y] | How to Learn Next.js in 30 Days |
| [Number] [Topic] ([Year]) | 10 CSS Grid Tricks (2026) |
| [Topic] — [Category] \| Brand | Meta Tags — SEO Guide \| Abu Bakar |
| [Question]? | What is DOCTYPE in HTML? |

## DevTools Commands
```javascript
// Read current title
document.title;

// Change title
document.title = "New Title";

// Title element access
document.querySelector('title').textContent;