# DOCTYPE — Complete Notes

## Definition
- `<!DOCTYPE html>` = HTML5 declaration
- Browser ko batata hai: Standards Mode use karo
- Tag nahi, declaration hai
- Closing tag nahi hota

## 3 Rules
1. Pehli line honi chahiye
2. Sirf ek DOCTYPE
3. Kuch bhi iske pehle nahi (comment, BOM, XML decl)

## 2 Modes
- Standards Mode → Modern CSS
- Quirks Mode → IE 5.5 jaisa behavior

## Detect Karne Ka Tareeqa
```javascript
document.compatMode
// "CSS1Compat" = Standards
// "BackCompat" = Quirks