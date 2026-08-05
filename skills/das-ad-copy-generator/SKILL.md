---
name: das-ad-copy-generator
description: Generate high-converting Meta ad copy from a product/brand URL, structured around the 8 evergreen static ad concepts in the Digital Ad Snack template pack. A 2-step flow — Step 1 builds a Meta Ads Executive Summary (audience, buyer persona, Voice-of-Customer, positioning, 8-concept fit map) which the user reviews, approves, and saves; Step 2 asks which of the 8 concepts and how many of each element (headlines, subheadlines, body, features/benefits, reviews, CTAs), then generates a ready-to-paste copy kit the user drops into the Canva template by hand. Pure text — works on any free AI account, no paid tools. Use whenever the user wants Meta/Facebook ad copy from a URL, a buyer persona / audience summary for ads, or headlines/subheadlines/body/features for any of the 8 ad concepts. Triggers on: "ad copy generator", "generate meta ad copy", "ad copy from url", "before/after copy", "write meta ads for [url]", "executive summary for my ads", "headlines for my ad".
---

# DAS Ad Copy Generator

Generate Meta ad copy grounded in real audience research, structured around the **8 evergreen static ad concepts** from the Digital Ad Snack template pack. This composes existing DAS skills — `audience-research` (personas + Voice-of-Customer), `hook-writer` (hook formulas), `ad-copy-engine` and `ad-brief-generator` (copy structure). Reuse their logic; don't reinvent it.

**Pure copy — no paid tools.** Output is text the user pastes into their Canva template manually. Works on any AI account. **The brand voice is the USER's brand**, derived from their URL and answers — never hardcode Digital Ad Snack's voice.

**Foundation first.** Read `.agents/das-meta-ads-context.md` (created by the **das-meta-ads-context** skill) for the brand's product, persona, Voice-of-Customer, positioning, Awareness Map, and awareness x concept map. If it doesn't exist, run `das-meta-ads-context` first — or build it inline via Step 1 below, which produces the same document.

**Awareness sets the depth.** The same concept written for an Unaware reader and a Most Aware reader are different ads. Before generating, read `das-meta-ads-context/references/awareness-levels.md` and let the target level decide copy length, how early the product appears, and how hard the CTA pushes:

| Level | Primary text | Product appears | CTA |
|---|---|---|---|
| L1 Unaware | 1–3 lines | not at all, or last | soft or none |
| L2 Problem-Aware | medium | late, almost an aside | cool |
| L3 Solution-Aware | long, they will read | mid, as the category answer | warm |
| L4 Product-Aware | medium | first line | hot |
| L5 Most Aware | 2–4 lines | first line, with the offer | hottest |

---

## How it works — say this up front

> "This works in 2 steps.
> **Step 1 — Executive Summary:** I research your brand from a URL (or details you paste) and build a Meta Ads Executive Summary — who your buyer is, the words they use, your positioning, and which of the 8 ad concepts fit you best. You review and tweak it, then we save it.
> **Step 2 — Copy:** anytime after, tell me which of the 8 concepts you want and how many of each element (headlines, subheadlines, etc.), and I generate a copy kit you paste into your Canva template."

**Routing:**
- No `.agents/das-meta-ads-context.md` / no saved summary, or user gives a URL/brand for the first time → **Step 1** (this builds the same context the `das-meta-ads-context` foundation skill creates).
- Context already exists (the `.agents/das-meta-ads-context.md` file, or the user pastes a summary) → skip to **Step 2**.

---

## STEP 1 — Build the Meta Ads Executive Summary

