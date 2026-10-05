# HTML Root Element — Notes

## Definition
- `<html>` = Document root
- `<head>` aur `<body>` iske andar
- Har HTML page mein ek hi

## Attributes
- lang → Language (MUST)
- dir → Direction (rtl/ltr)
- xmlns → XHTML only (skip)

## lang Values
- en, ur, ar, hi, fr
- en-US, ur-PK (region)
- ur-Latn (Roman Urdu)

## Why lang?
1. Screen reader pronunciation
2. SEO
3. Spell check
4. Translation
5. Font selection
6. CSS hyphens

## dir Values
- ltr → English, Hindi
- rtl → Arabic, Urdu, Hebrew
- auto → Mixed

## Gotchas
1. lang bhoolna → accessibility fail
2. Roman Urdu ke liye lang="ur" → wrong pronunciation
3. xmlns lagana HTML5 mein → unnecessary
4. Multiple html → invalid

## Interview Questions
Q: Root element ka kaam?
A: Document root, language + direction

Q: document.documentElement?
A: <html> element return karta hai

Q: lang vs :lang()?
A: Attribute + CSS selector combo