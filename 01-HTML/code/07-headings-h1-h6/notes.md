<h1>-<h6> Headings — Complete Postmortem

1. Why Do They Exist?
Heading tags HTML document ka outline banate hain. Yeh batate hain ke content ka structure kya hai — kaunsa part main hai, kaunsa section, kaunsa subsection.

Analogy:
  <h1> = Book ka title (cover par)
  <h2> = Chapter title
  <h3> = Section
  <h4> = Subsection
  <h5> = Sub-subsection
  <h6> = Deepest detail

Without headings:
  Document flat text ho jata
  Screen reader users navigate nahi kar sakte
  Google ko structure samajh nahi aata
  Content scannable nahi hota

History:
  1991 (HTML): H1-H6 introduce hue
  1999 (HTML 4.01): Align attribute common
  2014 (HTML5): Align obsolete, semantic promote
  2015+: SEO importance grow

2. Syntax
html
  <h1>Page Title</h1>
  <h2>Section Heading</h2>
  <h3>Subsection Heading</h3>
  ...
  <h6>Deepest Level</h6>

Rules:
  Closing tag zaroori
  Attributes optional (id, class)
  Inline elements allowed (strong, em, a)
  Block elements NOT allowed (p, div, h1)

3. Heading Levels — Kya Use Karna

Level	              Default Size	            Use Case
h1	                  2em (32px)	              Page title (1 per page)
h2	                  1.5em (24px)	            Major sections
h3	                  1.17em (18.72px)	        Subsections
h4	                  1em (16px)	              Sub-subsections
h5	                  0.83em (13.28px)	        Deep levels
h6	                  0.67em (10.72px)	        Deepest level

Best Practice: Usually 3-4 levels kaafi hain (h1-h3). H4-H6 rare.

4. Default Browser Styles

css
  h1 { font-size: 2em;    margin: 0.67em 0; font-weight: bold; }
  h2 { font-size: 1.5em;  margin: 0.83em 0; font-weight: bold; }
  h3 { font-size: 1.17em; margin: 1em 0;    font-weight: bold; }
  h4 { font-size: 1em;    margin: 1.33em 0; font-weight: bold; }
  h5 { font-size: 0.83em; margin: 1.67em 0; font-weight: bold; }
  h6 { font-size: 0.67em; margin: 2.33em 0; font-weight: bold; }

Note: Yeh sab CSS se override ho sakte hain. Aaj kal designers apne sizes define karte hain.

5. Heading Hierarchy (Correct Pattern)

Correct:
html
  <h1>Page Title</h1>
    <h2>Section 1</h2>
      <h3>Subsection 1.1</h3>
      <h3>Subsection 1.2</h3>
        <h4>Sub-subsection 1.2.1</h4>
    <h2>Section 2</h2>
      <h3>Subsection 2.1</h3>

Rules:
  Ek H1 per page
  Logical order (h1 → h2 → h3)
  Level skip mat karo
  Har section ka heading hona chahiye

Incorrect:
html
  <h1>Title</h1>
  <h4>Section</h4>  ❌ (h2, h3 skip)
  
  <h1>Title 1</h1>
  <h1>Title 2</h1>  ❌ (multiple h1)
  
  <h3>Section</h3>  ❌ (h1, h2 missing)

6. SEO Impact

6.1 Google Ka Approach
  H1 = Page ka main topic
  H2-H6 = Structure samajhne ke liye
  Headings mein keywords > paragraphs mein
  Heading hierarchy = content quality signal
  Poor hierarchy = SEO penalty (mild)

6.2 SEO Rules
Rule 1: Ek H1 per page
  ❌ Multiple H1
  ✅ Ek H1 with primary keyword

Rule 2: Natural hierarchy
  ❌ H1 → H4 (skip)
  ✅ H1 → H2 → H3

Rule 3: Descriptive text
  ❌ "Introduction"
  ✅ "Introduction to HTML Headings"

Rule 4: Keywords naturally
  ❌ "HTML HTML Headings HTML"
  ✅ "Understanding HTML Heading Hierarchy"

Rule 5: Front-load keywords
  ❌ "A Complete Guide to Heading Tags"
  ✅ "Heading Tags: A Complete Guide"

Rule 6: Unique H1 per page
  Homepage: "Abu Bakar — Full Stack Engineer"
  About: "About Abu Bakar"
  Blog post: "HTML Headings Guide"