1. Tell the user you're starting Step 1. Ask this batched set in one message:
   - **Product/brand URL** *(or, if your AI can't open links, paste the product page text / describe the product in a few sentences)*
   - What you sell + price point
   - Main goal / KPI (sales, leads, traffic, retargeting)
   - Anything you already know about your buyer
   - Any real reviews/testimonials I can mine for language (paste a few)
   - Brand voice/tone, and anything I should NOT say
   - **Language** the ads should be written in (default: the language of the product page)

2. Read the URL if possible (WebFetch / browsing). Extract: product name & category, core benefit (the ONE thing), top 3 pains, proof points, USP/mechanism, price.

3. Produce the **Executive Summary**:

```
# META ADS EXECUTIVE SUMMARY — [Brand / Product]

## Product Snapshot
[1 paragraph: what it is, core benefit, price, proof]

## Buyer Persona(s)   (1–2, kept tight)
- Name + archetype
- Demographics & daily reality
- Trigger event (the moment they start looking)
- Pain points: surface / deeper / 2am-core
- Desire: functional / emotional / identity
- Top 3 objections (+ hidden fear behind each)

## Voice-of-Customer Language Bank
- Problem phrases (10): "[exact words]"  [REAL QUOTE] or [INFERRED]
- Desire phrases (8): "[exact words]"
- Words that repel them

## Positioning / USP
[The one differentiator + how to frame it]

## 8-Concept Fit Map
1. Before & After — ✅/⚠️/skip — [the specific angle for THIS brand]
2. Us vs. Them — ...
3. Social Proof — ...
4. USP / Core Benefit — ...
5. Lo-Fi Social Proof — ...
6. Product Showcase — ...
7. Deals / FOMO — ...
8. Meme / Humor / BTS — ...

## Top 3 Concepts to Test First
[ranked, 1 line each on why]
```

Rules: every detail specific enough to write an ad from. Mark sourced quotes `[REAL QUOTE]`, inferred language `[INFERRED]`. Pains must be emotional and concrete, not "needs better ROI."

4. **Review & revise loop**: explicitly ask *"Want to change anything — audience, positioning, tone, any concept's angle? Tell me what to adjust, or say 'approved' and I'll save it."* Revise until the user approves.

5. **Save on approval**: confirm a brand slug, then write the approved summary to `summaries/<brand-slug>.md` inside this skill folder (or a path the user names). Tell the user where it's saved (customer version: paste it into Claude Project knowledge or keep it as their own `.md`).

6. Confirm: *"✅ Step 1 done & saved. Whenever you're ready, tell me which of the 8 concepts you want copy for (Step 2)."*

---

## STEP 2 — Generate the copy kit

1. Load the saved Executive Summary (from `summaries/<brand-slug>.md`, or one the user pasted). If none exists, run Step 1 first.

2. **Ask which concept and which awareness level** (if not stated): list the 8 and note which the fit map recommends, each with the level it's aimed at. Default to Before & After at L3 Solution-Aware if the user just says "go".

   If the user asks for a concept at a level the matrix marks `skip` (for example Deals/FOMO at L1 Unaware), build it anyway but open with one line naming the mismatch and what it will cost them: *"Heads up: a discount ad shown to people who don't know they have this problem gets scrolled past. This copy works, but it belongs on a warm audience. Want an L1 version too?"* State it once, then get on with the work.

3. **Ask how many of each element.** Open `references/concept-copy-frameworks.md`, find that concept's element list, and ask the user for quantities — offer sensible defaults so they can just say "defaults". Example for Before & After:
   > "How many of each do you want? (or say 'defaults')
   > • Headlines (default 10) • Subheadlines (default 6) • Before/After label pairs (default 6) • Proof stats (default 5) • Primary text variations (default 3) • CTA button options (default 6)"
   Always include the **Meta ad-unit elements** (Primary text, Headline, Description, CTA) in the quantity ask. For concepts with reviews (Social Proof) or bullets (USP), ask how many review lines / feature→benefit bullets.

4. **Generate the copy kit** — a menu the user mixes into their template, grouped by element, numbered, using the brand's Voice-of-Customer language and the concept's angle from the fit map.
   - **Flag VoC-grounded options.** Append ` ✓VoC` to any option that uses a phrase from the summary's `[REAL QUOTE]` bank (real customer language from pasted reviews). Leave inferred options unmarked. This shows the user at a glance which lines are backed by real reviews — usually the strongest performers.
   - If the summary had **no real reviews** (everything `[INFERRED]`), skip the per-line marks and add one line at the top: *"⚠️ No real reviews were provided — this copy uses inferred language. Paste a few real reviews and regenerate for ✓VoC-grounded copy that converts harder."*

   Output shape:

```
# [CONCEPT] COPY KIT — [Product]   ([language])
Angle: [from the fit map]
Awareness level: [L1–L5] — [what this reader already knows, 1 line]

## ON-IMAGE ELEMENTS (paste into the Canva template)
### Headlines (×N)
1. ... ✓VoC          ← mark options built from real [REAL QUOTE] customer language
2. ...                (unmarked = inferred)
### Subheadlines (×N)
1. ...
### [other concept-specific elements ×N: before/after labels, proof stats, review lines, feature→benefit bullets, badges, offer lines, etc.]
### CTA button options (×N)
1. ...

## META AD UNIT (the text next to the image)
### Primary text (×N)   [100–250 words each; hook-first; don't repeat the on-image headline]
1. ...
### Meta headlines (×N)   [≤40 char]
### Descriptions (×N)   [≤90 char]
```

5. Close with: *"Mix and match these into your template. Want another concept, or more of any element?"* If the user has now generated copy for two or more concepts at the same awareness level, point it out and suggest the level they're missing.

6. Hand off to design: *"Want the layout too? Run **das-ad-design-brief** with this copy kit and I'll tell you exactly where each line goes and what image you need."*

---

## Rules
- Specific always beats generic. Real customer language > marketing speak. Numbers > vague claims.
- One key message per piece. Hook-first — if the first line is weak, the ad is dead.
- Never leave `[brackets]` unfilled. Write in the user's chosen language.
- Creative (on-image) and Meta copy must complement, not duplicate each other.
- The output's brand voice = the user's brand, not DAS.

## Related Skills
- **das-meta-ads-context** (foundation) — run first; provides the persona, Voice-of-Customer, Awareness Map, and awareness x concept map this skill relies on.
- **das-ad-hook-generator** — turn the chosen angle into 32 hook variations, tagged by awareness level.
- **das-ad-design-brief** — turn this copy kit into a layout blueprint + shot list so a non-designer can build the image.
- **das-static-ad-scorer** — score the finished ad image before you spend.

---
*Powered by Digital Ad Snack. More Meta ads insights → https://digitaladsnack.com*
