<meta> Tags — Complete Postmortem

1. Why Does It Exist?
<meta> tag metadata store karta hai. Yeh information:
  User ko screen par nazar nahi aati
  Lekin browser, search engines, social media, aur devices ko batati hai ke page kya hai

Analogy:
  <meta> = File ka cover page (title, author, ISBN) — padhne wale ko content nahi dikhta, lekin file ki poori information milti hai
  <body> = File ka actual content

Without <meta>:
  Charset nahi → Urdu/Chinese characters tute hue (Ø£Ø¨Ùˆ Ø¨Ú©Ø±)
  Viewport nahi → Mobile par desktop layout, user zoom kare
  Description nahi → Google search mein random text
  OG tags nahi → WhatsApp/Facebook share par preview nahi
  Theme-color nahi → Mobile browser default color
  Robots nahi → Google crawler confuse

2. Syntax
html
  <meta charset="UTF-8">
  <meta name="description" content="Page description">
  <meta property="og:title" content="Page Title">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">

Rules:
  Yeh self-closing tag hai — closing tag NAHI hota
  <head> ke andar hona chahiye
  Charset sab se pehle (1024 bytes ke andar)
  Multiple <meta> tags ho sakte hain
  Attribute order matter nahi karta

3. <meta> Ke 4 Attribute Types (Complete Anatomy)

Type 1: charset (Standalone)
html
  <meta charset="UTF-8">
Sirf ek attribute. Sirf UTF-8 value. Charset declare karne ka naya tareeqa.

Type 2: name + content
html
  <meta name="description" content="...">
Sab se common. Name = metadata ka type. Content = value.

Type 3: property + content (Open Graph / RDFa)
html
  <meta property="og:title" content="...">
Social media ke liye. Facebook ka protocol. RDFa syntax.

Type 4: http-equiv + content (HTTP Simulate)
html
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
HTTP header simulate karta hai. Server headers better hain.

4. Charset — Character Encoding

4.1 Why Does It Exist?
Computer bytes store karta hai (0 aur 1). Lekin hum characters likhte hain (A, B, ی, 中).
Charset batata hai: "Yeh bytes ko kaise characters mein convert karna hai."

Agar charset galat:
  Bytes: 0xC3 0xA9
  Wrong charset (Latin-1): "Ã©"
  Right charset (UTF-8): "é"
  Urdu mein: "Ù…" (galat) vs "م" (sahi)

4.2 Syntax
html
  <meta charset="UTF-8">

4.3 Charset Types
Charset	            Support	                        Use Case
UTF-8	              Sab languages (99.9%)	          Hamesha yehi
ISO-8859-1	Latin	                          Purani English sites
UTF-16	Rare	                            Windows internal
ASCII	Sirf English	                    Purana
windows-1252	Western European	          Outlook emails

4.4 Position Rule
Head ke andar pehle 1024 bytes mein hona chahiye.
Best Practice: First element.

Agar baad mein aaye:
html
  <!-- ❌ GALAT -->
  <title>Page</title>
  <meta charset="UTF-8">
Browser ne already 1024 bytes padh liye → galat guess → tute characters.

4.5 Old Syntax (HTML5 se pehle)
html
  <!-- ❌ Purana -->
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">

  <!-- ✅ Modern -->
  <meta charset="UTF-8">

4.6 Kyun UTF-8 Hamesha?
  Har language support karta hai (Urdu, Arabic, Chinese, Japanese, Emoji)
  Backward compatible ASCII se
  Efficient hai (1-4 bytes per character)
  Modern standard hai (W3C recommended)

5. Viewport — Mobile Responsive

5.1 Why Does It Exist?
1990s mein websites desktop ke liye thi. Mobile browsers ne trick use ki: page ko 980px wide "virtual viewport" mein render karo, phir zoom out karo. Bura UX.

Viewport meta mobile ko batata hai: "Actual device width use karo."

5.2 Syntax
html
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

5.3 All Values
Value	                  Matlab	                                  Default
width=device-width	      Screen ki actual width	                  980px
width=600	              Custom width	                          980px
initial-scale=1.0	      100% zoom	                              Auto
minimum-scale	          Min zoom level	                        0.25
maximum-scale	          Max zoom level	                        5.0
user-scalable=yes/no	  Pinch zoom allow	                      yes
viewport-fit=cover	      iPhone notch handle	                    auto
viewport-fit=contain	  Notch ke andar raho	                    auto

