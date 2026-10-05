<html> Root Element — Complete Postmortem
Chalo ab 02-html-root-element ka deep dive karte hain.

1. Why Does It Exist?
<html> tag poori document ka root hai. Har cheez iske andar hai — <head> aur <body> dono.

Kyun zaroori hai?

-> Browser ko batata hai: "Yeh HTML document hai"
-> Language aur direction set karta hai
-> Accessibility tools (screen readers) ise use karte hain
-> CSS aur JavaScript document.documentElement se isay access karte hain

Without <html>:

-> Browser implicitly add kar deta hai (auto-fix), lekin aap control kho dete ho
-> Language attribute nahi hoga → Screen readers galat pronunciation
-> SEO mein issue

2. Syntax
html
<html lang="en">
  <head>
    <!-- Metadata -->
  </head>
  <body>
    <!-- Visible content -->
  </body>
</html>
Chhota hai lekin powerful.

3. All Attributes (Complete)
Attribute	            Value	                           Purpose	                                  Zaroori?
lang	                en, ur, ar, fr	                 Document language	                        ✅ Haan
dir	                  ltr, rtl, auto	                 Text direction	                            Recommended
xmlns	                http://www.w3.org/1999/xhtml	   XHTML ke liye (HTML5 mein optional)	      ❌ Nahi
manifest	            URL	                             PWA manifest (deprecated)	                ❌ Nahi
class	                Custom	                         Global attribute	                          Optional
id	                  Custom	                         Global attribute	                          Optional
data-*	              Custom	                         Custom data	                              Optional

4. lang Attribute — Deep Dive
Yeh sab se important attribute hai <html> par.

Values
Two-letter code (ISO 639-1):

en = English
ur = Urdu
ar = Arabic
hi = Hindi
fr = French
zh = Chinese

Two-letter + region (ISO 639-1 + ISO 3166-1):

en-US = English (USA)
en-GB = English (UK)
ur-PK = Urdu (Pakistan)
zh-CN = Chinese (China)

Kyun Zaroori Hai?

1. Screen Readers:
Screen reader lang="en" dekh kar English pronunciation use karta hai. lang="ur" dekh kar Urdu accent. Agar nahi lagaya to galat pronunciation.

2. SEO:
Google ko pata chalta hai page kis language mein hai. Search results mein sahi audience tak pohnchta hai.

3. Spell Check:
Browser spell-check language set karta hai.

4. Translation Tools:
Google Translate ko pata chalta hai source language kya hai.

5. CSS Hyphenation:

css
p { hyphens: auto; }
Language ke rules ke hisaab se words tootenge.

6. Font Selection:
Browser sahi font choose karta hai (Chinese, Arabic, Urdu).

Real-World Example
html
<!-- ❌ GALAT -->
<html>
Problem: Screen reader default (en-US) use karega. Urdu text bhi English accent mein padhega.

html
<!-- ✅ SAHI -->
<html lang="ur">
Fayda: Screen reader Urdu pronunciation use karega.

Mixed Language Content
Agar page English hai lekin beech mein Urdu paragraph hai:

html
<html lang="en">
<body>
  <p>This is English.</p>
  <p lang="ur">یہ اردو ہے۔</p>
</body>
</html>
Rule: Parent lang override karne ke liye child par naya lang lagao.

5. dir Attribute — Text Direction

3 values:
Value	      Matlab	                            Kaunsi Languages
ltr	        Left-to-Right	                      English, Urdu (Roman), Hindi, Chinese
rtl	        Right-to-Left	                      Arabic, Hebrew, Urdu (Arabic script), Persian
auto	      Browser detect kare	                Mixed content

Example: Urdu (Arabic Script)
html
<html lang="ur" dir="rtl">
Isse:

Text right se left likhega
Bullets right side par honge
Layout mirror ho jayega

RTL Kaise Kaam Karta Hai?

css
/* LTR mein */
margin-left: 20px;   /* Left side se space */

/* RTL mein automatically mirror ho jata hai */
/* Browser logical properties use karta hai */
Modern Approach: Logical properties use karo:

css
/* ❌ Purana (RTL mein masla) */
margin-left: 20px;

/* ✅ Modern */
margin-inline-start: 20px;

6. xmlns Attribute — Kab Use Karna Hai?
html
<html xmlns="http://www.w3.org/1999/xhtml">
Ye XHTML ke liye tha. Aaj HTML5 mein zaroori nahi.

Lekin: Agar aapka page:

-> SVG inline use karta hai → <svg xmlns="..."> mein chahiye
-> XHTML served ho raha hai (application/xhtml+xml) → chahiye
-> Regular HTML5 hai → skip karo
-> Best Practice: HTML5 mein na lagao.

7. Browser Mein Kya Hota Hai?

Step by step:
-> Browser DOCTYPE padhta hai → Standards Mode
-> Implicit <html> create karta hai agar missing
-> lang aur dir attributes read karta hai
-> Text rendering engine set karta hai
-> Accessibility tree mein language set
-> CSS engine ko :lang() selector ke liye enable
-> document.documentElement isko reference karta hai

JavaScript Access:

javascript
console.log(document.documentElement);        // <html> element
console.log(document.documentElement.lang);   // "en"
console.log(document.documentElement.dir);    // "" (default ltr)

8. Edge Cases / Gotchas

Gotcha 1: <html> Missing
html
<!DOCTYPE html>
<head>...</head>
<body>...</body>
Browser auto-add kar dega, lekin aap control kho dete ho. Kuch tools fail ho sakte hain.

Result: <html><head>...</head><body>...</body></html> implicit.

Gotcha 2: Multiple <html>
html
❌ <html><html>...</html></html>
Browser pehla rakhega, doosra ignore.

Gotcha 3: Content <head> Ke Bahar Aur <body> Ke Bahar
html
<html>
  <p>Yeh kahan jayega?</p>  ← ❌ Text directly html ke andar
  <head>...</head>
  <body>...</body>
</html>
Browser body mein daal dega (auto-fix), lekin valid nahi.

Gotcha 4: lang Nahi Lagana
html
<html>  ← ❌ W3C validator warning
Fix: <html lang="en">

Gotcha 5: lang="ur" Lekin Content Roman Urdu
html
<html lang="ur">
<p>Yeh Roman Urdu hai, Arabic script nahi.</p>
Problem: Screen reader Urdu pronunciation use karega, jo Roman ke liye galat hai.

Fix: Roman Urdu ke liye lang="en" (ya lang="ur-Latn") use karo.

9. Tricky Interview Questions
Q1. <html> tag ka kya kaam hai?
A: Poori document ka root element. <head> aur <body> dono iske andar. Language aur direction define karta hai.

Q2. lang attribute kyun zaroori hai?
A: Screen readers, SEO, spell-check, translation, fonts, hyphenation — sab isi par depend karte hain. Accessibility ke liye must.

Q3. lang="en-US" aur lang="en" mein kya farq?
A: en general English, en-US American English specifically. Pronunciation aur spelling differences (color vs colour) ke liye.

Q4. dir="rtl" aur CSS direction: rtl; mein kya farq?

A:
-> dir HTML attribute — semantic, accessibility tools dekhte hain
-> direction CSS property — sirf visual
-> Hamesha dir use karo semantic ke liye.

Q5. Kya <html> tag lazmi hai?
A: Technically nahi — browser auto-add kar deta hai. Lekin hamesha likho — control aur validation ke liye.

Q6. xmlns aaj kyun nahi lagate?
A: HTML5 mein attribute optional hai. Browser automatically samajh leta hai. SVG ke liye zaroori hai <svg> par.

Q7. :lang() CSS selector kaise kaam karta hai?
A:
css
  :lang(en) { font-family: Arial; }
  :lang(ur) { font-family: 'Noto Nastaliq Urdu'; }
  <html lang="ur"> wale page par Urdu font apply hoga.

Q8. Agar parent lang="en" aur child lang="ur" ho, to child par kaunsa apply hoga?
A: Child — nearest ancestor ka lang override karta hai.

Q9. document.documentElement kya return karta hai?
A: <html> element. document.body <body> ko, document.head <head> ko.

Q10. SSR mein <html> par dynamic lang kaise set karoge (jaise Next.js)?
A:
javascript
  // Next.js App Router
  export default function RootLayout({ children }) {
    const locale = "ur"; // dynamic
    return (
      <html lang={locale} dir={locale === "ur" ? "rtl" : "ltr"}>
        <body>{children}</body>
      </html>
    );
  }

10. Common Mistakes
Mistake	                                      Fix
lang nahi lagana	                            Hamesha <html lang="...">
Roman Urdu ke liye lang="ur"	                lang="ur-Latn" ya lang="en"
dir CSS se lena	                              HTML dir attribute use karo
xmlns HTML5 mein	                            Skip karo
Multiple <html>	                              Ek hi
Content directly <html> mein	                <body> mein daalo