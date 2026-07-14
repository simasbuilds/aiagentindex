# CLAUDE.md

## Project purpose

This repository contains the companion website for the **AI Agent Building 101: From Concept to Working Prototype** presentation and workshop. Attendees should be able to open one memorable domain during the presentation, follow along, find workshop exercises and supporting resources, and download the presentation materials afterward.

The site is intended to be published from GitHub to Vercel and may later use a custom domain.

## Audience and experience

The primary audience is a mixed business and project-management group, not necessarily a technical audience. Keep language plain, concise, and action-oriented.

The page should make these actions immediately understandable:

1. Follow the live presentation.
2. Open the workshop exercise materials.
3. Download the slide decks and other resources.
4. Return later to review the material or continue learning.

Important links:

- Live presenter: <https://aiagentspresentation.vercel.app/presenter#1>
- Workshop exercise files/PDFs: <https://drive.google.com/drive/folders/1m_kXiXqz4AMeSwhoeEl1qaCERgEwvnkQ?usp=sharing>

External resources should open in a new tab with `target="_blank"` and `rel="noopener noreferrer"`. Downloadable files stored in this repository should use clear file names and the HTML `download` attribute where appropriate.

## Current implementation

This is intentionally a small static site:

```text
workshop-site/
├── index.html
├── resources/
│   └── index.html
├── demo-1/
│   ├── index.html
│   ├── demo-1.css
│   └── downloads/
│       └── project-analyzer-agent.zip
├── demo-2/
│   ├── index.html
│   └── downloads/
│       └── meeting-intelligence-agent.zip
├── assets/
│   ├── logo.svg
│   ├── logo-512.png
│   ├── apple-touch-icon.png
│   ├── favicon-16.png
│   └── favicon-32.png
├── vercel.json
├── event.ics
├── README.md
├── CLAUDE.md
```

- `index.html` contains all HTML, CSS, and a small progressive-enhancement script for scroll reveals.
- `resources/index.html` is the enterprise resource center for project managers and business analysts, including role-based workflows, prompt guidance, governance, and workshop downloads.
- `demo-1/index.html` is the live-demo companion page: it walks attendees through building a Project Analyzer Agent (scenario, source PDFs, a copy-to-clipboard starting prompt, live-build steps, the exact final `CLAUDE.md`/`SKILL.md` file contents with per-file copy buttons, a one-click `downloads/project-analyzer-agent.zip` of the complete finished agent, and debrief questions).
- `demo-2/index.html` is the Meeting Intelligence Agent companion page. It uses three Teams transcript PDFs from the linked Google Drive folder and reuses the Demo #1 design system, including the same final-output pattern: the exact `CLAUDE.md`/`SKILL.md`/delivery-brief file contents with per-file copy buttons and a one-click `downloads/meeting-intelligence-agent.zip` of the complete finished agent.
- `assets/` holds the site's favicon and brand mark, reused across all pages.
- Public routes are `/`, `/resources/`, `/demo-1/`, and `/demo-2/`. Keep the legacy redirects in `vercel.json` so old `.html` and `/workshop-exercises/` links continue to work.
- There is no JavaScript framework, package manager, build command, or generated output.
- `event.ics` is the attendee-downloadable calendar event and must stay synchronized with the visible date, time, venue, and presentation URL.
- The builder toolkit in `index.html` is a curated set of third-party GitHub resources with client-side search and category filters.
- Google Fonts are the only current remote design dependency.

Do not introduce a framework, build system, or package dependency unless the requested feature genuinely requires it. Prefer semantic HTML and small amounts of vanilla CSS/JavaScript.

## Content priorities

When extending the page, preserve a simple top-to-bottom attendee journey:

1. Hero with event identity and a strong primary action.
2. Live presentation/follow-along link.
3. Workshop exercises and resource links.
4. Downloadable slide decks.
5. Event details.
6. Presenter information and follow-up links.

Use descriptive calls to action such as **Follow the presentation**, **Open workshop exercises**, and **Download the foundations deck**. Avoid vague labels such as “Click here.” Clearly distinguish links that open a web resource from files that download.

Do not claim that a Google Drive resource is a direct PDF download unless its final URL points to an actual file. The current workshop link is a shared Drive folder, so label it as a folder or collection of workshop files.

## Design direction

Preserve the live presentation's cinematic agent-operations aesthetic:

- Near-black `#07110f` and `#030806` backgrounds, `#0c1916` panels, lime `#c8ff3d`, mint `#78f6c7`, orange `#ff7747`, blue `#5aa7ff`, and pale text `#e9eee7`.
- Bricolage Grotesque and Syne for display type, Manrope for body copy, and DM Mono for technical labels.
- Cinematic dark surfaces, lime-to-mint emphasized words, subtle 64px technical grids, grain, thin glowing borders, ghosted oversized type, and precise mono annotations.
- Responsive layouts that collapse cleanly below `760px`.

New sections should reuse the existing CSS variables, typography, card language, button styles, and spacing system. Avoid generic SaaS visuals, excessive gradients, animations that distract from workshop use, or unnecessary decorative elements.

## Accessibility and usability

- Use semantic landmarks and heading levels in order.
- Every interactive element must be reachable and visibly focused with a keyboard.
- Do not rely on color alone to communicate meaning.
- Maintain readable color contrast and a minimum comfortable tap target of about 44px.
- Add meaningful accessible text to icon-only controls; decorative SVGs should be hidden from assistive technology.
- Respect `prefers-reduced-motion` for any new motion.
- Keep the essential attendee actions usable on mobile and on venue Wi-Fi.
- Never put essential instructions only inside a downloadable deck.

## Editing rules

- Make focused changes and preserve working content unless the request calls for a rewrite.
- Keep asset paths relative so GitHub and Vercel deployments behave the same way.
- Use lowercase, hyphenated file names for new downloads.
- Do not embed secrets, private URLs, analytics keys, or credentials in this public static repository.
- Check external copy, event details, dates, and presenter information before changing them.
- Keep toolkit URLs direct (never Google redirect URLs), verify that repositories still resolve, label community projects honestly, and avoid implying endorsement or guaranteed security.
- When adding or removing toolkit cards, update the visible resource total and the JavaScript count message together.
- If a custom domain is added, keep the Vercel URL functional as a fallback and document any DNS/configuration change in `README.md`.

## Local verification

Because the site has no build step, serve it locally from `workshop-site/`:

```bash
python3 -m http.server 8000
```

Then review `http://localhost:8000/` at desktop and mobile widths. Before considering a change complete, verify:

- The page loads without console errors or missing local files.
- The live presenter link opens at slide `#1`.
- The Google Drive workshop folder opens and is shared with the intended audience.
- Navigation anchors land on the correct sections.
- Keyboard focus, hover states, and mobile layouts remain usable.
- Page title and description still accurately describe the event.

## Deployment

The repository should deploy to Vercel as a static site using the **Other** framework preset, with no build command and `.` as the output directory when `workshop-site/` is the repository root.

Push changes to the GitHub branch connected to Vercel. Vercel should redeploy automatically. After deployment, test the public URL rather than assuming local relative links behave identically.

If the parent directory becomes the GitHub repository root instead, either configure Vercel's root directory as `workshop-site` or move the site files to the repository root. Do not leave Vercel pointed at a directory that does not contain `index.html`.