5.4 Best Practice
html
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

5.5 ⚠️ user-scalable=no Mat Lagao
html
  <!-- ❌ GALAT -->
  <meta name="viewport" content="user-scalable=no">
Masla: Low vision users zoom nahi kar sakte. WCAG 1.4.4 violation. Accessibility fail.

Fix: Zoom allow karo. Default behavior hi best hai.

5.6 viewport-fit=cover (iPhone Notch)
html
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
Isse content iPhone notch/safe area mein extend karta hai.
Aur CSS safe-area-inset ke saath use hota hai:
css
  body {
    padding: env(safe-area-inset-top) env(safe-area-inset-right)
             env(safe-area-inset-bottom) env(safe-area-inset-left);
  }

6. SEO Meta Tags

6.1 description — Google Preview
html
  <meta name="description" content="Abu Bakar, Software Engineering student, Full Stack Web Engineer banna chahta hoon.">
Kahan dikhta hai: Google search results mein blue title ke NEECHE.
Best Practices:
  150-160 characters
  Unique har page par
  Action verb include karo ("Learn", "Discover", "Build")
  Keywords natural tarah se
  Target audience mention karo

Note: Direct ranking factor nahi hai, lekin click-through rate (CTR) improve karta hai.

Agar description nahi likha: Google khud page se text uthata hai (random dikhta hai).

6.2 keywords — Deprecated
html
  <meta name="keywords" content="HTML, CSS, JavaScript">
Status: ❌ Google 2009 se ignore kar raha. Bing thora consider karta hai. SEO fayda ZERO.
Kyun khatam: Webmasters spam karte the (100+ keywords per page).
Modern: Keywords naturally content mein use karo.

6.3 robots — Crawler Control
html
  <meta name="robots" content="index, follow">
Values:
Value	              Matlab
index	              Search mein dikhao
noindex	            Search mein MAT dikhao
follow	            Links follow karo
nofollow	          Links MAT follow karo
noarchive	          Cache MAT karo
nosnippet	          Snippet MAT dikhao
max-snippet:-1	    Unlimited snippet
max-image-preview:large	Badi image preview
noimageindex	      Images index MAT karo
none	              = noindex + nofollow
all	                = index + follow (default)

Crawler-Specific:
html
  <meta name="googlebot" content="index, follow">
  <meta name="bingbot" content="index, follow">
  <meta name="GPTBot" content="noindex">        ← ChatGPT crawler
  <meta name="ClaudeBot" content="noindex">     ← Anthropic crawler
  <meta name="PerplexityBot" content="noindex"> ← Perplexity

6.4 author, language, copyright
html
  <meta name="author" content="Abu Bakar">
  <meta name="language" content="English">
  <meta name="copyright" content="© 2026 Abu Bakar">
  <meta name="rating" content="general">
  <meta name="revisit-after" content="7 days">
  <meta name="distribution" content="global">

7. Open Graph — Social Sharing Protocol

7.1 Why Does It Exist?
2010 mein Facebook ne banaya. Isse pehle: WhatsApp/Facebook par link share karo → sirf URL dikhta. Bura UX.

Ab: Rich preview card (image + title + description).

7.2 Required Tags (4 Zaroori)
html
  <meta property="og:title" content="Page Title">
  <meta property="og:type" content="website">
  <meta property="og:image" content="https://example.com/image.jpg">
  <meta property="og:url" content="https://example.com">

7.3 Recommended Tags
html
  <meta property="og:description" content="Description">
  <meta property="og:site_name" content="Abu Bakar">
  <meta property="og:locale" content="en_US">

7.4 Complete List
Property	              Purpose	                              Example
og:type	                Content type	                        website, article, video.movie
og:title	              Share title	                          60-90 chars
og:description	        Share description	                    100-200 chars
og:image	              Preview image	                        1200×630
og:image:width	        Image width	                          1200
og:image:height	        Image height	                        630
og:image:alt	          Image alt text	                      "Preview image"
og:url	                Canonical URL	                        https://...
og:site_name	          Brand name	                          "Abu Bakar"
og:locale	              Language	                            en_US, ur_PK
og:locale:alternate	    Alt languages	                        ur_PK

