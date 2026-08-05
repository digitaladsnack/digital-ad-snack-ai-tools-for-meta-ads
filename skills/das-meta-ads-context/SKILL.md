---
name: das-meta-ads-context
description: "When the user wants to set up or update their Meta ads context — the foundation document every DAS Meta ads skill reads first. Also use when the user mentions 'meta ads context', 'set up context', 'buyer persona for ads', 'voice of customer', 'positioning for my ads', 'who is my audience', 'awareness levels', 'problem aware', 'awareness funnel', 'executive summary for my ads', or is starting Meta ads work for a brand. Run this FIRST before the other DAS skills — it creates `.agents/das-meta-ads-context.md` that das-ad-hook-generator, das-ad-copy-generator, das-ad-design-brief, and das-static-ad-scorer all reference for product, audience, Voice-of-Customer, positioning, the 5 problem awareness levels, and the awareness x concept map."
metadata:
  version: 1.1.0
---

# DAS Meta Ads Context (Foundation Skill)

You help users create and maintain the **Meta Ads Context** document — the foundation that every other Digital Ad Snack Meta ads skill reads first, so the user never repeats their product, audience, or positioning. This is the DAS equivalent of a product-marketing brief, focused on what's needed to make scroll-stopping Meta ads.

The document is stored at **`.agents/das-meta-ads-context.md`**.

## Workflow

### Step 1 — Check for existing context
Check if `.agents/das-meta-ads-context.md` exists.
- **If it exists:** read it, summarize what's captured, ask which sections to update, and only re-gather those.
- **If it doesn't exist, offer two options:**
  1. **Auto-draft from a URL (recommended):** ask for the product/brand URL, read it, and draft a V1. (If you can't open links, ask the user to paste the page text or describe the product.)
  2. **Start from scratch:** walk through each section conversationally, one at a time.

### Step 2 — Gather information
Push for **verbatim customer language** — exact phrases from real reviews beat polished descriptions, because they reflect how customers actually think and become your highest-converting copy. Mark sourced phrases `[REAL QUOTE]` and your own inferences `[INFERRED]`.

Before writing sections 6 and 7, read `references/awareness-levels.md`. Then ask the one question that exposes the real gap:

> "Which of these does your current advertising sound like: (a) 'here's what we sell', (b) 'here's why we're better than the alternative', or (c) 'here's a discount'?"

Almost every answer is (a) or (c), which means the brand is only speaking to the ~8% of the audience that is Product-Aware or Most Aware. Say so plainly in the Awareness Map and name the biggest gap. That single observation is usually the most valuable line in the whole document.

### Step 3 — Review & save
Present the draft and ask: *"What needs correcting? What's missing?"* Iterate until the user approves, then write it to `.agents/das-meta-ads-context.md` and confirm the path.

---

## Sections to capture (the document structure)

```
# META ADS CONTEXT — [Brand]
_Language: [ads language] · Primary goal/KPI: [sales/leads/...]_

## 1. Product Snapshot
One-liner · what it does (2–3 sentences) · category (the "shelf" customers search on) · price point · core benefit (the ONE thing).

## 2. Buyer Persona(s)  (1–2)
Archetype · demographics & daily reality · trigger event (the moment they start looking) ·
pains (surface / deeper / 2am-core) · desires (functional / emotional / identity) ·
top 3 objections + the hidden fear behind each.

## 3. Voice-of-Customer Language Bank
10 problem phrases + 8 desire phrases in the customer's exact words ([REAL QUOTE] / [INFERRED]) ·
words that repel them.

## 4. Positioning / USP
The one differentiator + how to frame it vs. alternatives.

## 5. Offer & Proof
Current offer/promo · reviews, ratings, results, awards, press.

## 6. Awareness Map
For each of the 5 problem awareness levels, capture how THIS brand's buyer shows up at that level:
what they're thinking, the exact phrase in their head, and the one message that lands.
1) Unaware  2) Problem-Aware  3) Solution-Aware  4) Product-Aware  5) Most Aware
Then: which level the brand is currently over-serving (almost always 4 and 5), and which is the biggest gap.

## 7. Awareness x Concept Map
For each of the 8 DAS static ad concepts, mark ✅ / ⚠️ / skip, the specific angle for THIS brand,
AND the awareness level(s) that angle is aimed at:
1) Before & After  2) Us vs. Them  3) Social Proof  4) USP / Core Benefit
5) Lo-Fi Social Proof  6) Product Showcase  7) Deals / FOMO  8) Meme / Humor / BTS
Then: Top 3 concepts to test first, each tagged with its awareness level.

## 8. Brand Voice & Guardrails
Tone · language · anything the ads should NOT say.
```

Every detail must be specific enough to write an ad from. Generic personas are useless — "I need better ROI" is noise; "I just fired my third media buyer and I'm back to doing it myself" is gold.

---

## DAS Meta ads fundamentals (shared knowledge for all skills)

**A great static ad is structured communication, not a pretty picture.** It usually contains: a Headline (the hook), a Subheadline (re-hook/clarification), a clear Visual, supporting Body text, and a CTA. Rule: **see → understand → act.**

**Creative and Meta copy must complement, not duplicate.** The creative = attention + the core idea. The Meta ad unit (primary text, headline, description, CTA) = depth + persuasion + qualification. Never repeat the on-image headline word-for-word in the primary text — go deeper.

**The 8 evergreen concepts** are psychological containers you reuse to scale creative: Before & After, Us vs. Them, Social Proof, USP/Core Benefit, Lo-Fi Social Proof, Product Showcase, Deals/FOMO, Meme/Humor/BTS. See `references/8-evergreen-concepts.md`.

**Awareness decides everything downstream.** Schwartz's 5 levels (Unaware → Problem-Aware → Solution-Aware → Product-Aware → Most Aware) determine which concept fits, which hook type lands, how long the copy runs, what the image looks like, and how hard the CTA pushes. Roughly 70% of any cold audience is Unaware and only ~3% is ready to buy, so a brand running only product and offer ads is talking to 3% of the room. See `references/awareness-levels.md` for the per-level playbook and the awareness x concept matrix. Every spoke skill reads it.

**Strategy first, AI second.** AI writes great copy from great input. Only the user knows their margins, CAC/LTV, and market — which is exactly what this context document captures.

---

## Related Skills
After this context exists, use:
- **das-ad-hook-generator** — generate 32 scroll-stopping hooks, tagged by awareness level.
- **das-ad-copy-generator** — generate ready-to-paste ad copy for any of the 8 concepts.
- **das-ad-design-brief** — turn a concept + copy kit into a layout blueprint and shot list so a non-designer can build the image.
- **das-static-ad-scorer** — score a finished ad image before you spend.

---
*Powered by Digital Ad Snack. More Meta ads insights → https://digitaladsnack.com*
