# Ship an Automation Workflow v2: Source-Grounded Study Notes Pipeline

## Pipeline Overview
A 4-step pipeline that turns any topic into a study-ready package: a comprehensive study guide and a quiz, built entirely from real sources rather than the model's memory.

**Tool:** NotebookLM (Google) — chosen because it's built specifically for source-grounded synthesis, which the brief itself calls the strongest no-code option for gather-and-synthesize work.

## Step-by-Step Flow

```
[1. GATHER] → [2. SYNTHESIZE] → [3. DRAFT] → [4. REVIEW]
```

**1. Gather** — Create a new notebook per topic. Use NotebookLM's built-in web search ("Add sources" → search) to pull in real, current source material (official docs, tutorials) rather than relying on the model's training data alone.

**2. Synthesize** — Use the Studio panel's "Study Guide" report. NotebookLM reads every imported source and produces a structured document: architectural overview, a reference table of key concepts, common mistakes, and a glossary — all traceable back to the actual sources.

**3. Draft** — Use the Studio panel's "Quiz" tool on the same source set. This generates comprehension questions with an answer key, grounded in the same material as the study guide (not a separate, ungrounded generation).

**4. Review** — Manually skim the study guide and quiz for anything a human still needs to check (see "Failure Points" below). This step is intentionally not automated — the brief requires knowing what still needs human judgment, not eliminating it.

## Five Real Runs

| # | Topic | Sources Found | Time |
|---|---|---|---|
| 1 | React Hooks | 10 (official React docs) | 7 min |
| 2 | Git & version control | Multiple tutorials/docs | 5 min |
| 3 | Next.js basics | Multiple tutorials/docs | 3 min |
| 4 | JavaScript async/await | Multiple tutorials/docs | 3 min |
| 5 | SQL basics | Multiple tutorials/docs | 4 min |

**Average: ~4.4 minutes per topic**, each producing a full study guide (overview, reference table, common mistakes, essay questions, glossary) and a comprehension quiz with an answer key.

## Time-Saved Estimate
Manually researching a topic, writing a structured study guide, and drafting a quiz with an answer key takes me an estimated **45–60 minutes** per topic. At ~4.4 minutes per topic through this pipeline, that's roughly a **90% time reduction** — turning what would be most of an hour into under 5 minutes.

## Known Failure Points (what a human must still check)
1. **Source quality varies by topic.** NotebookLM's web search picked 10 official sources for React Hooks (a well-documented topic) but fewer, more varied sources for something like SQL basics. A human should skim the source list before trusting the output — a thin source set produces a thinner (though still usable) study guide.
2. **No guarantee of technical accuracy on edge cases.** The study guide is grounded in its sources, but if a source itself has a minor inaccuracy or is slightly outdated, that error carries through. This is the single most important thing to spot-check — I would not publish or study from a guide without at least skimming it against something I already know.
3. **Quiz difficulty is not tunable.** All 5 runs produced comprehension-level questions (2-3 sentence answers) plus essay-level questions — there's no built-in way to ask for, say, only multiple-choice or only beginner-level questions. A human has to decide if the difficulty matches the actual study need.
4. **Essay questions are intentionally left unanswered.** This is correct behavior (they're meant for reflection), but it means the "draft" step isn't 100% autonomous — a learner still has to do the actual thinking for that section.

## Deliverable Links
- Notebooks: created per-topic in NotebookLM (personal Google account, not publicly shareable by default)
- This document: pushed to the portfolio/capstone repo for reference
