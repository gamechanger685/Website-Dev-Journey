# Meta Tags — Complete Notes

## 1. Meta Tag Kya Hai?

`<meta>` = Metadata element. Self-closing. `<head>` ke andar.

**Matlab:** Data ke baare mein data. User ko nazar nahi aata, lekin **browser, search engines, social media, aur devices** padhte hain.

---

## 2. Position & Order

**Rules:**
- Hamesha `<head>` ke andar
- `charset` sab se pehle (1024 bytes ke andar)
- Baaki order matter nahi — lekin best practice follow karo

**Recommended Order:**
1. `charset`
2. `viewport`
3. `title`
4. `description`
5. `canonical`
6. Open Graph
7. Twitter Cards
8. Favicon
9. Preconnect
10. CSS
11. Scripts

---

## 3. Meta Ke 4 Attribute Types

### 3.1 charset
```html
<meta charset="UTF-8">