# AI Agent Building 101 — Workshop Resources

A static workshop companion with event details, two guided live demos, and a
curated resource center for the *AI Agent Building 101: From Concept to Working
Prototype* talk (PMI Florida Suncoast, July 14, 2026).

## Structure

```
workshop-site/
├── index.html              # the page
├── resources/
│   └── index.html          # PM and business analyst AI resource center
├── demo-1/
│   ├── index.html          # Demo #1: Project Analyzer Agent (live-demo companion)
│   └── demo-1.css          # demo page design system
├── demo-2/
│   └── index.html          # Demo #2: Meeting Intelligence Agent
├── assets/                 # favicon and brand mark, shared across pages
├── vercel.json             # clean routes, legacy redirects, and security headers
├── event.ics               # downloadable calendar event
```

No build step — plain HTML/CSS, ready to deploy as-is.

## Deploy to Vercel

1. Push this folder to a GitHub repo (see below).
2. Go to [vercel.com/new](https://vercel.com/new) and import the repo.
3. Framework preset: **Other**. Leave the build command empty and set the
   output directory to `.` (the repo root) — there's nothing to build.
4. Deploy. Vercel will give you a live URL immediately.

## Push to GitHub

From inside this folder:

```bash
git init
git add .
git commit -m "Add workshop resources page"
gh repo create ai-agent-building-101-resources --public --source=. --remote=origin --push
```

(Or create the repo manually on github.com and `git remote add origin <url>`
followed by `git push -u origin main`.)

## Updating

Editing `index.html`, either demo page, `resources/index.html`, or `event.ics` and pushing to the
connected GitHub branch will trigger an automatic redeploy on Vercel.
