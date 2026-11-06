# The Data Diaries With Dee - website

The website for **thedatadiarieswithdee.com**, the course and training platform of
The Data Diaries With Dee (Accra, Ghana). Based on the files in this folder, it is
a plain static website: HTML, CSS and JavaScript files with no build step. The
repository this folder came from is `Debv122/The-Data-Diaries-With-Dee` on GitHub,
and the site is hosted on Vercel.

## What is in this folder

| File(s) | What they are |
|---|---|
| `index.html` | Home page |
| `about-data-with-dee.html`, `faq.html`, `emberlern.html`, `corporate-data-training-ghana.html`, `python-training-ghana.html` | Information and landing pages |
| `course-01*.html` ... `course-04*.html`, `course-cyber*.html` | Course overview pages, module pages and capstone pages |
| `login.html`, `account.html` | Sign-in page and learner account page |
| `auth.js` | The accounts system as implemented in code: sign-up/sign-in, module gating, progress tracking and drill submissions (uses Supabase, see below) |
| `vercel.json` | Vercel settings (clean URLs, no trailing slash) |
| `sitemap.xml`, `robots.txt`, `llms.txt`, `BingSiteAuth.xml` | SEO and search-engine verification files |
| `*.jpg` | Photos used on the site |
| `data-diaries-site_2.zip` | An older snapshot of the site from September 2026, kept inside this folder. Safe to delete once you confirm you don't need it. |

## How the courses are set up in the code

`auth.js` configures five courses:

1. How to Be a Top-Notch Data Analyst (`course-01`, 10 modules + capstone)
2. AI for Business Operations (`course-02`)
3. The Assistant They Can't Replace (`course-03`, 10 modules + capstone)
4. The Ticket That Doesn't Come Back (`course-04`, 10 modules + capstone)
5. Cyber Security Fundamentals (`course-cyber`, 8 modules + capstone)

Per that configuration, the first 3 modules of every course are open to
everyone; from module 4 onward (and all capstones) visitors are asked to create
a free account. Signed-in learners get buttons to mark modules complete and to
save written drill answers.

Note: this gating happens in the visitor's browser. `auth.js` hides the lesson
visually until the person signs in, but the lesson text is still inside the page
file itself, so it is a sign-in prompt, not real content protection. Anyone who
opens the page's source can read it.

## Accounts and progress (Supabase)

`auth.js` is written to connect to a **Supabase** project for learner accounts,
progress and submissions. The connection details (project URL and public anon
key) are already filled in at the top of `auth.js`; the anon key is designed to
be public. **Never** put the Supabase *service_role* key in any file in this
folder - it must stay secret.

Other settings at the top of `auth.js`:

- `GOOGLE_LOGIN: false` - "Sign in with Google" is off until Google sign-in is
  enabled in the Supabase dashboard.
- `FREE_MODULES: 3` - how many modules of each course stay open without an account.

The code expects two tables in the Supabase project: `progress` and
`submissions`. Whether those tables are actually set up is something to confirm
in the Supabase dashboard; the code can't verify that from here. If a save
fails, the learner sees a "Could not save" message on the page.

The descriptions above reflect what the supplied code is written to do. They
don't confirm the live backend is working end to end - that needs a quick test
on the live site (sign up, mark a module complete, save an answer).

## How to make changes

There is nothing to install and no build step.

1. Edit the HTML/CSS/JS files (for example by pasting updated code from Claude).
2. Upload or commit the changed files to the GitHub repository
   `Debv122/The-Data-Diaries-With-Dee`.
3. If the repository is connected to a Vercel project (the presence of
   `vercel.json` suggests it is set up for that), Vercel republishes the site
   automatically after each push. If it isn't connected yet, import the
   repository in the Vercel dashboard once and future pushes will deploy
   automatically.

To preview the site on your own computer, either double-click `index.html`, or
run this in the project folder and open http://localhost:8000 :

```
python -m http.server 8000
```

## Known open items

- **Course 02 vs Course 04 mismatch.** The files named `course-02-*.html`
  contain "The Ticket That Doesn't Come Back" lessons, but `auth.js` labels
  course 02 as "AI for Business Operations" and course 04 as "The Ticket That
  Doesn't Come Back". The course-02 files also run to module 10 while `auth.js`
  expects 8 for course 02. Decide which numbering is right, then rename files or
  update `auth.js` so they agree.
- **`data-diaries-site_2.zip`** inside this folder is an old snapshot and can be
  removed to keep the repository tidy.
- **Apex domain (historical, unverified).** As of October 2026,
  `www.thedatadiarieswithdee.com` loaded but the bare domain
  `thedatadiarieswithdee.com` (no www) did not. That was a DNS setting in
  Vercel's Domains settings. It may have been fixed since; check both addresses
  before acting on this.
