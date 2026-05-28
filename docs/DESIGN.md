OCSA Senior Hub — Design Reference
Core Aesthetic
Notebook / paper — the app looks like a physical art school sketchbook. Every design decision reinforces this.
Warm cream paper backgrounds (`--pa`, `--pa2`, `--pa3`)
Faint blue ruled lines across every surface via `repeating-linear-gradient`
Cards are translucent white sitting on top of the ruled paper
Dashed borders (`border: 1.5px dashed rgba(26,18,9,0.18)`) for softer elements
Slight rotation on hover for activity cards (feels hand-placed)
---
Typography
Two fonts, used consistently:
Font	Variable	Use
DM Sans	`--T`	All titles, headings, card titles, buttons, labels, nav section headers, badges, stat numbers
Patrick Hand	`--P`	All body text, descriptions, nav item labels, form inputs, placeholders, everything conversational
Never mix these up. DM Sans = structure and hierarchy. Patrick Hand = the handwriting voice.
---
Color System
Five OCSA brand colors used as accents. Never used for large fills.
```
--oo: #ef5c21  orange
--bl: #0f5ba8  blue
--re: #e9282f  red
--ye: #fcb712  yellow
--pi: #ad0553  pink
```
Sidebar section headers are color-coded to these:
Overview → orange
Opportunities → blue
Senior Life → yellow
Arts Prep → red
Wellbeing → pink
The topbar stripe at the top of the app cycles through all five colors left to right.
---
Highlight / Callout Boxes — Option D
This is the most important design rule. We explicitly decided against the overused pattern of light colored fill + matching colored border — it looks generic and cheap.
Option D rule:
```css
background: var(--pa2);        /* paper texture, no color */
border-top: 3px solid [color]; /* colored stripe at top only */
border-radius: 0;              /* square corners */
color: var(--ink);             /* normal dark ink text */
```
Examples in the codebase:
`.crisis-box` → red top border
`.tip-mh` cards → each has its own accent color top border
`.pp-notice` → yellow top border
`.pp-hl` → orange top border
`.success-box` → green top border
`.inbox-reply` → green top border
Never do `background: #fde8dc; border: 1.5px solid var(--oo)` — that's the pattern we replaced.
---
Badges
Small inline labels (e.g. "don't wait", "California state", "national").
```css
/* Pattern: transparent bg, colored border, dark text from same family */
background: transparent;
border: 1.5px solid [color];
color: [dark shade of same color];
font-family: var(--T);
font-size: 9.5px;
font-weight: 700;
text-transform: uppercase;
letter-spacing: 0.3px;
padding: 2px 7px;
border-radius: 2px;
```
Classes: `.bo` (orange), `.bb` (blue), `.br` (red), `.by` (yellow), `.bp` (pink), `.bg2` (green), `.bt` (teal)
---
Cards
```css
.nb-card {
  background: rgba(255,255,255,0.7);  /* translucent white on paper */
  border: 2px solid rgba(26,18,9,0.14);
  border-radius: 3px;
  padding: 14px 16px;
  margin-bottom: 12px;
}
```
Card titles use `.ct` (DM Sans, 14px, 700 weight).
Card body uses `.cb` (Patrick Hand, 13px, 600 weight).
---
The OCSA Logo
Five polygon SVG, no external file. Used at three sizes throughout the app.
```html
<svg viewBox="0 0 503.5 508.5" xmlns="http://www.w3.org/2000/svg">
  <polygon points="67.5 116.5 .5 261 138 325 204 179.5 67.5 116.5" fill="#ef5c21"/>
  <polygon points="404 .5 279.5 5.5 284.5 134 380 131 409 120 404 .5" fill="#0f5ba8"/>
  <polygon points="249 226.5 154.5 293.5 138 325.5 120.5 318.5 76.5 350.5 190.5 508 363 383 249 226.5" fill="#fcb712"/>
  <polygon points="165.5 16.5 145.5 103 226 121 246 34.5 165.5 16.5" fill="#ad0553"/>
  <polygon points="445 108.5 299.5 161.5 357.5 320 503 267 445 108.5" fill="#e9282f"/>
</svg>
```
Sizes used: `width="80"` (auth screen), `width="38"` (topbar), `width="32"` (sidebar)
---
Icons
Tabler Icons webfont. Loaded via CDN:
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@2.44.0/tabler-icons.min.css">
```
Usage: `<i class="ti ti-[name]" aria-hidden="true"></i>`
Common icons used in the app:
Navigation: `ti-home`, `ti-user`, `ti-list-check`, `ti-award`, `ti-building-community`, `ti-calendar-event`, `ti-confetti`, `ti-microphone`, `ti-pencil`, `ti-clipboard-check`, `ti-heart`, `ti-help-circle`, `ti-shield`, `ti-edit`, `ti-lock`
Actions: `ti-plus`, `ti-trash`, `ti-check`, `ti-send`, `ti-search`, `ti-logout`, `ti-calendar-plus`
Status: `ti-circle-check`, `ti-urgent`, `ti-info-circle`, `ti-shield-check`
Content: `ti-flame`, `ti-chart-bar`, `ti-bulb`, `ti-mood-smile`, `ti-building-hospital`
Always add `aria-hidden="true"` on decorative icons.
---
Ruled Line Background
Applied to sidebar, main content area, and auth screen:
```css
background-image: repeating-linear-gradient(
  transparent, transparent 27px,
  var(--ru) 27px, var(--ru) 28.5px
);
```
Where `--ru: rgba(15,91,168,0.13)` — a very faint blue.
---
Topbar Color Stripe
The 6px rainbow stripe at the very top:
```css
background: linear-gradient(90deg,
  var(--pi) 0%, var(--pi) 20%,
  var(--oo) 20%, var(--oo) 40%,
  var(--ye) 40%, var(--ye) 60%,
  var(--re) 60%, var(--re) 80%,
  var(--bl) 80%, var(--bl) 100%
);
```
---
User Avatars
Color-coded by email hash — deterministic so the same user always gets the same color. Eight color pairs defined in `AVC` array. Initials extracted from display name.
```js
const AVC = [
  {bg:'#fde8dc',c:'#8c2e0a'},
  {bg:'#dce8f8',c:'#0e2d68'},
  // ... 6 more
];
function getAC(email) { /* hash email → index into AVC */ }
function getInits(name) { /* first + last initial */ }
```
---
What NOT To Do
- Light fill + matching border on highlight boxes (the overused pattern we replaced)
- Use `localStorage` directly — always use `stGet`/`stSet` helpers
- Hardcode the Google search URL on individual buttons — go through `openSearch()`
- Use DM Sans for body text or Patrick Hand for titles
- Add `border-radius` to Option D boxes (they're square by design)
- Hardcode colors instead of CSS variables
- Bright saturated fills for large areas — colors are accents only
