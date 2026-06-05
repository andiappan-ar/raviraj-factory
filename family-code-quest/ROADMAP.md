# ROADMAP — Family Code Quest curriculum

## Philosophy
Teach **thinking like a builder** — decomposition, logic, and *directing AI* — not syntax. Both learners cover the same idea each day, at two levels:
- **kid (Raviraj, ScratchJr):** one tiny idea, concrete real-world example, emoji, read-aloud, 3 questions. Never punishing.
- **grownup (Anusha, Scratch):** same idea slightly deeper, a "why" on each answer, 4–5 questions.

Daily rhythm: ~10–15 min (concept → quiz). Weekly: one "build it with AI" mission together.

## Status
- ✅ **Week 1 — Telling the Computer What to Do** (Days 1–5): what a program is, exact instructions, order/sequence, sprites & the green flag, motion + review.
- ✅ **Week 2 — Repeating & Reacting** (Days 6–10): events, loops, forever loops, combining motion + loops, big review.
- ⬜ Weeks 3–10 below.

## To build

### Week 3 — Decisions: if / then
Concept: programs make choices — "IF it's raining, THEN take an umbrella." In Scratch: the `if` block; ScratchJr: the touch/collision triggers.
Build mission idea: when the cat touches the edge (or a color), make it do something.

### Week 4 — Comparing & sensing
Concept: how a program *checks* things — is it touching? is a number bigger? In Scratch: sensing + comparison operators; ScratchJr: bump/touch tiles.
Build: make the cat react when it touches another sprite.

### Week 5 — Variables: the computer's memory
Concept: a variable is a labelled box that remembers a value — like a score. In Scratch: `variables` + `change score by 1`; ScratchJr: keep it concrete (a counter of taps/catches).
Build: add a score that goes up when something happens.

### Week 6 — Decomposition
Concept: break a big idea into small steps (the core "solutioning" skill). Take "make a birthday card animation" and list the steps before building.
Build: plan a 4-step mini-animation on paper, then build it.

### Week 7 — Make a simple game (catch the falling apple 🍎)
Concept: combine everything — events, loops, sensing, a score. 
Build: apple falls, move the basket, score when caught.

### Week 8 — How real apps work
Concept (kid-simple): every app has a **screen** (what you see), a **brain** (the steps), and a **memory** (what it remembers). Map to frontend / backend / data without jargon for the kid; name them for the grownup.
Build: draw the screen / brain / memory of a favourite app.

### Week 9 — Building WITH AI
Concept: you don't have to write every line — you describe what you want, read what the AI makes, try it, and fix it. The skill is *clear instructions* (callback to Week 1: computers/AI do what you say).
Build: ask the AI helper to add a feature to the Week 7 game; read its suggestion and try it.

### Week 10 — Family project
Concept: design and build something small together, start to finish. Decompose → build → test → show.
Build: pick one idea as a family and ship it.

## Authoring notes
- Keep the kid track readable aloud and free of typing-heavy tasks (ScratchJr has no text coding).
- Reuse earlier ideas in later quizzes to reinforce (spaced repetition).
- Each new week: add a `WEEKS[n]` entry in `index.html` and remove its line from `FUTURE`.
