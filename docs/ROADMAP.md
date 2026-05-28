OCSA Senior Hub — Roadmap
High Priority (Before Student Launch)
1. Connect the Help Form to a Real Backend
File: `index.html` → `submitQ()` function
Current state: Shows a success message but sends nothing.
Options (simplest first):
Formspree — free tier, just change the fetch URL. No backend needed.
Google Forms — embed or post to a Google Form endpoint.
Airtable — free tier, gives a proper inbox with filters.
Implementation: Replace the `submitQ()` function body with a `fetch()` POST to whichever service.
---
2. Real Google OAuth
Current state: `googleSignIn()` creates a fake account called "OCSA Student".
Requirements before doing this:
App must be hosted at a real domain (GitHub Pages URL works, or a custom domain)
Need a Google Cloud Console project (free)
Register the domain as an authorized origin
Steps when ready:
Go to console.cloud.google.com → New project
APIs & Services → Credentials → Create OAuth 2.0 Client ID
Add your GitHub Pages URL to authorized JavaScript origins
Add the Google Identity Services script to `index.html`
Replace `googleSignIn()` with real `google.accounts.id.initialize()` flow
User's real name, email, and profile photo come back automatically
Time estimate: ~1 hour first time.
---
3. Update Staff Email Addresses
File: `index.html` → Who to contact tab in the Help panel
Current: Placeholder `@ocsarts.net` addresses
Action: Replace with real staff contacts for Student Services, College Counseling, Arts, and Financial Aid.
---
4. Confirm Official Event Dates
File: `index.html` → `DEFAULT_EVENTS` array (top of JS)
Current: Approximate dates for Senior Sunset, Showcases, Prom, Graduation
Action: Once OCSA confirms official dates, update via the Admin Panel (no code change needed). The Admin Panel at the bottom of the sidebar lets admins add/edit/delete events.
---
5. Privacy Policy Legal Review
File: `index.html` → `panel-privacy`
Status: Drafted to cover COPPA, FERPA (California), and CCPA. Covers all the right areas but needs an attorney to sign off before real students use it.
Contact: OCSA's district attorney or an education law firm familiar with California student privacy law.
---
6. Upgrade Password Storage — done
Implementation: Passwords are hashed with PBKDF2-SHA256 (100k iterations) and a per-user random salt via the Web Crypto API. See `hashPassword()` in `index.html`.
Still recommended long-term: switch to Google OAuth so passwords never live in the browser at all.
---
Medium Priority (Nice to Have)
Custom Domain
Buy a domain (e.g. `ocsaseniohub.com` or `seniors.ocsarts.net`)
In GitHub repo → Settings → Pages → Custom domain → enter domain
Add a CNAME record in your domain registrar's DNS pointing to `yourusername.github.io`
Takes ~24 hours to propagate
Push Notifications for Deadline Reminders
Would need a service worker + Push API
Free tier options: OneSignal, Firebase Cloud Messaging
Could notify students of upcoming deadlines they haven't checked off
Scholarship Search Filter
Currently shows all scholarships in one list
Could add a filter by conservatory so students see the most relevant ones first
Pure JS, no backend needed — just filter the `liveScholarships` array
Dark Mode
App is currently light-only (warm paper aesthetic)
Could add a toggle that switches to a dark ink/charcoal version
Would need a second set of CSS variables
---
Long-Term (App Store)
Capacitor Wrapper for iOS + Android
What it is: Capacitor takes the existing HTML app and wraps it in a native shell so it can be submitted to the App Store and Google Play. Your actual code doesn't change.
Steps when ready:
Install Node.js and Capacitor CLI (`npm install -g @capacitor/cli`)
`npx cap init` in the project folder
`npx cap add ios` and `npx cap add android`
`npx cap sync` to pull in the web code
Open Xcode (iOS) or Android Studio (Android) to build and submit
Accounts needed:
Apple Developer Program: $99/year (required for App Store)
Google Play Developer: $25 one-time fee
Privacy policy requirement: Both stores require a publicly accessible URL for your privacy policy. Since it's currently built into the app, you'd also need to host it as a standalone page — GitHub Pages makes this easy (just add a `privacy.html` file to the repo).
Timeline estimate: 1–2 days of setup, then 1–3 days for Apple review (Google is usually same-day).