6.3 Real Google Ranking Factors
  H1 keyword presence: Important
  H1 length: <70 characters
  H2-H3 count: Positive signal
  Keyword density in headings: Natural
  Heading hierarchy: Quality signal

7. Accessibility Impact

7.1 Screen Readers
Users headings se navigate karte hain:
  NVDA: H = next heading, Shift+H = previous
  JAWS: Insert + F6 = heading list
  VoiceOver: Rotor (VO + U) = heading navigation
  
10 headings = 10 navigation points
Bad hierarchy = confusing navigation

7.2 WCAG Guidelines
  WCAG 1.3.1 (Info and Relationships): Structure semantic ho
  WCAG 2.4.1 (Bypass Blocks): Skip links + headings
  WCAG 2.4.6 (Headings and Labels): Descriptive
  WCAG 2.4.10 (Section Headings): Sections headings se organize

7.3 Best Practices
  - Ek H1 per page (page ka naam)
  - Logical hierarchy (level skip nahi)
  - Descriptive text (context ke saath)
  - Empty headings mat use karo
  - Screen reader test karo
  - Skip link ke saath combine karo

8. Attributes

8.1 Modern Attributes
Attribute	            Purpose	                    Example
id	                  Anchor linking	            <h2 id="section-1">
class	                CSS styling	                <h2 class="section-title">
style	                Inline CSS (avoid)	        <h2 style="color:red">
lang	                Language override	          <h2 lang="ur">اردو</h2>
dir	                  Direction	                  <h2 dir="rtl">اردو</h2>
title	                Tooltip	                    <h2 title="Hover text">

8.2 Obsolete Attributes
Attribute	            Replacement
align	                CSS text-align
bgcolor	              CSS background-color
color	                CSS color
size	                CSS font-size

8.3 Anchor Linking (Zaroori!)
html
  <h2 id="introduction">Introduction</h2>
  <a href="#introduction">Introduction par jao</a>

Yeh table of contents banane ke liye use hota hai.

9. Headings vs Paragraphs vs Divs

Tag	                Kaam	                    Kab Use
<h1>-<h6>	          Structural heading	      Section titles
<p>	                Paragraph	                Text content
<div>	              Generic container	        Layout/styling
<span>	            Inline container	          Text styling

Rule: Agar woh section ka title hai → heading use karo. Agar woh paragraph hai → p use karo.

10. Browser Mein Kya Hota Hai?

10.1 Rendering
  1. Parser heading tag dekhta hai
  2. DOM node banata hai (HTMLHeadingElement)
  3. CSS apply (browser default ya custom)
  4. Render tree mein add
  5. Layout: block element, full width
  6. Paint: text render

10.2 Accessibility Tree
  Headings accessibility tree mein "heading" role assign hoti hai
  Level (1-6) bhi store hota hai
  Screen readers isse navigation karte hain

10.3 JavaScript Access
javascript
  // Select
  document.querySelector('h1');
  document.querySelectorAll('h1, h2, h3');
  
  // Read
  document.querySelector('h1').textContent;
  document.querySelector('h1').tagName;  // "H1"
  
  // Modify
  document.querySelector('h1').textContent = 'New';
  document.querySelector('h1').className = 'title';

11. Edge Cases / Gotchas

Gotcha 1: Multiple H1
html
  <h1>Title 1</h1>
  <h1>Title 2</h1>
Masla: SEO confusion. Best practice: 1 per page.
Fix: Ek h1, baaki h2.

Gotcha 2: Level Skip
html
  <h1>Title</h1>
  <h4>Section</h4>  ❌
Masla: Accessibility + SEO issue.
Fix: H2 ya H3 use karo.

Gotcha 3: Heading Sirf Size Ke Liye
html
  <h4>Bada text</h4>  ❌
Masla: Semantic galat. Screen reader confuse.
Fix: CSS se size, heading se structure.

Gotcha 4: Empty Heading
html
  <h2></h2>  ❌
Masla: Screen reader meaningless.
Fix: Descriptive text ya heading hata do.

Gotcha 5: Align Attribute
html
  <h2 align="center">  ❌
Masla: Obsolete. CSS modern hai.
Fix: <h2 style="text-align: center;"> ya class.

Gotcha 6: Heading Ke Andar Block
html
  <h2><div>Wrong</div></h2>  ❌
Masla: Invalid HTML. Browser auto-fix karega.
Fix: Sirf inline elements.

