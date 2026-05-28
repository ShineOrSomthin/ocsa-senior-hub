OCSA Senior Hub — Project Context
What This Is
A senior year companion web app for Orange County School of the Arts (OCSA), 1010 N. Main St, Santa Ana, CA 92701. Built for the Class of 2027. The entire app is a single HTML file (`index.html`) with no build system, no framework, no dependencies beyond two CDN links.
Live Site
Hosted on GitHub Pages. The file in this repo (`index.html`) IS the app. Edit it, commit, and the live site updates within ~60 seconds.
Tech Stack
Single file: `index.html` — all HTML, CSS, and JS in one file
Fonts: DM Sans (titles/headings) + Patrick Hand (body/handwriting feel) via Google Fonts
Icons: Tabler Icons webfont via jsDelivr CDN (`ti ti-*` classes)
Storage: Abstracted helper functions — works with `localStorage` when hosted, falls back to `window.storage` when running inside a preview renderer
No framework, no bundler, no npm
Design System
Colors (CSS variables)
```css
--oo: #ef5c21  /* OCSA orange — primary accent */
--bl: #0f5ba8  /* OCSA blue */
--re: #e9282f  /* OCSA red */
--ye: #fcb712  /* OCSA yellow */
--pi: #ad0553  /* OCSA pink */
--ink: #1a1209   /* primary text — warm near-black */
--ink2: #3a2a14  /* secondary text */
--ink3: #6b5030  /* muted text */
--pa: #faf7f0    /* paper white */
--pa2: #f3ede0   /* paper surface */
--pa3: #ece4ce   /* paper background */
--ru: rgba(15,91,168,0.13)  /* ruled line color */
```
Fonts
```css
--T: 'DM Sans', sans-serif      /* titles, headings, buttons, labels */
--P: 'Patrick Hand', sans-serif /* body text, nav items, descriptions */
```
Aesthetic
Notebook / paper aesthetic. Warm cream backgrounds with faint blue ruled lines (`repeating-linear-gradient` with `--ru`). Cards are slightly translucent white on top of the ruled paper. The vibe is a real art school sketchbook.
Highlight Boxes — Option D (important design decision)
We deliberately moved away from the overused "light colored fill + matching border" pattern. All highlight/callout boxes use Option D:
`background: var(--pa2)` — paper texture, no color fill
`border-top: 3px solid [accent color]` — colored top stripe only
`border-radius: 0` — square corners on these
Text in `var(--ink)` / `var(--ink3)` — NOT tinted to match the border color
```css
/* Example: yellow tip box */
background: var(--pa2);
border-top: 3px solid var(--ye);
border-radius: 0;
```
Badges
Transparent background, colored border only:
```css
.bo { background: transparent; color: #8c2e0a; border: 1.5px solid var(--oo); }
/* same pattern for .bb .br .by .bp .bg2 .bt */
```
Sidebar Section Headers
Color-coded by section with a right-extending rule:
Overview → orange (`--oo`)
Opportunities → blue (`--bl`)
Senior Life → yellow (`--ye`)
Arts Prep → red (`--re`)
Wellbeing → pink (`--pi`)
Staff Admin → dark background label
---
App Structure
Navigation Panels
Each section is a `<div id="panel-X" class="panel">`. The `show(p)` function switches panels. Panel IDs map to `navMap` array in JS.
```
home, profile, checklist, scholarships, college, events,
activities, auditions, essays, testing, mentalhealth, help, admin, privacy
```
Auth System
Sign-in screen shown when no saved session
Email/password accounts stored in `localStorage` (`ocsa_users` key)
Passwords stored as `btoa()` encoded (not truly secure — note for future improvement)
Auto-login via `ocsa_last_user` key
Google sign-in is a placeholder — not real OAuth yet
Admin System
Controlled by `ADMIN_EMAILS` array at top of JS. Anyone signing in with a listed email gets:
Admin badge in topbar
Admin Panel in sidebar
Ability to add/delete events, scholarships, deadlines
Current admin emails:
`admin@ocsarts.net`, `counseling@ocsarts.net`, `studentservices@ocsarts.net`, `arts@ocsarts.net`, `financialaid@ocsarts.net`
`henrykim.20081120@gmail.com`, `hyojoon.kim@ocsarts.net`, `shinekim008@gmail.com`, `shine.kim@ocsarts.net`, `anthony.tatsuta@ocsarts.net`
Live Data (Shared Storage)
Admin-published content uses shared storage keys:
`ocsa_shared_events`
`ocsa_shared_scholarships`
`ocsa_shared_deadlines`
Polls for updates every 30 seconds via `setInterval`.
Default seed data is defined in `DEFAULT_EVENTS`, `DEFAULT_SCHOLARSHIPS`, `DEFAULT_DEADLINES` constants — shown before admins add anything.
Per-User Private Storage
`ocsa_{uid}_checklist` — which tasks are checked
`ocsa_{uid}_consent` — whether consent banner was dismissed
`ocsa_users` — all account data
`ocsa_last_user` — auto-login uid
Storage Abstraction
The app works in two environments:
Hosted HTML — uses `localStorage`
Preview renderer — uses `window.storage` API
Abstraction functions at top of JS: `stGet`, `stSet`, `stDel`, `stGetShared`, `stSetShared`
Never use `localStorage` directly — always go through these helpers so the app keeps working in both environments.
Search Helper
`openSearch(text)` opens a Google search for the given query in a new tab. Used by the "Find more scholarships", activity tiles, and conservatory tag buttons.
OCSA Logo
Inlined SVG — five colored polygons, no external image file:
```html
<svg viewBox="0 0 503.5 508.5">
  <polygon points="67.5 116.5 .5 261 138 325 204 179.5 67.5 116.5" fill="#ef5c21"/>
  <polygon points="404 .5 279.5 5.5 284.5 134 380 131 409 120 404 .5" fill="#0f5ba8"/>
  <polygon points="249 226.5 154.5 293.5 138 325.5 120.5 318.5 76.5 350.5 190.5 508 363 383 249 226.5" fill="#fcb712"/>
  <polygon points="165.5 16.5 145.5 103 226 121 246 34.5 165.5 16.5" fill="#ad0553"/>
  <polygon points="445 108.5 299.5 161.5 357.5 320 503 267 445 108.5" fill="#e9282f"/>
</svg>
```
Used at three sizes: 80px (auth screen), 38px (topbar), 32px (sidebar).
---
Key JS Functions Reference
Function	What it does
`init()`	Boot — checks for saved session, shows auth or app
`loginUser(uid, ud)`	Sets currentUser, loads checklist, starts polling
`renderUserUI()`	Updates topbar avatar, name, admin state, profile fields
`show(p)`	Switches active panel, updates sidebar nav highlight
`loadLiveData()`	Fetches shared events/scholarships/deadlines from storage
`startPolling()`	Sets 30s interval to refresh live data
`buildChk()`	Renders checklist, updates progress bar and stats
`tog(i)`	Toggles checklist item and saves to storage
`addEvent()`	Admin: adds event to shared storage
`addScholarship()`	Admin: adds scholarship to shared storage
`addDeadline()`	Admin: adds deadline to shared storage
`calBtn(title, start, end, desc)`	Returns HTML for Google/Apple calendar add button
`openSearch(text)`	Opens a Google search for the given query in a new tab
`renderFaqs(filter)`	Renders FAQ list with optional category filter
`selectMood(el, mood)`	Handles mood check-in selection
`dismissConsent()`	Hides consent banner, saves to user storage
---
What's Intentionally Placeholder / TODO
[ ] Google OAuth — `googleSignIn()` creates a fake account. Needs real Google Cloud OAuth when hosted on a proper domain. See `docs/ROADMAP.md` for steps.
[ ] Help form backend — `submitQ()` shows a success message but doesn't actually send anything. Needs Formspree, Google Forms, or similar.
[ ] Staff email addresses — contact cards throughout use placeholder `@ocsarts.net` addresses. Update with real staff contacts before student launch.
[ ] Event dates — default event dates (graduation, prom, etc.) are approximate. Admins should update via Admin Panel once official dates are confirmed.
[ ] Privacy policy legal review — drafted to cover COPPA, FERPA, CCPA. Needs OCSA attorney review before student-facing launch.
[ ] Password security — currently `btoa()` encoded, not truly hashed. Fine for prototype, needs upgrade for production.
---
Future Plans
App Store / Google Play — plan is to wrap with Capacitor (WebView wrapper). GitHub Pages stays as the source of truth. Apple Developer account ($99/yr) + Google Play ($25 one-time) needed when ready.
Custom domain — can point a domain like `seniorsocsa.com` to GitHub Pages via DNS settings.
Real Google OAuth — needs a hosted domain first, then ~1hr setup in Google Cloud Console.
---
File Structure in This Repo
```
index.html          ← The entire app
docs/
  README.md         ← This file (project context and developer reference)
  ROADMAP.md        ← Pending features and priorities
  DESIGN.md         ← Design decisions and component reference
  CONTENT.md        ← All editable content (checklist items, FAQs, default data)
```
---
How to Make Changes
Edit `index.html` locally (VS Code recommended)
Test by opening the file directly in a browser
When ready: go to GitHub repo → click `index.html` → pencil icon → paste new code → commit
Live site updates within ~60 seconds
Hard refresh browser (Cmd+Shift+R / Ctrl+Shift+R) to clear cache
---
Developer Notes
Key rules to follow when making any changes to this codebase:
Single file app — all changes go in `index.html`
Storage abstraction — always use `stGet`/`stSet`/`stGetShared`/`stSetShared`, never `localStorage` directly
Highlight boxes — always use Option D (paper bg + colored top border, no fill). See Design System above.
Typography — `--T` for all titles/headings/labels, `--P` for all body text. Never swap these.
Notebook aesthetic — warm paper colors, ruled line backgrounds, dashed borders. Don't introduce bright fills or modern flat UI patterns.
Search helper — use `openSearch()` for any "open results in a new tab" button
Badges — transparent background, border only. No light fills.
New panels — add the panel ID to `navMap` array and create a corresponding `.ni` nav item in the sidebar
