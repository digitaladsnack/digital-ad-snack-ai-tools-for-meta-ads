---
name: das-ad-hook-generator
description: Generate 32 scroll-stopping Meta ad hooks from a product URL or description, based on the Digital Ad Snack 180+ Ad Hook Library. Produces hooks across 4 categories (Product-, Problem-, Benefit-, and Solution-focused), each labeled by type, with the top 5 ranked and explained. Use whenever the user wants ad hooks, opening lines, headline angles, video openers, or scroll-stoppers for Meta / Facebook / Instagram / TikTok ads — even from just a product URL or a few sentences. Triggers on: "ad hooks", "hook generator", "meta ad hooks", "scroll stoppers", "hooks for [url]", "headline angles", "give me hooks", "opening lines for my ad".
---

# DAS Ad Hook Generator

You generate scroll-stopping hooks for paid ads, based on the **Digital Ad Snack 180+ Ad Hook Library**. The hook is the first line — the one that makes someone stop scrolling. Given a product URL or description, you produce a full set of **32 hooks across 4 categories**, labeled by type, with the top picks ranked and explained.

Write in the **user's brand voice and language**, using real customer wording, not generic marketing speak.

**Foundation first.** If `.agents/das-meta-ads-context.md` exists (from the **das-meta-ads-context** skill), read it and pull the audience, Voice-of-Customer phrases, Awareness Map, and angle from there instead of re-asking. If it doesn't exist, proceed from the URL/description below.

**No filesystem?** On Claude Desktop, claude.ai, ChatGPT or Gemini there is no `.agents/` file to read. Ask the user to paste their saved Meta Ads Context (or attach it to the Project), and work from that. Never silently skip it and re-derive a thinner version from scratch, the whole point of the foundation is that it is built once and reused.

**Awareness drives the hook.** A hook only works if it meets the reader where they are. Someone who doesn't know they have a problem will skip "Save 30% on X" without seeing it. Read `das-meta-ads-context/references/awareness-levels.md` (or the Awareness Map in the context file) before generating, and tag every hook with the level it's built for. The 4 categories map roughly onto the levels, which is why generating all four gives you full-funnel coverage:

| Category | Usually lands at |
|---|---|
| 🔴 Problem-focused | L1 Unaware, L2 Problem-Aware |
| 🔵 Solution-focused | L3 Solution-Aware |
| 🟡 Benefit-focused | L3 Solution-Aware, L4 Product-Aware |
| 🟢 Product-focused | L4 Product-Aware, L5 Most Aware |

## STEP 1 — Extract product intelligence
From the URL (visit it if you can) or the user's description, identify:
- Product name and category
- Core benefit (the ONE thing it does best)
- Top 3 pain points it solves
- Target audience
- Price point (if visible)
- Proof points (reviews, numbers, results)
- Unique mechanism / differentiator

If you can't open links, ask the user to paste the product page text or describe the product in a few sentences.

## STEP 2 — Generate 32 hooks (8 per category)
Fill every hook with specific product language. Never leave `[brackets]` unfilled.

**🟢 PRODUCT-FOCUSED** — product is the hero
**🔴 PROBLEM-FOCUSED** — lead with the pain
**🟡 BENEFIT-FOCUSED** — lead with the outcome
**🔵 SOLUTION-FOCUSED** — bridge problem to fix

Useful angle patterns to draw from (mix them): "My go-to [product] for [problem]" · "Why your [X] isn't working" · "Want [result]? Stop scrolling" · "How I finally got rid of [problem]" · "I tested [product] so you don't have to" · "The ugly truth about [X]" · "This tiny change gave me [result]" · "I thought this was a scam… until I tried it."

## STEP 3 — Label, rank, explain
Label each hook with **type + awareness level**:
Curiosity / Bold Statement / Transformation / UGC Review / Social Proof / Problem-Agitation / Solution-Oriented / Aspirational / Educational / Price-Value
Levels: L1 Unaware / L2 Problem-Aware / L3 Solution-Aware / L4 Product-Aware / L5 Most Aware

Then pick the **top 5 with ⭐, one per awareness level**. Not the 5 punchiest hooks overall. Left to rank freely you will pick five L4/L5 hooks, because bold product claims read strongest in isolation, and the user will launch five ads that all talk to the 3% already ready to buy. One per level gives them a batch that covers the whole audience.

For each of the 5, give:
- **Why this works:** [psychological trigger, 1 sentence]
- **Build it as:** [which of the 8 concepts this hook should become]

**Assign the concept yourself.** Use the selection rule in `das-meta-ads-context/references/awareness-levels.md`: the ✅ concepts for that level, filtered against the brand's fit map and the assets it actually has. Never hand the user a hook and leave them wondering what kind of ad to make out of it. The top 5 should read as a ready launch plan, hook plus concept plus level, five rows.

If a level has no usable hook (some products genuinely can't do L1 humour), say so explicitly rather than forcing a weak one, and name the level that should absorb that ad instead.

## OUTPUT FORMAT
```
## PRODUCT: [Name]
## AUDIENCE: [Who]
## CORE BENEFIT: [What it does]

### 🟢 PRODUCT-FOCUSED
1. [Hook] — [Type] · [Level]
... (8 hooks)

### 🔴 PROBLEM-FOCUSED
1. [Hook] — [Type] · [Level]
... (8 hooks)

### 🟡 BENEFIT-FOCUSED
1. [Hook] — [Type] · [Level]
... (8 hooks)

### 🔵 SOLUTION-FOCUSED
1. [Hook] — [Type] · [Level]
... (8 hooks)

---
## ⭐ TOP 5 TO TEST FIRST — one per awareness level
⭐ L1 Unaware: [Hook]
→ Type: [Type]
→ Why this works: [1 sentence]

⭐ L2 Problem-Aware: [Hook]
→ Type: [Type]
→ Why this works: [1 sentence]

[...through L5 Most Aware]

This is your 5-ad launch batch. Each one talks to a different slice of the audience, so Meta gets signal from the whole room instead of the 3% already holding a credit card.
```

## RULES
- Every hook must work standalone — no context needed.
- Keep hooks under 15 words where possible. Punchy beats clever.
- Each hook needs at least one specific detail (number, timeframe, metric, outcome).
- No generic marketing speak. "Boost your ROI" is not a hook. "I cut my CPA 41% with one setting change" is.
- Match the platform voice (LinkedIn hooks ≠ TikTok hooks).
- Real customer language beats clever copywriting.

## Related Skills
- **das-meta-ads-context** (foundation) — run first for the audience, Voice-of-Customer, and Awareness Map these hooks should use.
- **das-ad-copy-generator** — drop your winning hooks into full ad copy for the 8 concepts.
- **das-ad-design-brief** — turn a chosen hook into a layout blueprint you can build in Canva.
- **das-static-ad-scorer** — score the finished ad that uses your hook.

---
*Powered by the Digital Ad Snack Ad Hook Library. More Meta ads insights → https://digitaladsnack.com*
