OCSA Senior Hub — Editable Content Reference
This file documents all the content that lives in `index.html` and may need updating. Reference this file when you need to change content.
---
School Info
School name: Orange County School of the Arts (OCSA)
Address: 1010 N. Main St, Santa Ana, CA 92701
Website: ocsarts.net
Class: Class of 2026
Privacy contact: studentservices@ocsarts.net
---
Admin Emails
Defined at the top of the JS section as `ADMIN_EMAILS` array. Anyone who signs in with one of these emails gets admin access.
```js
const ADMIN_EMAILS = [
  'admin@ocsarts.net',
  'counseling@ocsarts.net',
  'studentservices@ocsarts.net',
  'arts@ocsarts.net',
  'financialaid@ocsarts.net',
  'henrykim.20081120@gmail.com',
  'hyojoon.kim@ocsarts.net',
  'shinekim008@gmail.com',
  'shine.kim@ocsarts.net',
  'anthony.tatsuta@ocsarts.net',
];
```
---
Conservatories (16 total)
Used in sign-up form and profile editor. Current list:
Acting
Arts & Enterprise
Classical & Contemporary Dance
Classical Voice
Commercial Dance
Creative Writing
Culinary Arts & Hospitality
Digital Media
Film & Television
Integrated Arts
International Dance
Instrumental Music
Musical Theater
Popular Music
Production & Design
Visual Arts
---
Checklist Items
Defined as `chkItems` array in JS. Each item has `l` (label), `d` (description), and `done` (default state).
#	Label	Description	Default
1	Register for SAT or ACT	Check if your target schools require scores	done
2	Request letters of recommendation	Ask conservatory director + 1 academic teacher	done
3	Start your Common App essay	650 words — lean into your artistic identity	done
4	Research arts colleges & conservatories	Reach / match / safety	todo
5	Complete FAFSA	Opens Oct 1 — file as soon as possible	todo
6	Build or update your arts portfolio / reel	Start early — quality over quantity	todo
7	Schedule auditions or portfolio reviews	Many arts colleges require separate portals	todo
8	Apply for early action / early decision	Nov 1–15 for most private schools	todo
9	Apply for CAEA and arts scholarships	CAEA deadline: Mar 1, 2027	todo
10	Submit UC / CSU application	Hard deadline: Nov 30, 2026	todo
11	Get senior conservatory photos & headshots	Needed for auditions and portfolios	done
12	Perform in senior conservatory showcase	Your final OCSA performance	todo
13	Submit remaining college applications	Regular decision: Jan 1–15, 2027	todo
14	Compare financial aid award letters	Letters arrive March–April 2027	todo
15	Make your final college decision	National Decision Day: May 1, 2027	todo
16	Celebrate graduation at OCSA	You trained for this. Take your bow.	todo
---
Default Events (seed data)
Shown before admins add anything. Defined as `DEFAULT_EVENTS` in JS. Admins can override via the Admin Panel.
Name	Month	Day	Date Display	Description
Senior Sunset	May	23	May 23, 2026	Last outdoor hangout before finals — a beloved OCSA tradition.
Senior Conservatory Showcases	Jun	~3	Jun 3–8, 2026	Final performances and exhibitions. Your last bow on the OCSA stage.
Prom	Jun	~6	Jun 6, 2026	Plan your look early — OCSA seniors bring the creative energy.
OCSA Graduation	Jun	~14	Jun 14, 2026	The main stage — cap, gown, and a crowd that knows how to celebrate.
---
Default Scholarships (seed data)
Defined as `DEFAULT_SCHOLARSHIPS` in JS.
Name	Badge	Deadline	Description
Scholastic Art & Writing Awards	portfolio	Jan 2027	Most prestigious recognition program for teen artists. Gold Key winners receive scholarships at many partner schools. All OCSA disciplines eligible.
CAEA Duane Hagen & Laurel Burch	California	Mar 1, 2027	For CA seniors majoring in visual art or design. Great for Visual Arts, Digital Media, and Film conservatories.
Jack Kent Cooke Young Artist Award	need-based	Check jkcf.org	$10,000 grant for outstanding young artists with financial need. Strong fit for music, dance, and theatre students.
Cal Grant A & B	California state	FAFSA by Mar 2, 2027	Up to full UC/CSU tuition. Need-based — file FAFSA or CADAA. Nearly all OCSA seniors attending a CA college should apply.
Gates Millennium Scholars	national	Jul 15, 2026	Up to full college costs. Minority students, GPA 3.3+. Covers tuition, room, board, and books.
---
Default Deadlines (seed data)
Defined as `DEFAULT_DEADLINES` in JS, organized by category.
Financial Aid
Name	Date	Description
FAFSA — file now	ASAP	Federal student aid
California FAFSA / CADAA priority	Mar 2, 2027	For Cal Grant consideration
CSS Profile (private arts colleges)	Rolling	CalArts, USC, NYU, Berklee
UC & CSU
Name	Date	Description
UC / CSU application window opens	Aug 1, 2026	All campuses open same day
UC / CSU application deadline	Nov 30, 2026	No late applications accepted
National Decision Day	May 1, 2027	Commit to your school
Arts Colleges
Name	Date	Description
CalArts (Valencia, CA)	Jan 5, 2027	Portfolio + audition required
USC Thornton / Roski / SCA	Dec 1, 2026	Music, Art, Cinematic Arts
Berklee College of Music	Jan 15, 2027	Audition required — schedule early
NYU Tisch School of the Arts	Jan 1, 2027	Supplemental arts application
Common App (Regular Decision)	Jan 1–15, 2027	Most private colleges
---
FAQs
Defined as `faqs` array in JS. Categories: `college`, `scholarships`, `arts`, `senior`.
Question	Category
When is the FAFSA deadline for California students?	scholarships
Do I need a separate application for UC schools vs Common App?	college
How many schools should I apply to?	college
Can I apply test-optional?	college
How do I ask my conservatory director for a letter of recommendation?	college
What arts scholarships are available for OCSA students?	scholarships
Is the FAFSA the same as the CSS Profile?	scholarships
Do I need a separate audition beyond Common App?	arts
How many pieces in my portfolio?	arts
When is OCSA graduation?	senior
What is National Decision Day?	college
---
Staff Contacts (placeholder — needs updating)
In the "Who to contact" tab of the Help panel:
Role	Description	Email (placeholder)
Student Services	Graduation, transcripts, general support	studentservices@ocsarts.net
College Counseling	Applications, deadlines, letters of rec, FAFSA	counseling@ocsarts.net
Arts Conservatories	Auditions, portfolios, conservatory questions	arts@ocsarts.net
Financial Aid	Scholarships, FAFSA, Cal Grant, award letters	financialaid@ocsarts.net
---
Sample Inbox Replies (hardcoded)
Three example Q&A pairs in the "Recent answers" tab. Currently hardcoded HTML — not dynamic.
Maria V. (Musical Theater) — "Do I need a separate audition video for CalArts if I already sent one through Common App?" → Yes — CalArts uses its own audition portal. Both must be completed.
Jordan R. (Film & Television) — "Is the FAFSA the same as the CSS Profile?" → No — FAFSA covers federal and state aid. CSS Profile is required separately by many private colleges.
Aiden L. (Visual Arts) — "How many pieces in my portfolio?" → Typically 10–20, varies by school. Lead with your strongest, show range.
---
Mood Check-In Messages
Defined as `moodMessages` object in JS:
Great: "That's great to hear! Keep riding that energy — senior year has some amazing moments ahead."
Okay: "Okay is perfectly fine. Senior year has its ups and downs — you're doing the work, and that matters."
Stressed: "Stress during senior year is real and valid. Try to take one thing off your plate today. The coping tips below can help."
Struggling: "Thank you for being honest with yourself. Struggling doesn't mean you're failing — it means you need support, and that's okay. Please look at the resources below."
---
Crisis Resources
In the Mental Health panel crisis box:
988 Suicide & Crisis Lifeline — call or text 988
Crisis Text Line — text HOME to 741741
OC Crisis Line — (877) 727-4747
In the resources section below:
OCSA School Counselors — Student Services · 1010 N. Main St
988 Suicide & Crisis Lifeline — Call or text 988
Teen Line — Call (800) 852-8336 or text TEEN to 839863
Headspace (free for students) — headspace.com/students
---
Privacy Policy
Effective date: May 25, 2026
Contact: studentservices@ocsarts.net
Address: 1010 N. Main Street, Santa Ana, CA 92701
Covers: COPPA (under-13), FERPA (student records), CCPA (California rights), cookies, third parties (Google Calendar, Google Fonts).
Status: Draft — needs attorney review before student launch.