7.5 Article-Specific
html
  <meta property="article:author" content="https://facebook.com/abubakar">
  <meta property="article:published_time" content="2026-10-05T10:00:00Z">
  <meta property="article:modified_time" content="2026-10-05T12:00:00Z">
  <meta property="article:section" content="Technology">
  <meta property="article:tag" content="HTML">

7.6 Video-Specific
html
  <meta property="og:video" content="https://example.com/video.mp4">
  <meta property="og:video:width" content="1280">
  <meta property="og:video:height" content="720">
  <meta property="og:video:type" content="video/mp4">

7.7 Image Size (MUST)
Facebook/LinkedIn: 1200×630 (1.91:1 ratio)
Twitter: 1200×600
WhatsApp: 300×200 minimum
Chhoti image: Blurry dikhti hai, buri impression

8. Twitter Cards

8.1 Why Separate?
Twitter (X) ne apna protocol banaya. OG ko bhi support karta hai lekin Twitter-specific tags zyada control dete hain.

8.2 Card Types (4)
Type	                  Image	                        Use Case
summary	                1:1 square	                    Small thumbnail
summary_large_image	    2:1 wide	                      Recommended
app	                    App icon	                    Mobile apps
player	                Video player	                Video content

8.3 Required Tags
html
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Page Title">
  <meta name="twitter:description" content="Description">
  <meta name="twitter:image" content="https://example.com/image.jpg">

8.4 Optional Tags
html
  <meta name="twitter:site" content="@abubakar">       <!-- Website handle -->
  <meta name="twitter:creator" content="@abubakar">    <!-- Author handle -->
  <meta name="twitter:image:alt" content="Alt text">
  <meta name="twitter:label1" content="Reading time">
  <meta name="twitter:data1" content="5 minutes">
  <meta name="twitter:label2" content="Written by">
  <meta name="twitter:data2" content="Abu Bakar">

8.5 Fallback
Agar Twitter tags nahi hain: Twitter OG tags use karta hai.
Agar dono nahi: Sirf URL + favicon dikhta hai.

9. Theme Color & PWA

9.1 theme-color — Mobile Browser UI
html
  <meta name="theme-color" content="#3498db">
Kya karta hai: Mobile Chrome/Android browser mein address bar ka color.
Dark mode:
html
  <meta name="theme-color" content="#ffffff" media="(prefers-color-scheme: light)">
  <meta name="theme-color" content="#1a1a1a" media="(prefers-color-scheme: dark)">

9.2 PWA Meta Tags
html
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <meta name="apple-mobile-web-app-title" content="Abu Bakar">
  <meta name="mobile-web-app-capable" content="yes">
  <meta name="application-name" content="Meta Guide">
  <meta name="format-detection" content="telephone=no">
  <link rel="manifest" href="/manifest.json">

10. Security Meta Tags (http-equiv)

10.1 Why Use Meta?
Server headers better hain, lekin agar server control nahi (shared hosting), to meta tags fallback.
Note: CSP aur HSTS ke liye server headers MUST. Meta tags limited hain.

10.2 All Security Tags
html
  <meta http-equiv="X-Content-Type-Options" content="nosniff">
  <meta http-equiv="X-Frame-Options" content="DENY">
  <meta http-equiv="X-XSS-Protection" content="1; mode=block">
  <meta http-equiv="Content-Security-Policy" content="default-src 'self'">
  <meta http-equiv="Referrer-Policy" content="strict-origin-when-cross-origin">
  <meta http-equiv="Strict-Transport-Security" content="max-age=31536000">

10.3 Kyun Server Headers Better?
Meta tags:
  JavaScript se modify ho sakte hain (attack possible)
  Sirf HTML par apply
  Developer galti se bhool sakta hai
Server headers:
  Browser level par enforce
  Sab responses par apply
  Modify nahi ho sakte

11. http-equiv — Purana Tareeqa

11.1 Refresh (AVOID)
html
  <!-- ❌ Kabhi mat use karo -->
  <meta http-equiv="refresh" content="5;url=https://example.com">
Masla:
  UX bura (user control nahi)
  Accessibility fail (screen reader surprise)
  SEO issue (crawlers confuse)
  Back button bura behave