Gotcha 7: Heading As Link
html
  <a href="#"><h2>Click me</h2></a>  ❌ (mostly)
Masla: Accessibility issue — click target vs heading.
Fix: Heading ke andar link: <h2><a href="#">Click</a></h2>

Gotcha 8: Heading Missing In Section
html
  <section>
    <p>Content without heading</p>  ❌
  </section>
Masla: Structure unclear.
Fix: Section ko heading do.

Gotcha 9: Heading Change in SPA
Masla: React Router se navigation par h1 change nahi hota.
Fix: useEffect se document title + h1 update karo.

Gotcha 10: Lang Attribute Missing
html
  <h2>Urdu text</h2>  ❌ (agar page English hai)
Masla: Screen reader wrong pronunciation.
Fix: <h2 lang="ur">اردو</h2>

12. Tricky Interview Questions

Q1. Heading tag kya hai?
A: HTML structural element. Document outline banate hain. 6 levels (h1-h6).

Q2. Kitne H1 per page?
A: Ek. Page ka main topic. W3C recommends.

Q3. Kitne headings total per page?
A: No limit. Jitne sections, utne headings.

Q4. Heading level skip kar sakte hain?
A: Nahi. H1 → H2 → H3 logical order. Skip karne se accessibility + SEO issue.

Q5. H1 aur title tag mein farq?
A: 
  <title> = Browser tab + SEO metadata
  <h1> = Page ka visible main heading
  Dono related lekin different roles.

Q6. H1 mein keyword kitni baar?
A: 1-2 baar natural. Zyada = stuffing.

Q7. Kya h1 chhota dikha sakte hain?
A: Haan, CSS font-size se. Lekin semantic level same rahega.

Q8. Heading mein div aa sakta hai?
A: Nahi. Sirf inline elements (span, strong, em, a).

Q9. Multiple h1 galat kyun?
A: Google confuse hota. Screen reader user ko structure pata nahi chalta.

Q10. Heading size fix kaise karo?
A: CSS se — font-size, margin. Inline style better than attribute.

Q11. Headings screen reader kaise padhte hain?
A: Heading role assign hota hai. Users H key se navigate karte hain.

Q12. h1 ke liye SEO best practice?
A: Ek per page. Primary keyword front-load. Descriptive text. <60 chars.

Q13. Kya heading tag style ke liye use kar sakte hain?
A: Nahi, semantic ke liye use karo. Style CSS se.

Q14. h1 ke baad h3 aa sakta hai?
A: HTML valid hai, lekin accessibility fail. h2 use karo.

Q15. Heading ke andar image?
A: Haan, inline allowed. Alt text zaroori.

Q16. Hidden heading (visually) SEO mein?
A: Risky. Google penalty possible. Sirf a11y ke liye use karo.

Q17. h1 ke saath <a> tag?
A: <h1><a href="/">Title</a></h1> valid. <a><h1>Title</h1></a> mostly avoid.

Q18. Empty heading ka kya karo?
A: Hata do. Ya visually hidden text use karo.

Q19. Headings in cards/components?
A: Har card ko h3 (agar section ka part) ya h2. Hierarchy maintain karo.

Q20. SPA mein heading change?
A: useEffect se document.title + h1 update. Screen reader announcement ke liye.

Q21. h1 CSS reset se hide?
A: Screen readers ke liye hide mat karo. Visually hidden (clip) better.

Q22. Heading outline algorithm?
A: HTML5 mein multiple h1 ka plan tha, kabhi implement nahi hua. Ab bhi 1 h1 per page.

Q23. h1 mein HTML tags?
A: Inline only: <strong>, <em>, <a>, <span>, <br>. Block nahi.

Q24. Heading font ka best practice?
A: CSS se. rem units preferred (accessible). System fonts fast.

Q25. Kya heading role="heading" chahiye?
A: Nahi, heading tags automatically role assign karte hain.

13. Common Mistakes

Mistake	                              Fix
Multiple H1	                          Ek per page
Level skip	                          Logical hierarchy
Heading sirf size ke liye	            CSS se size
Empty heading	                        Descriptive text
align attribute	                      CSS text-align
Block elements in heading	            Inline only
Heading as link wrapper	              Link inside heading
Heading missing in section	          Har section ko heading
Keyword stuffing	                    Natural language
Duplicate headings	                  Unique per section
Generic text	                        Descriptive ("Intro" → "Intro to X")
Language override missing	            lang attribute
SPA without heading update	          useEffect se update
h1 > h2 > h4 (skip)	                  h1 > h2 > h3

