# Three Roads: Choosing the Portfolio Stack

## Constraints given
1. **Free only** — no paid hosting or tools
2. **Honest skill level** — learning MERN stack, comfortable with React/Next.js (built StudyBuddy capstone), still building depth
3. **What the portfolio needs to do** — display a sitemap of Home / Case Studies / Contact, following the content map (one-line claim, 3 case studies leading to a "message for interview" CTA)
4. **How work must be shown** — links to GitHub repos, an embedded/linked live demo (StudyBuddy), and long-form case study documents. Nothing needs to be dynamic yet.

## Three options considered

| | Simplest | Middle | Most Powerful |
|---|---|---|---|
| **Stack** | Plain HTML/CSS | Next.js (same as StudyBuddy) | Next.js + a headless CMS |
| **Hosting** | Vercel (free) | Vercel (free) | Vercel (free tier) |
| **Backend needed?** | No | Optional | Yes (CMS API) |
| **Trade-off** | No path to dynamic features without a rewrite | More setup, but easy to add features later | Powerful, but real learning curve for a feature not needed yet |

## Pressure-testing the front-runner (Simplest)
**What breaks if I pick the simplest?** If I ever want an on-page dynamic feature — like an embedded live quiz demo instead of just a link to StudyBuddy — plain HTML/CSS would need a rewrite to add that.
**Can I finish in two weeks?** Yes, easily — it's already built and live.
**Does it show my work the way it needs to be shown?** Yes — GitHub links, a live demo link, and case study documents are all just links and text, which plain HTML handles fine.

## Decision: Plain HTML/CSS

**Rationale, in my own words:**
I chose plain HTML/CSS because my portfolio right now only shows static content — my name, links to case studies, and a link to the live StudyBuddy demo. I don't need a dynamic feature (like a database or form submission) because that functionality already lives inside StudyBuddy itself. **Can I maintain this?** Yes — editing a single HTML file is simpler than maintaining a framework, especially while I'm still building depth in React/Next.js rather than mastering it. **Does it show my work well?** Yes — the case studies are GitHub links, the demo is a live Vercel link, and the whole page loads in under a second since there's no JavaScript bundle to download. If I ever need dynamic content later, I already know how to migrate to Next.js — I did exactly that for StudyBuddy — so nothing about this choice is a dead end.

**Alternatives not chosen, and why:**
- **Next.js:** Would work fine, but adds setup and build complexity for a page that's currently 100% static text and links. Overkill for the current need.
- **Next.js + CMS:** Rejected — the extra layer (content modeling, API keys, CMS learning curve) doesn't serve the actual goal right now, which is proving I can ship fast and reliably, not managing a content system.