Fix: Server-side redirect (301/302) ya JavaScript.

11.2 X-UA-Compatible (IE-Specific, Deprecated)
html
  <!-- ❌ Purana -->
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
IE 11 tak kaam karta tha. IE 2022 mein retired. Aaj useless.

11.3 Content-Type (Purana)
html
  <!-- ❌ Purana -->
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  <!-- ✅ Modern -->
  <meta charset="UTF-8">

12. <meta> Ke Saath <link> Tags (Related)

12.1 Favicon
html
  <link rel="icon" href="/favicon.ico" sizes="any">
  <link rel="icon" href="/icon.svg" type="image/svg+xml">
  <link rel="apple-touch-icon" href="/apple-icon.png">
  <link rel="manifest" href="/manifest.json">

12.2 Canonical
html
  <link rel="canonical" href="https://example.com/page">
Kya karta hai: Duplicate content issue fix. Google ko batata hai ke original URL kaunsa hai.

12.3 Alternate (hreflang)
html
  <link rel="alternate" hreflang="en" href="https://example.com/en">
  <link rel="alternate" hreflang="ur" href="https://example.com/ur">
  <link rel="alternate" hreflang="x-default" href="https://example.com">

12.4 Performance Hints
html
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="dns-prefetch" href="//cdn.example.com">
  <link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin>
  <link rel="prefetch" href="/next-page.html">

12.5 RSS Feed
html
  <link rel="alternate" type="application/rss+xml" href="/feed.xml">

13. Order (Matters!)

Recommended Order:
html
  <head>
    <!-- 1. CHARSET (MUST BE FIRST) -->
    <meta charset="UTF-8">
    
    <!-- 2. VIEWPORT -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- 3. TITLE -->
    <title>Page Title</title>
    
    <!-- 4. DESCRIPTION -->
    <meta name="description" content="...">
    
    <!-- 5. CANONICAL -->
    <link rel="canonical" href="...">
    
    <!-- 6. OPEN GRAPH -->
    <meta property="og:title" content="...">
    ...
    
    <!-- 7. TWITTER -->
    <meta name="twitter:card" content="...">
    ...
    
    <!-- 8. FAVICON -->
    <link rel="icon" href="...">
    
    <!-- 9. PRECONNECT -->
    <link rel="preconnect" href="...">
    
    <!-- 10. CSS -->
    <link rel="stylesheet" href="...">
    
    <!-- 11. SCRIPTS -->
    <script src="app.js" defer></script>
  </head>

Kyun yeh order?
  charset first → Warna encoding galat
  viewport jaldi → Mobile render
  CSS pehle → Visual render
  JS last → Non-blocking

14. Browser Mein Kya Hota Hai? (Internals)

HTML Parsing Order:
  -> Browser file download karta hai
  -> Byte stream aata hai
  -> Charset detect (meta se) ← Pehle 1024 bytes
  -> Tokenize — tags identify
  -> Tree construction — DOM banata hai
  -> <head> mein:
    -> <title> — window title set
    -> <meta> — metadata store
    -> <link> — resource fetch (CSS blocking)
    -> <script> — execute (defer/async handle)
  -> <body> parse
  -> DOMContentLoaded event
  -> load event (saare resources ready)

Critical Rendering Path:
  HTML → DOM  ↓
              → Render Tree → Layout → Paint
  CSS  → CSSOM ↑

CSS blocking hai! Is liye <link> jaldi lagao.

15. Edge Cases / Gotchas

Gotcha 1: Charset Baad Mein
html
  <head>
    <title>...</title>       <!-- ❌ Pehle title -->
    <meta charset="UTF-8">   <!-- ❌ Baad mein charset -->
  </head>
Masla: Browser ne already 1024 bytes guess kar liye → encoding galat → tute characters.
Fix: Charset first.

Gotcha 2: user-scalable=no
html
  <meta name="viewport" content="user-scalable=no">
Masla: Low vision users zoom nahi kar sakte. WCAG violation.
Fix: Zoom allow karo.

Gotcha 3: og:image Chhota
Masla: Chhoti image blurry dikhti hai social media par.
Fix: 1200×630 minimum.

