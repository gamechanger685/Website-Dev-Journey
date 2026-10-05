<a> Tag — Complete Postmortem

1. Why Does It Exist?

<a> = Anchor tag. Yeh web ki jaan hai. Isi ki wajah se "web" ko "web" kehte hain — ek page se doosre page par links ka jaal.

Without <a>:

1) Sirf alag alag pages hote, connected nahi
2) Search engines crawl nahi kar paate
3) Internet ek library hoti jisme books bikhri hoti, organized nahi

Kyun <a>? Anchor = jahaz ka langar. Ek jagah se doosri jagah ka "connection point".

2. Syntax
html
<a href="https://example.com" target="_blank" rel="noopener noreferrer">Click here</a>

3. All Attributes (Complete List)

Attribute	            Values	                                   Purpose
href	                URL, #id, mailto:, tel:, path	             Destination
target	              _self, _blank, _parent, _top	             Kahan kholna
rel	                  noopener, noreferrer, nofollow, noopener	 Relationship
download	            filename (optional)	                       File download
hreflang	            en, ur, ar	                               Language of linked page
type	                MIME type	                                 File type hint
ping	                URL	                                       Track clicks (analytics)
referrerpolicy      	no-referrer, origin	                       Referrer control
id	                  Custom	                                   Identify
class	                Custom	                                   Style hook
title	                Text	                                     Tooltip
aria-*	              Various	                                   Accessibility
tabindex	            Number	                                   Tab order
draggable	            true, false	                               Drag support

5. Browser Mein Kya Hota Hai (Step by Step)

-> Browser <a> ko link element samajhta hai
-> href value ko URL parser mein daalta hai
-> URL resolved hota hai (relative ko absolute)
-> Tab index mein add hota hai (keyboard navigation)
-> Hover par cursor: pointer (user agent stylesheet)
-> Click par navigation event fire hota hai
-> Default action: current tab navigate
-> target="_blank" ho to new tab open
-> rel="noopener" ho to security maintain (window.opener block)
-> Browser Referer header bhejta hai (default)

6. Security: Why rel="noopener noreferrer"?

Without rel="noopener" — Malicious site aapki tab ka window.opener access kar sakti hai:

    javascript

    // Attacker's code in their page
    if (window.opener) {
      window.opener.location = "https://phishing-site.com";
    }

Yeh Tabnabbing attack hai.
Without rel="noreferrer" — Referrer header jata hai, privacy issue.

Rule: target="_blank" use karo to hamesha rel="noopener noreferrer" lagao.

7. Accessibility Rules

A. Descriptive text:

html
❌ <a href="/article">Click here</a>
✅ <a href="/article">Read the full article about CSS Grid</a>

Screen reader links ki list deta hai. "Click here" 10 baar sun kar user confuse hota hai.

B. Button vs Link:
Navigation (naya page) → <a>
Action (JS trigger) → <button>

html
❌ <a href="#" onclick="deleteItem()">Delete</a>
✅ <button onclick="deleteItem()">Delete</button>

C. Skip links:
html
<a href="#main-content" class="skip-link">Skip to content</a>

Keyboard users ke liye — pehla focus element.

D. Focus indicator:
css
a:focus-visible {
  outline: 3px solid #3498db;
  outline-offset: 2px;
}

8. Edge Cases / Gotchas

1. href="#" vs href="":
href="#" — Top par jata hai
href="" — Current page reload

Best: href="#" ko role="button" ke saath, ya better <button>

2. Nested links — NOT ALLOWED:
html
❌ <a href="/a"><a href="/b">Inner</a></a>

3. <a> ke andar block elements:
HTML5 mein <a> ke andar <div>, <section> allowed hai — lekin accessibility issue ho sakta hai.

4. Void elements nahi hai:
html
❌ <a href="/x" />
✅ <a href="/x"></a>

5. download cross-origin:
html
<!-- Sirf same-origin par kaam karta hai -->
<a href="https://other-site.com/file.pdf" download>❌ Download</a>

9. Tricky Interview Questions
Q1. target="_blank" ke saath rel="noopener" kyun zaroori hai?
A: Tabnabbing attack rokne ke liye. Warna attacker's page window.opener.location change kar sakta hai.

Q2. <a href="#"> aur <a href="javascript:void(0)"> mein kya farq?
A: # scroll top karta hai, javascript:void(0) kuch nahi karta lekin bad practice hai. Better: <button> use karo.

Q3. Kya <a> ke andar <button> aa sakta hai?
A: HTML valid hai lekin bad practice — accessibility issue. Screen reader confuse hota hai.

Q4. href attribute na ho to <a> kaise behave karega?
A: Link ki tarah behave nahi karega. Style dikhega lekin click par navigate nahi hoga. Focusable bhi nahi.

Q5. Kaise pata chalega ke user ne link click kiya (analytics)?
A: onclick handler, ya ping attribute, ya navigator.sendBeacon(), ya server-side referrer.

Q6. <a> tag ko keyboard se focusable banane ke liye kya chahiye?
A: href attribute (automatically focusable), warna tabindex="0".

Q7. Prefetch vs Preload vs Preconnect — kab use karein?
A:

prefetch — Future navigation ke liye
preload — Current page ki critical resource
preconnect — DNS + TCP handshake pehle karo

10. Common Mistakes
Mistake	                                       Fix
Click here link text	                        Descriptive text
target="_blank" bina rel	                    rel="noopener noreferrer"
JS action ke liye <a>	                        <button> use karo
Nested <a>	                                  Alag links
Empty href	                                  Meaningful URL
href="javascript:void(0)"	                    <button> ya proper URL
Block elements bina wajah	                    Semantic structure

11. Performance Considerations

Prefetch — <link rel="prefetch" href="/next-page">
Preload — <link rel="preload" as="document" href="/page">
DNS-prefetch — <link rel="dns-prefetch" href="//cdn.example.com">
Beacon API — Click tracking ke liye non-blocking