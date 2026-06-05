# CLAUDE.md — Code Quest

Context for Claude Code working on this project. Read this fully before editing.

## What this is
A day-by-day coding curriculum + quiz web app built for **one young learner**:
- **Raviraj** — the son, under 8, **ScratchJr** track. Short, playful, emoji-heavy, read-aloud.

This is a **single-track, kid-only** syllabus. There is no second (grownup/parent) learner track. The goal is teaching **computational thinking + directing AI**, not syntax memorization. Tone is warm and encouraging; wrong answers are never punished.

## Core principle: computer ≠ AI (keep these distinct)
The kid codes *with AI*, so the syllabus must hold two mental models apart and never blur them:
- 🤖 **The computer / Scratch blocks** = a careful but *not-clever* robot. Does **exactly what you SAY**, step by step. Be precise; order matters.
- 🧠 **The AI** = a *clever* helper. You tell it **what you MEAN** in plain words; it writes the steps — but it can be wrong, so you **try it and fix it**.

Rules when authoring:
- Never teach "be exact or it won't work" as a universal truth. That's the **computer's** nature, not the AI's. Scope literal/exact lessons to "the computer/blocks."
- The dedicated lesson is **Day 2 — "Two Helpers: the Computer & the AI."** Reinforce the contrast in later review days and build missions.
- Build missions = AI mindset: *describe what you want → try it → fix it together.*

## Stack & philosophy
- A single self-contained **`index.html`** — vanilla HTML/CSS/JS. **No build step, no framework, no npm dependencies.** Only external resource is Google Fonts (Fredoka + Nunito) via CDN.
- Must keep working in **three** environments without changes:
  1. opened directly as a local file (`file://`),
  2. hosted as a static site (Netlify / Cloudflare Pages / Vercel),
  3. rendered as a Claude artifact.
- Keep it single-file and dependency-free unless explicitly migrating (see *Future: sync version*).

## Run / deploy
- Run locally: open `index.html`, or `python3 -m http.server` then visit `http://localhost:8000`.
- Deploy: drag this folder onto **Netlify Drop** (app.netlify.com/drop), or push to Cloudflare Pages / Vercel / GitHub Pages. Entry file **must** be `index.html`.

## Architecture (everything lives in the `<script>` in index.html)
- **`Store`** — storage abstraction. Tries `window.storage` (Claude artifact API, async) → `localStorage` → in-memory object. Always `await Store.get(key)` / `await Store.set(key, value)`. **Never call `localStorage`/`sessionStorage`/cookies directly** — going through `Store` is what keeps all three environments working.
- **`LEARNER`** — the one learner (role, avatar, default name, tool).
- **`CURRICULUM`** — array of *day objects*. **This is the content you edit to add lessons.**
- **`WEEKS`** — per-week `title` + a weekly `build` mission.
- **`FUTURE`** — roadmap labels shown for weeks not yet built.
- **Screen render functions** (each rewrites `#app`): `renderHome` → `renderRoadmap` → `openDay` (concept) → `startQuiz`/`renderQuestion`/`answer`/`nextQ` → `finishQuiz`; plus `renderDashboard` (parent view: stats, weekly review, recent activity).
- **`speak()`** — read-aloud via `SpeechSynthesis`.
- **Confetti** — small canvas burst on good scores (`miniBurst`, `bigConfetti`).
- **`sattr()`** — escapes strings for safe embedding inside inline `onclick='...'` attributes (apostrophes/quotes). Use it whenever passing text into an inline handler.

## Data model
A day object:
```js
{
  day: 11, week: 3, title: "If / Then", emoji: "🔀",
  concept: "short, warm, emoji-rich, read-aloud sentence...",
  quiz: [
    { q: "question?", o: [ {e:"🍪", t:"Recipe"}, {e:"😴", t:"Nap"} ], a: 0 }
  ]
}
```
Rules:
- `a` = index of the correct option. The renderer highlights the correct one regardless of position; vary positions so it isn't always first.
- **quiz**: 3 questions (4 for a week-review day), an emoji (`e`) on every option. Keep reading level very low (a 5–7 year old, often read to by a parent). No "why" explanations — this is the kid track.
- Feedback copy must stay gentle. Do not add scoring that shames wrong answers.

Progress is stored under key `fcq:progress`:
```js
{ completed: { [day]: stars1to3 }, dates: { [day]: ISO }, builds: { [week]: ISO | false }, lastActive: ISO }
```
The learner name is stored under `fcq:name` (default: Raviraj).

## How to add lessons (the most common task)
1. Find the `CURRICULUM` array in `index.html`.
2. Copy an existing day object; set the new `day` number and its `week`.
3. Write `concept` (one warm, emoji-rich sentence) and `quiz` (3 questions, emoji on each option).
4. If it starts a new week, add a `WEEKS[n]` entry (`title` + `build`) and delete that week's line from `FUTURE`.
5. That's it — days unlock sequentially and render on the map automatically; no other wiring.
6. Verify: open the file, play the new day, confirm the dashboard counts update.

## Pending content (roadmap)
Weeks 1–2 are written (Days 1–11; Week 1 = Days 1–6, Week 2 = Days 7–11). Still to build, keeping ScratchJr-appropriate (no typing-heavy tasks):
- Week 3 — Decisions: if / then
- Week 4 — Comparing & sensing (is it touching? is it bigger?)
- Week 5 — Variables: the computer's memory (keep a score)
- Week 6 — Decomposition: break a big idea into small steps
- Week 7 — Make a simple game (catch the falling apple)
- Week 8 — How real apps work: screen, brain & memory (frontend / backend / data, kid-simple)
- Week 9 — Building WITH AI: describe → get code → try → fix
- Week 10 — Family project: design & build something together

See `ROADMAP.md` for per-week concept notes.

## Constraints / don'ts
- No build step, no framework, no npm deps. One static file.
- Never touch `localStorage`/`sessionStorage`/cookies directly — use `Store`.
- Don't break the three-environment storage fallback.
- Don't make wrong-answer feedback harsh; keep the reading level low.
- Keep it single-track (kid only). Don't reintroduce a second learner track.
- Keep changes to `index.html` unless told to migrate.

## Future: cross-device sync version (separate track — only when asked)
`localStorage` is per-device, so a parent can't monitor from their own phone. For real sync, migrate to **Next.js + Supabase**:
- Tables: `learner(id, name, tool, avatar)`, `progress(learner_id, day, stars, completed_at)`, `build_missions(learner_id, week, completed_at)`.
- Move `CURRICULUM`/`WEEKS` into a shared module; keep the same screen flow.
- Replace `Store` with Supabase client calls; add magic-link auth so each device writes to the right learner and the dashboard reads live.
Default remains the static single-file version.
