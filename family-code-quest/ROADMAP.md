# ROADMAP — Code Quest curriculum

## Philosophy
Teach **thinking like a builder** — decomposition, logic, and *directing AI* — not syntax. One learner, one track:
- **Raviraj (ScratchJr):** one tiny idea per day, concrete real-world example, emoji, read-aloud, 3 questions. Never punishing.

Daily rhythm: ~10–15 min (concept → quiz). Weekly: one "build it with AI" mission.

### Core distinction (runs through the whole syllabus)
The kid will *code with AI*, so the syllabus must keep two mental models clearly apart:
- 🤖 **The computer / the blocks** = a careful but *not-clever* robot. It does **exactly what you SAY**, step by step. Be precise; order matters.
- 🧠 **The AI** = a *clever* helper. You tell it **what you MEAN** in your own words and it writes the steps — but it can be wrong, so you **try it and fix it**.

Never teach "be exact or it won't work" as a blanket rule — that's true for the computer, not the AI. Scope literal-computer lessons to "the computer/blocks," and pair them with the AI contrast.

## Status
- ✅ **Week 1 — Telling the Computer What to Do** (Days 1–6): what a program is, **two helpers (computer vs AI)**, exact instructions (computer), order/sequence, sprites & the green flag, motion + review.
- ✅ **Week 2 — Repeating & Reacting** (Days 7–11): events, loops, forever loops, combining motion + loops, big review.
- ⬜ Weeks 3–10 below.

## To build

### Week 3 — Decisions: if / then
Concept: programs make choices — "IF it's raining, THEN take an umbrella." In ScratchJr: the touch/collision triggers.
Build mission idea: when the cat touches the edge (or a color), make it do something.

### Week 4 — Comparing & sensing
Concept: how a program *checks* things — is it touching? In ScratchJr: bump/touch tiles.
Build: make the cat react when it touches another sprite.

### Week 5 — Variables: the computer's memory
Concept: a variable is a labelled box that remembers a value — like a score. Keep it concrete (a counter of taps/catches).
Build: add a score that goes up when something happens.

### Week 6 — Decomposition
Concept: break a big idea into small steps (the core "solutioning" skill). Take "make a birthday card animation" and list the steps before building.
Build: plan a 4-step mini-animation on paper, then build it.

### Week 7 — Make a simple game (catch the falling apple 🍎)
Concept: combine everything — events, loops, sensing, a score.
Build: apple falls, move the basket, score when caught.

### Week 8 — How real apps work
Concept (kid-simple): every app has a **screen** (what you see), a **brain** (the steps), and a **memory** (what it remembers).
Build: draw the screen / brain / memory of a favourite app.

### Week 9 — Building WITH AI
Concept: you don't have to write every line — you describe what you want, read what the AI makes, try it, and fix it. The skill is *clear instructions* (callback to Week 1: computers/AI do what you say).
Build: ask the AI helper to add a feature to the Week 7 game; read its suggestion and try it.

### Week 10 — Family project
Concept: design and build something small together, start to finish. Decompose → build → test → show.
Build: pick one idea and ship it.

## Authoring notes
- Keep the track readable aloud and free of typing-heavy tasks (ScratchJr has no text coding).
- Reuse earlier ideas in later quizzes to reinforce (spaced repetition) — including the computer-vs-AI distinction.
- Each new week: add a `WEEKS[n]` entry in `index.html` and remove its line from `FUTURE`.
- Single track only — keep everything at kid (5–7 year old) reading level.
- Honour the computer-vs-AI distinction: "exact/literal" lessons are about the computer; "describe what you want, then check & fix" is about the AI.
