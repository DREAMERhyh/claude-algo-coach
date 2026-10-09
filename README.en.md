# claude-algo-coach

**Turn your AI into a coach, not an answer generator.**

A coaching skill (prompt rules) for [Claude Code](https://claude.com/claude-code), built for competitive programming and algorithm practice — Luogu, Codeforces, ICPC/CCPC training, university algorithm courses. Anywhere you have "a problem to solve and code to write yourself".

> [中文说明](README.md)

---

## The problem: getting code from AI does not mean you learned it

The usual pattern:

> "How do I solve this?" → AI produces complete code → you understand it → next problem.

The result: **you can read it, but you can't write it.**

Algorithm skill comes from thinking it through and writing it yourself. A complete answer handed to you skips exactly that process.

## The fix: constrain the AI into a coach

This skill locks the AI's behavior with **four iron rules**:

| Rule | Meaning |
|---|---|
| 🚫 **Never give complete code** | Even if you say "I can't", "just give it to me", "just this once" |
| 🤔 **Don't think for you** | When stuck, it asks "where do you think you're stuck?" — direction and self-check methods, not answers |
| 📖 **Anchor every issue to your lecture notes** | "This was covered in Lecture 07 §7.7 — go take another look" |
| 🔁 **Debrief immediately after each AC** | Dual-track notes: per-problem summary + cross-problem mistake list |

## How a session flows

### Stage 1: Opening — framework only, no code

You drop in the problem statement and say "let's do this one". The coach reads it and gives:

1. **One-line restatement** (plain words, not a copy of the statement)
2. **What it drills** (the concept being practiced)
3. **Step breakdown** (pure prose, zero code)
4. **Pitfalls** (raised as *questions*: "What happens to your loop when n=0?")
5. **Suggested self-test data** (you come up with a boundary case)

It always closes with: *"Try writing it — ask me whenever you're stuck, tell me your thinking."*

### Stage 2: While you write — four graded hint levels (strictly one at a time)

| Level | Trigger | What you get |
|---|---|---|
| 1️⃣ Direction | First "I'm stuck" | Direction only: "It's a loop boundary issue — hand-simulate sample 3" |
| 2️⃣ Location | Still stuck | The exact line/variable at fault — **but not how to fix it** |
| 3️⃣ Pseudocode | Still stuck | Pseudocode for **that step only**, not the whole problem |
| 4️⃣ Snippet | Genuinely can't | **That small piece** of code, with the reasoning explained |

Most of the time one or two levels is all you need — and that's exactly the "figure it out yourself" process you want.

### Stage 3: After AC — immediate debrief

Line-by-line review (style / habits / hazards: out-of-bounds, overflow, uninitialized values, strict weak ordering…), every issue anchored to a lecture section; anything outside your notes is explicitly flagged as new knowledge.

### Stage 4: Dual-track notes

- **Per-problem summary** → 1–3 lines appended to the problem file (key insight / pitfalls hit / reusable pattern)
- **Cross-problem pitfalls** → appended to a root-level `易错点清单.md` (only "mistakes I'll make again on another problem")
- The two tracks are kept separate so the list never turns into a diary

## Does it work?

The author has used it across three settings: **Luogu practice, Codeforces, and a university Algorithms course**. Practical observations:

- **No more "AI writes, I read"** — you write everything; the AI only offers the smallest hint when you're stuck
- **Hints are graded** — from "point a direction" to "show a snippet"; shallow hints usually suffice
- **Debriefs compound** — per-problem notes accumulate into your own personal pitfalls library; the list of repeated mistakes shrinks
- **Notes-linked** — every issue maps to a section of your own material, so review is grounded
- **Cheap to port** — the same rules moved from Luogu → Codeforces → coursework with ~10 lines changed each time (see `examples/`)

## Install (Claude Code)

In your practice project root:

```bash
mkdir -p .claude/skills/algo-coach
curl -o .claude/skills/algo-coach/SKILL.md \
  https://raw.githubusercontent.com/DREAMERhyh/claude-algo-coach/main/SKILL.md
```

Then open `SKILL.md` and edit **two things** to fit you:

1. **User profile** — your current level and goal (it determines how the coach treats you)
2. **Lecture-notes map** — if you have your own course notes/textbook, fill in the chapter mapping (optional)

Finally, open a Claude Code session from the project root and say "let's do this problem".

> 💡 A project-level `CLAUDE.md` describing the coaching mode makes it stickier. All three `examples/` show this pattern.

## Repository layout

```
.
├── README.md            # Chinese
├── README.en.md         # You are here
├── SKILL.md             # Generic coaching rules (skeleton — edit two spots)
└── examples/
    ├── luogu.md         # Luogu adaptation (problem-set folders, P1001.md + P1001.cpp)
    ├── codeforces.md    # Codeforces adaptation (contest folders, auto-fetch English statements)
    └── coursework.md    # University coursework adaptation (instructor-provided problems)
```

The `examples/` files are **complete, ready-to-use versions** — copy one to `.claude/skills/algo-coach/SKILL.md` and start.

## Requirements

- Claude Code (project skill: `.claude/skills/<name>/SKILL.md`)
- (Optional, strongly recommended) Your own lecture notes / textbook — rule 3 depends on it
- (Optional) Problem statement files; if missing, the coach will help you turn problems into files first

## License

[MIT](LICENSE)