14. Real-World Patterns

14.1 Blog Post
html
  <h1>Post Title</h1>
  <h2>Introduction</h2>
  <h2>Main Topic</h2>
    <h3>Subsection 1</h3>
    <h3>Subsection 2</h3>
      <h4>Detail</h4>
  <h2>Conclusion</h2>

14.2 Documentation
html
  <h1>API Reference</h1>
  <h2>Authentication</h2>
    <h3>API Keys</h3>
    <h3>OAuth</h3>
  <h2>Endpoints</h2>
    <h3>GET /users</h3>
    <h3>POST /users</h3>

14.3 Product Page
html
  <h1>Product Name</h1>
  <h2>Description</h2>
  <h2>Specifications</h2>
    <h3>Dimensions</h3>
    <h3>Weight</h3>
  <h2>Reviews</h2>

14.4 Landing Page
html
  <h1>Main Value Proposition</h1>
  <h2>Features</h2>
    <h3>Feature 1</h3>
    <h3>Feature 2</h3>
  <h2>Pricing</h2>
  <h2>FAQ</h2>

14.5 Portfolio
html
  <h1>Abu Bakar — Full Stack Engineer</h1>
  <h2>About Me</h2>
  <h2>Skills</h2>
    <h3>Frontend</h3>
    <h3>Backend</h3>
  <h2>Projects</h2>
  <h2>Contact</h2>

15. Modern Considerations (2026)

15.1 Search Engine Updates
  Google: H1 still important but content quality > keywords
  Bing: H1 + H2 combination matters
  AI Search: Headings help AI understand content

15.2 Voice Search
  Headings conversational ho to better
  Question-based headings (What, How, Why)

15.3 Accessibility Standards
  WCAG 2.2 stricter on headings
  Section headings required for long content
  Landmark + heading combo

15.4 Frameworks
  React: h1-h6 in components
  Next.js: Dynamic headings per route
  Vue: Component-based headings

15.5 AI Tools
  ChatGPT content: Headings zaroori
  AI SEO: Semantic structure help
  AI Reading: Headings se summary

16. Yaad Rakhne Ka Tareeqa

Headings ke 4 Rules:
  1. One H1 — Ek per page
  2. Logical — H1 → H2 → H3
  3. Descriptive — Clear text
  4. Semantic — Structure ke liye, style ke liye nahi

Memory Trick: "OLDS"
  O = One H1
  L = Logical order
  D = Descriptive
  S = Semantic purpose

17. Heading Structure Ka Framework

html
  <h1>Page Title (Primary Keyword)</h1>
  
  <section>
    <h2>Section 1 (Secondary Keyword)</h2>
    <p>Content...</p>
    
    <h3>Subsection 1.1</h3>
    <p>Content...</p>
    
    <h4>Detail 1.1.1</h4>
    <p>Content...</p>
  </section>
  
  <section>
    <h2>Section 2</h2>
    ...
  </section>

18. Charan Rule (5 H's)

  1. Hierarchy — Logical order
  2. Header — H1 sab se pehle
  3. Highlight — Keywords naturally
  4. Human — Descriptive text
  5. Handle — CSS se size, headings se structure

19. Final Notes

Headings:
  Document ka outline hain
  SEO ka important factor
  Accessibility ka base
  Screen reader navigation
  Content scannable banate hain
  
Ek line mein:
  "Headings = Document ka skeleton. Ek H1, logical hierarchy, 
   descriptive text — SEO, a11y, UX teenon kaam karenge."


DevTools Commands
  javascript
  // All headings
    document.querySelectorAll('h1, h2, h3, h4, h5, h6');

  // Count H1
    document.querySelectorAll('h1').length;

  // Heading text + level
    document.querySelectorAll('h1, h2, h3')
      .forEach(h => console.log(h.tagName, h.textContent));

Practice
  index.html kholo — outline generator try karo
  professional.html parho — real blog post structure
  Apni website ka heading hierarchy check karo
  H1 count karo (ek hi hona chahiye)
  Screen reader test karo (NVDA ya VoiceOver)

Testing Tools
  W3C Validator — HTML structure
  WebAIM — Accessibility check
  Lighthouse — SEO score
  Google Search Console — Actual SERP