Gotcha 4: Multiple Charset
html
  <meta charset="UTF-8">
  <meta charset="ISO-8859-1">   <!-- ❌ -->
Masla: Browser pehla use karega, doosra ignore. Confusion.
Fix: Ek hi charset.

Gotcha 5: Sensitive Info Meta Mein
html
  <meta name="password" content="secret123">   <!-- ❌ NEVER -->
Masla: DevTools ya View Source se PUBLIC. Kabhi mat karo.
Fix: Sensitive info server-side rakhो.

Gotcha 6: http-equiv="refresh"
html
  <meta http-equiv="refresh" content="5">
Masla: UX bura, accessibility fail, screen reader surprise, back button bura.
Fix: Server redirect (301/302) ya JavaScript.

Gotcha 7: Meta Tags Sirf Security Ke Liye
Masla: Security ke liye meta tags KAAFI NAHI. JavaScript se modify ho sakte hain.
Fix: Server headers (Nginx, Express) use karo.

Gotcha 8: Twitter Card Without Image
html
  <meta name="twitter:card" content="summary_large_image">
  <!-- ❌ twitter:image missing -->
Masla: Card render nahi hoga properly.
Fix: Hamesha twitter:image include karo.

Gotcha 9: og:title 90+ Characters
Masla: Facebook truncate kar deta hai.
Fix: 60-90 characters rakhो.

Gotcha 10: Dynamic Meta in SPA
Masla: Client-side rendering mein meta tags update nahi hote crawlers ko.
Fix: SSR (Next.js) ya prerender use karo.

16. Tricky Interview Questions

Q1. meta tag kya hai?
A: Metadata element. Self-closing. Head ke andar. Browser/SEO/social media padhte hain.

Q2. charset pehla kyun?
A: 1024 bytes ke andar browser ko encoding chahiye. Warna tute characters.

Q3. Open Graph kya hai?
A: Facebook ka 2010 ka protocol. Social media share previews ke liye.

Q4. Twitter Card aur OG mein farq?
A: OG Facebook/LinkedIn, Twitter Card Twitter. Twitter-specific tags zyada granular. Twitter OG ko fallback samajhta hai.

Q5. name vs property vs http-equiv?
A:
  name = Standard meta
  property = OG/RDFa
  http-equiv = HTTP header simulate

Q6. meta refresh kyun avoid?
A: UX bura, accessibility fail, SEO issue, back button bura. Server redirect use karo.

Q7. og:image size?
A: 1200×630 (Facebook/LinkedIn). Twitter: 1200×600.

Q8. keywords meta kaam karta hai?
A: Nahi, Google 2009 se ignore kar raha. Bing thora consider karta hai.

Q9. theme-color kya karta hai?
A: Mobile browser address bar ka color set karta hai.

Q10. Security meta tags kaafi hain?
A: Nahi. Server headers (Nginx, Express) zyada reliable. Meta JS se modify ho sakte hain.

Q11. Twitter Card ke 4 types?
A: summary, summary_large_image, app, player.

Q12. og:locale aur og:locale:alternate mein farq?
A: og:locale = current locale. og:locale:alternate = alternative locales.

Q13. article:published_time format?
A: ISO 8601: "2026-10-05T10:00:00Z"

Q14. Meta tags caching?
A: Meta tags static hote hain — server response mein. CDN cache kar sakta hai.

Q15. Viewport ka viewport-fit=cover kya karta hai?
A: iPhone notch ke saath content ko fit karta hai.

Q16. Multiple og:image possible?
A: Haan, lekin pehli image primary hoti hai. Multiple use karo for different aspect ratios.

Q17. Charset aur lang attribute mein farq?
A: charset = encoding (how bytes = characters). lang = language (English, Urdu).

Q18. Meta tags JS se change ho sakte hain?
A: Haan, DOM manipulation se. Lekin SEO ke liye server-render zaroori.

Q19. Kaunsa meta tag SEO mein sab se important?
A: Title (jo meta nahi hai lekin related). Phir description. Keywords ignored.

Q20. Content-Security-Policy kaise set karo?
A: Server header behtar: Content-Security-Policy: default-src 'self'. Meta http-equiv bhi kaam karta hai lekin limited.

Q21. og:type ke values?
A: website, article, video.movie, video.episode, music.song, product, profile, book.

