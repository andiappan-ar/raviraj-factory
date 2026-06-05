# Code Quest 🚀

A tiny, day-by-day coding curriculum + quiz app for one young learner — **Raviraj** (ScratchJr).

Each day is one small concept + a short quiz; each week ends with a "build it with AI" mission. A parent **Dashboard** shows daily progress and a weekly review.

## Run it
- Open `index.html` in any browser, **or**
- Serve it: `python3 -m http.server` then visit `http://localhost:8000`

## Deploy (get a shareable URL)
- **Netlify Drop** — drag this folder onto https://app.netlify.com/drop (instant URL)
- Or **Cloudflare Pages / Vercel / GitHub Pages** — entry file is `index.html`

## Add more lessons
The full plan is in `ROADMAP.md`; the how-to is in `CLAUDE.md` → *How to add lessons*. In short: copy a day object in the `CURRICULUM` array inside `index.html`, change the text, done.

## Note on saved progress
Progress is saved in the browser (localStorage). Perfect on one device — the dashboard shows Raviraj's progress. It does **not** sync across separate devices. For cross-device monitoring, see the Supabase path in `CLAUDE.md`.

## Develop with Claude Code
Open this folder in Claude Code — it automatically reads `CLAUDE.md`. Then ask, for example:

> Add Week 3 (if/then decisions), Days 11–13, following the data model and kid-only rules in CLAUDE.md.

or

> Migrate to the Next.js + Supabase sync version described in CLAUDE.md.

## Files
- `index.html` — the whole app (deployable)
- `CLAUDE.md` — context + rules for Claude Code
- `ROADMAP.md` — curriculum plan and per-week notes
- `README.md` — this file
