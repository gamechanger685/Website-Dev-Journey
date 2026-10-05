<!DOCTYPE html> — Complete Postmortem

1. Why Does It Exist? (Tareekh)
1990s mein HTML standard nahi tha. Netscape(Purana Browser) aur Internet Explorer apni marzi se tags bana rahe the. Jis website ko jo browser support karta, woh chalti thi.

Problem: Web developers ke liye nightmare. Same code Firefox mein kuch, IE mein kuch aur dikhta.

1999 (HTML 4.01): W3C ne DOCTYPE introduce kiya — taake browser ko pata chale kaunsa HTML version use ho raha hai.

Lekin twist: Purani websites (bina DOCTYPE wali) ko bhi support karna tha. Is liye browsers ne 2 modes banaye:

Mode	                            Behavior
Standards Mode	                  Modern CSS rules follow karo
Quirks Mode	                      Purane rules follow karo (IE 5.5 jaisa)

DOCTYPE ka asli kaam: Browser ko batana ke konsa mode use karna hai.

Aaj (2026): <!DOCTYPE html> ka sirf ek hi matlab hai: "Standards Mode use karo". Bas.

2. Syntax Evolution
html
<!-- HTML 4.01 Strict (1999) — LAMBI line -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
  "http://www.w3.org/TR/html4/strict.dtd">

<!-- XHTML 1.0 Strict (2000) — LAMBI line -->
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

<!-- HTML5 (2014) — CHHOTI line -->
<!DOCTYPE html>
Dekho farq: HTML5 ne DOCTYPE ko short aur simple bana diya. Bas 15 characters. Aur kuch nahi chahiye.

3. Anatomy of <!DOCTYPE html>
text
<!DOCTYPE html>
│       │    │
│       │    └── Document type = HTML
│       │
│       └── Declaration keyword
│
└── "Bang!" — yeh tag nahi, declaration hai

Important Points:

-> Case insensitive — <!DOCTYPE html>, <!doctype html>, <!DocType HTML> — sab valid hain. Lekin convention: uppercase DOCTYPE, lowercase html.
-> Yeh tag nahi hai — is liye closing tag nahi hota. Na hi koi attributes.
-> Document ki sab se pehli line honi chahiye. Kuch bhi pehle nahi — na space, na comment, na BOM.
-> HTML element ka parent nahi — yeh document ke bahar rehta hai.

4. Browser Mein Kya Hota Hai? (Internals)

Step by step:
-> Browser HTML file download karta hai
-> Pre-parser DOCTYPE ko sab se pehle padhta hai
-> Agar DOCTYPE recognized hai → Standards Mode
-> Agar DOCTYPE nahi hai ya galat hai → Quirks Mode
-> Mode document lifetime tak fix rehta hai (change nahi hota)
-> CSS engine us mode ke hisaab se rules apply karta hai
-> JavaScript mein check kar sakte ho:

javascript
console.log(document.compatMode);
// "CSS1Compat" = Standards Mode
// "BackCompat"  = Quirks Mode

5. Standards vs Quirks Mode — Real Differences
Yeh bohot important hai. Yahi wajah hai ke DOCTYPE zaroori hai.

Example 1: Box Model
html
<!-- Bina DOCTYPE (Quirks Mode) -->
<div style="width: 200px; padding: 20px; border: 5px solid;">
  Width = 200px (padding aur border ANDAR aate hain — IE 5.5 style)
</div>

<!-- DOCTYPE ke saath (Standards Mode) -->
<div style="width: 200px; padding: 20px; border: 5px solid;">
  Width = 250px (200 + 40 padding + 10 border — total)
</div>
Wait — aur confusing: Modern Standards Mode mein bhi box-sizing: content-box default hai. Lekin Quirks Mode mein box-sizing bilkul different behave karta hai.

Example 2: Centering
css
body { text-align: center; }
Quirks Mode: Saare text elements center ho jayenge (weird)

Standards Mode: Sirf text center hoga

Example 3: Percent Height
css
html, body { height: 100%; }
Quirks Mode: height: 100% kaam nahi karta theek se

Standards Mode: Properly kaam karta hai

Example 4: Image Alt
Quirks Mode: <img> bina alt ke bhi fine

Standards Mode: alt zaroori

Example 5: Font Size Inheritance
css
table { font-size: 14px; }
Quirks Mode: Table mein text 14px, lekin uske andar ke elements aglay rules follow karte

Standards Mode: Proper inheritance

6. Quirks Mode Ke 5 Alag Modes (Bohot Advanced)
Modern browsers actually 5 modes use karte hain:

Mode	                                          Kab Trigger Hota
No Quirks (Standards)	                          <!DOCTYPE html>
Limited Quirks	                                HTML 4.01 Transitional
Quirks	                                        DOCTYPE missing ya unknown
Almost Standards	                              XHTML 1.0 Transitional
Full Standards	                                HTML5

Yeh aaj kal matter nahi karta kyunki sab <!DOCTYPE html> use karte hain. Lekin interview mein poocha ja sakta hai.

