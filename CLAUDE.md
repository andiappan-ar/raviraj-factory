# CLAUDE.md — Family Code Quest

Context for Claude Code working on this project. Read this fully before editing.

## What this is
A day-by-day coding curriculum + quiz web app built for one family:
- **Raviraj** — the son, under 8, **ScratchJr** track (`track: 'kid'`). Short, playful, emoji-heavy, read-aloud.
- **Anusha** — the wife, complete beginner, **Scratch** track (`track: 'grownup'`). One level deeper, with "why" explanations.

The goal is teaching **computational thinking + directing AI**, not syntax memorization. Tone is warm and encouraging; wrong answers are never punished.

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
- **`PROFILES`** — the two learners (`son`, `wife`): track, avatar, color vars, tool, default name.
- **`CURRICULUM`** — array of *day objects*. **This is the content you edit to add lessons.**
- **`WEEKS`** — per-week `title` + a dual-track weekly `build` mission.
- **`FUTURE`** — roadmap labels shown for weeks not yet built.
- **Screen render functions** (each rewrites `#app`): `renderPicker` → `renderRoadmap` → `openDay` (concept) → `startQuiz`/`renderQuestion`/`answer`/`nextQ` → `finishQuiz`; plus `renderDashboard` (parent view: per-learner stats, weekly review, recent activity).
- **`speak()`** — read-aloud via `SpeechSynthesis` (used on the kid track).
- **Confetti** — small canvas burst on good scores (`miniBurst`, `bigConfetti`).
- **`sattr()`** — escapes strings for safe embedding inside inline `onclick='...'` attributes (apostrophes/quotes). Use it whenever passing text into an inline handler.

## Data model
A day object:
```js
{
  day: 11, week: 3, title: "If / Then", emoji: "🔀",
  concept: { kid: "short, warm, emoji...", grownup: "a bit deeper..." },
  quiz: {
    kid: [
      { q: "question?", o: [ {e:"🍪", t:"Recipe"}, {e:"😴", t:"Nap"} ], a: 0 }
    ],
    grownup: [
      { q: "question?", o: [ {t:"Right answer"}, {t:"Distractor"} ], a: 0, ex: "why it's right" }
    ]
  }
}
```
Rules:
- `a` = index of the correct option. The renderer highlights the correct one regardless of position; vary positions so it isn't always first.
- **kid quiz**: 3 questions, an emoji (`e`) on every option, no `ex`. Keep reading level very low (a 5–7 year old, often read to by a parent).
- **grownup quiz**: 4–5 questions, include `ex` (the "why") on each. No emoji needed on options.
- Feedback copy must stay gentle. Do not add scoring that shames wrong answers.

Progress is stored per learner under key `fcq:progress:<son|wife>`:
```js
{ completed: { [day]: stars1to3 }, dates: { [day]: ISO }, builds: { [week]: ISO | false }, lastActive: ISO }
```
Names under `fcq:names` → `{ son, wife }` (defaults: Raviraj / Anusha).

## How to add lessons (the most common task)
1. Find the `CURRICULUM` array in `index.html`.
2. Copy an existing day object; set the new `day` number and its `week`.
3. Write `concept.kid` + `concept.grownup`, then `quiz.kid` (3 Q) and `quiz.grownup` (4–5 Q with `ex`).
4. If it starts a new week, add a `WEEKS[n]` entry (`title` + dual-track `build`) and delete that week's line from `FUTURE`.
5. That's it — days unlock sequentially and render on the map automatically; no other wiring.
6. Verify: open the file, play the new day on **both** profiles, confirm the dashboard counts update.

## Pending content (roadmap)
Weeks 1–2 are written (Days 1–10). Still to build, keeping ScratchJr-appropriate for the kid track (no typing-heavy tasks) and Scratch for the grownup track:
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
- Don't make wrong-answer feedback harsh; keep the kid track's reading level low.
- Keep changes to `index.html` unless told to migrate.

## Future: cross-device sync version (separate track — only when asked)
`localStorage` is per-device, so a parent can't monitor from their own phone. For real sync, migrate to **Next.js + Supabase**:
- Tables: `learners(id, name, track, avatar)`, `progress(learner_id, day, stars, completed_at)`, `build_missions(learner_id, week, completed_at)`.
- Move `CURRICULUM`/`WEEKS` into a shared module; keep the same screen flow.
- Replace `Store` with Supabase client calls; add magic-link auth so each device writes to the right learner and the dashboard reads live.
Default remains the static single-file version.