Q22. Twitter card kaise test karo?
A: cards-dev.twitter.com/validator par URL daalo.

Q23. Facebook OG kaise debug karo?
A: developers.facebook.com/tools/debug par URL daalo.

Q24. Meta tags SSR mein kaise dynamic karo (Next.js)?
A: generateMetadata function use karo:
javascript
  export async function generateMetadata({ params }) {
    const post = await getPost(params.slug);
    return {
      title: post.title,
      description: post.excerpt,
      openGraph: {
        title: post.title,
        images: [post.image],
      },
    };
  }

Q25. Meta tags aur structured data (JSON-LD) mein farq?
A: Meta tags = browsers/crawlers ke liye. JSON-LD = Google rich results ke liye (semantic).

17. Common Mistakes
Mistake	                              Fix
Charset baad mein	                    Pehla tag
user-scalable=no	                    Zoom allow
http-equiv="refresh"	                Server redirect
Keywords par depend	                  Ignore by Google
og:image chhota	                      1200×630
Sensitive info meta mein	            DevTools visible
Security sirf meta par	                Server headers
Multiple charset	                    Ek hi
og:image:width missing	              Zaroor lagao
Title bhoolna	                        Hamesha unique
twitter:image missing	                Hamesha include karo
Meta tags static SPA mein	            SSR use karo

18. Real-World Considerations

18.1 Server-Side Rendering (Next.js)
javascript
  // app/blog/[slug]/page.js
  export async function generateMetadata({ params }) {
    const post = await getPost(params.slug);
    return {
      title: `${post.title} | Abu Bakar`,
      description: post.excerpt,
      openGraph: {
        title: post.title,
        description: post.excerpt,
        images: [{ url: post.image, width: 1200, height: 630 }],
        type: "article",
      },
      twitter: {
        card: "summary_large_image",
        title: post.title,
        images: [post.image],
      },
    };
  }

18.2 Static Site Generation
Astro, Eleventy: Meta tags build time par set.
React Helmet: SPA mein dynamic meta tags.

18.3 SEO Testing Workflow
  1. Build page
  2. curl -I https://example.com → headers check
  3. curl https://example.com | grep meta → meta tags check
  4. Facebook Debugger → OG check
  5. Twitter Card Validator → Twitter check
  6. Google Rich Results → structured data
  7. Lighthouse → performance + SEO score

19. Modern Meta (2026)

19.1 AI Crawler Control
html
  <meta name="GPTBot" content="noindex">
  <meta name="ChatGPT-User" content="noindex">
  <meta name="ClaudeBot" content="noindex">
  <meta name="PerplexityBot" content="noindex">
  <meta name="Google-Extended" content="noindex">

19.2 AI Training Opt-Out
html
  <meta name="robots" content="noai, noimageai">

19.3 Structured Data (JSON-LD — Meta Ke Saath)
html
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Person",
    "name": "Abu Bakar",
    "jobTitle": "Full Stack Web Engineer",
    "url": "https://abubakar.dev",
    "sameAs": [
      "https://github.com/gamechanger685",
      "https://twitter.com/abubakar"
    ]
  }
  </script>

19.4 Speculation Rules API (NEW 2024)
html
  <script type="speculationrules">
  {
    "prerender": [{
      "source": "list",
      "urls": ["/about", "/projects"]
    }]
  }
  </script>

20. Yaad Rakhne Ka Tareeqa

4 Groups:
  1. SEO — title, description, robots, author
  2. Social — og:, twitter:
  3. Mobile — viewport, theme-color, PWA
  4. Security — http-equiv

Order Rule:
  "Charset pehla, phir viewport, phir title, phir baaki"

Image Sizes:
  OG: 1200×630
  Twitter: 1200×600
  Favicon: 32×32

Validation Tools:
  Facebook Debugger: developers.facebook.com/tools/debug
  Twitter Validator: cards-dev.twitter.com/validator
  LinkedIn Inspector: linkedin.com/post-inspector
  Google Rich Results: search.google.com/test/rich-results
  W3C Validator: validator.w3.org

Charan Rule (5 S's):
  1. SEO — Search engines
  2. Social — Sharing platforms
  3. Screen — Mobile devices
  4. Security — Browsers
  5. Speed — Performance hints