7. Historical DOCTYPE Declaration Structure
Purane DOCTYPE mein 4 parts hote the:

text
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
  "http://www.w3.org/TR/html4/strict.dtd">
        │       │              │         │
        │       │              │         └─ System Identifier (URL)
        │       │              └─ Public Identifier
        │       └─ "PUBLIC" keyword
        └─ Root element
Aaj HTML5 mein sirf:

text
<!DOCTYPE html>
Bas. Koi PUBLIC, koi URL, koi version — kuch nahi.

8. Edge Cases / Gotchas
Gotcha 1: DOCTYPE Ke Pehle Kuch Bhi
html
<!-- ❌ GALAT — comment pehle -->
<!-- My website -->
<!DOCTYPE html>
<html>...
Result: Quirks Mode. Browser comment ko bhi ignore nahi karta — woh DOCTYPE ke baad hona chahiye.

Gotcha 2: DOCTYPE Ke Baad Space
html
<!-- ❌ GALAT -->
<!DOCTYPE html >
<html>...
Result: Standards Mode (aaj kal browsers tolerant hain, lekin best practice: koi extra space nahi).

Gotcha 3: Do DOCTYPE
html
<!-- ❌ GALAT -->
<!DOCTYPE html>
<!DOCTYPE html>
<html>...
Result: Pehla ignore, doosra use hoga. Lekin yeh invalid HTML hai.

Gotcha 4: Server-Side Rendering (SSR)
    php
    <!-- ❌ GALAT — PHP ke baad DOCTYPE -->
    <?php
    session_start();
    ?>
    <!DOCTYPE html>
    Problem: PHP ke <?php ?> tags ke baad whitespace ho sakta hai, jo DOCTYPE ke pehle aata hai → Quirks Mode.

Fix:
  php
    <?php session_start(); ?><!DOCTYPE html>
    Gotcha 5: BOM (Byte Order Mark)

UTF-8 files mein 3 bytes (EF BB BF) start mein ho sakte hain. Browser inhe content samajhta hai → Quirks Mode.
Fix: Editor mein "Save without BOM" option use karo.

Gotcha 6: XML Declaration Ke Saath
html
<!-- ❌ GALAT -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html>

Yeh XHTML ke liye tha. HTML5 mein XML declaration nahi chahiye.

9. Tricky Interview Questions
Q1. DOCTYPE ka asli kaam kya hai?
A: Browser ko batana ke Standards Mode use kare ya Quirks Mode. Aaj kal sirf Standards Mode enforce karna.

Q2. <!DOCTYPE html> aur <!doctype HTML> mein kya farq hai?
A: Kuch nahi. Case-insensitive hai. Lekin convention: UPPERCASE DOCTYPE.

Q3. DOCTYPE ke bina page kaise behave karega?
A: Browser Quirks Mode mein chala jayega. CSS different behave karegi. 99% websites tut jayengi.

Q4. Kya DOCTYPE tag ka closing hota hai?
A: Nahi. Yeh tag nahi, declaration hai. Like <?php ?> ya <!-- -->.

Q5. Agar DOCTYPE ke pehle HTML comment aaye to?
A: Browser us comment ko content samajhta hai aur DOCTYPE ke pehle hai → Quirks Mode. Comments hamesha DOCTYPE ke baad honi chahiye.

Q6. JavaScript mein kaise check karoge ke page Standards Mode mein hai?

A:
  javascript
    if (document.compatMode === "CSS1Compat") {
      console.log("Standards Mode");
    } else {
      console.log("Quirks Mode");
    }

Q7. Modern browsers mein DOCTYPE ka importance kam ho gaya hai kyunki...?
A: Aaj kal sab developers <!DOCTYPE html> use karte hain. Purani quirks wali sites ab khatam ho gayi hain. Lekin DOCTYPES without standards still trigger Quirks Mode — is liye zaroori hai likhna.

Q8. Kya HTML5 mein DOCTYPE ke values badle hain?
A: HTML5 mein DOCTYPE sirf 15 characters hai. Aur koi version number ya DTD nahi. Yeh intentional simplification hai.

Q9. Server-side (PHP, Node) mein DOCTYPE kaise safe rakhoge?
A: Saari server-side processing khatam karo, php closing tag na lagao, aur DOCTYPE ko file ki pehli bytes banao.

Q10. Quirks Mode mein CSS ka width kaise behave karta hai?
A: Purane IE (5.5) ki tarah — padding aur border width ke andar aate hain. Modern Standards Mode mein default box-sizing: content-box hai jisme padding aur border bahar add hoti hai.

10. Common Mistakes
Mistake	                                        Fix
DOCTYPE bhool jana	                            Hamesha first line
DOCTYPE ke pehle comment	                      Comment ko <html> ke baad rakho
<!DOCTYPE html > (extra space)	                Exact <!DOCTYPE html>
Server-side output                              DOCTYPE se pehle	Buffering ya closing tags avoid karo
BOM bytes	                                      Save without BOM
XML declaration                                 HTML5 mein	Nahi zaroori
Multiple DOCTYPE	                              Ek hi rakho