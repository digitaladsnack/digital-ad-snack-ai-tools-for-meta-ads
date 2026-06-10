# Digital Ad Snack — AI Tools for Meta Ads

**Free, open AI agent skills that help you research, write, and pressure-test Meta (Facebook & Instagram) ads — built by a media buyer who's managed €500k+ in ad spend.**

Built by [Frici Barabas](https://digitaladsnack.com), writer of **[Digital Ad Snack](https://digitaladsnack.com)** — the newsletter that turns Meta ads strategy into something you can actually use. Want sharper Meta ads every week? [Subscribe to the newsletter](https://digitaladsnack.com).

These work as installable skills in [Claude Code](https://claude.ai) (and any agent that supports the [Agent Skills spec](https://agentskills.io) — Codex, Cursor, Windsurf), **and** as copy-paste prompts in any AI (ChatGPT, Gemini, Claude, Grok). No paid tools required.

## What are Skills?

Skills are markdown files that give an AI agent specialized knowledge and workflows for a task. Add them to your setup and the agent recognizes when you're working on a Meta ads task and applies the right frameworks — instead of generic advice.

## How Skills Work Together

The `das-meta-ads-context` skill is the **foundation** — every other skill reads it first to understand your product, audience, Voice-of-Customer, and positioning before doing anything. You build it once; every other tool reuses it.

```
                          ┌────────────────────────────────────────┐
                          │            das-meta-ads-context             │
                          │     (foundation — read first, always)   │
                          │  product · persona · VoC · positioning  │
                          │         · 8-concept fit map             │
                          └─────────────────────┬──────────────────-┘
                                                │
                ┌───────────────────────────────┼───────────────────────────────┐
                ▼                                ▼                                ▼
      ┌───────────────────┐          ┌───────────────────┐          ┌───────────────────┐
      │ das-ad-copy-      │          │ das-ad-hook-      │          │ das-static-ad-    │
      │ generator         │          │ generator         │          │ scorer            │
      ├───────────────────┤          ├───────────────────┤          ├───────────────────┤
      │ ready-to-paste    │          │ 32 scroll-stopping│          │ 26-point creative │
      │ copy for 8 static │          │ hooks across 4    │          │ readiness score   │
      │ ad concepts       │          │ categories        │          │ for a finished ad │
      └───────────────────┘          └───────────────────┘          └───────────────────┘

   Skills cross-reference each other:
     das-meta-ads-context → ad-copy-generator → static-ad-scorer
     ad-hook-generator → ad-copy-generator (hooks become headlines)
```

See each skill's **Related Skills** section for the full map. More skills are added over time.

## Available Skills

| Skill | Description |
|-------|-------------|
| [das-meta-ads-context](skills/das-meta-ads-context/) | **Foundation.** Build a `.agents/das-meta-ads-context.md` for your brand — product, buyer persona, Voice-of-Customer, positioning, and which of the 8 static ad concepts fit. Run this first. |
| [das-ad-copy-generator](skills/das-ad-copy-generator/) | Generate ready-to-paste Meta ad copy for the 8 evergreen static ad concepts — headlines, subheadlines, body, features/benefits, CTAs — grounded in your context. |
| [das-ad-hook-generator](skills/das-ad-hook-generator/) | Generate 32 scroll-stopping ad hooks from a product URL across 4 categories, labeled by type, with the top 5 ranked and explained. |
| [das-static-ad-scorer](skills/das-static-ad-scorer/) | Score a static ad image against a 26-point Creative Readiness Scorecard before you spend — element breakdown, total, launch verdict, and the top 3 fixes. |

## What each skill does

### 🧭 das-meta-ads-context — *the foundation*
**Your brand brief for Meta ads, built once and reused by every other tool.** Run it first. It interviews you (or reads your product URL), then saves a `.agents/das-meta-ads-context.md` capturing your product, buyer persona, the exact words your customers use (Voice-of-Customer), your positioning, your offer, and which of the 8 static ad concepts fit you best. Every other skill reads this file first — so your copy, hooks, and scores are grounded in your real audience instead of generic AI guesses, and you never repeat yourself. *Based on the Digital Ad Snack Meta ads research framework.*

### ✍️ das-ad-copy-generator
**This copywriter skill creates ready-to-paste copy for the 8 evergreen static ad concepts.** Tell it which concept you want and how many headlines, subheadlines, body texts, features/benefits, and CTAs — it returns a full copy kit in your brand's voice, flagging every line drawn from real customer reviews with ✓VoC (usually the strongest performers). The 8 concepts:

1. **Before & After / Transformation**
2. **Us vs. Them (Comparison)**
3. **Social Proof (Testimonials, Reviews, Ratings)**
4. **USP / Core Benefit / Feature-Led**
5. **Lo-Fi Social Proof (UGC, PR, Comments, Screenshots)**
6. **Product Showcase / Collage**
7. **Deals / Promotions / FOMO**
8. **Meme / Humor / Trends / Behind-the-Scenes**

Built to pair with the Canva templates it's based on → **[200+ High Converting Static Meta Ad Templates](https://digitaladsnack.com/high-converting-meta-ad-templates)**. Generate the copy here, paste it straight into the matching template.

### 🪝 das-ad-hook-generator
**32 scroll-stopping hooks from a single product URL.** The hook is the first line — the one that stops the scroll. This skill generates 32 hooks across 4 categories (Product-, Problem-, Benefit-, and Solution-focused), each labeled by type (Curiosity, Bold Statement, UGC Review, Social Proof, Problem-Agitation, Aspirational…), then ranks the top 5 with a one-line reason each works. Built on the **[Digital Ad Snack 180+ Ad Hook Library →](https://e.pcloud.link/publink/show?code=XZVdkcZe8497V3cqdFkfQOzP7ko2y6jfzrk)**

### 📊 das-static-ad-scorer
**Scores your finished ad before you spend a cent.** Upload a static ad image and it grades it against the 8 criteria of a high-converting static ad — Headline/Hook, Subheadline, Additional Copy, Visuals, Offer, CTA, plus the 5-Second Rule and the Scroll Test — for a total out of 26, a clear launch verdict (13+ = ready to launch, 17+ = strong winner), the top 3 improvements ranked by impact, and one thing it already nails. Built on the **[Digital Ad Snack Meta Static Ads Creative Readiness Scorecard →](https://e.pcloud.link/publink/show?code=XZ0TevZdkYCqSqjvX4RHxHHQvQciz81FYek)**

## Install — Claude Code (plugin marketplace)

```
/plugin marketplace add digitaladsnack/digital-ad-snack-ai-tools-for-meta-ads
/plugin install das-meta-ads-skills@digital-ad-snack
```

Or install manually (Claude Code / Claude Desktop / any Agent Skills agent):

```bash
git clone https://github.com/digitaladsnack/digital-ad-snack-ai-tools-for-meta-ads.git
mkdir -p ~/.claude/skills
cp -R digital-ad-snack-ai-tools-for-meta-ads/skills/* ~/.claude/skills/
```

Then just describe what you need — *"set up my meta ads context"*, *"generate meta ad copy for [url]"*, *"give me ad hooks"*, or *"score my ad"* (attach the image). The right skill triggers automatically.

## Use without an agent (any AI — free)

1. Open the skill folder you want → open its `SKILL.md`.
2. Copy the instructions (everything below the frontmatter).
3. Paste into a new chat in ChatGPT, Claude, Gemini, etc. — or save them as a [Claude Project](https://claude.ai) instruction.
4. Start with `das-meta-ads-context` to build your brand brief, then use the other skills.

> The Static Ad Scorer needs an AI that can see images — upload your ad creative when prompted.

## Who's behind this

I'm **Frici Barabas** — Meta ads agency owner (10+ years, €500k+ managed, €3M+ generated) and writer of **Digital Ad Snack**, read by performance marketers and DTC operators across Europe.

- 📰 **Newsletter:** [digitaladsnack.com](https://digitaladsnack.com)
- 🎨 **200+ High Converting Static Meta Ad Templates** (Canva) + the **180+ Ad Hook Library** and **Creative Readiness Scorecard** → [digitaladsnack.com](https://digitaladsnack.com)

If these tools save you time, [subscribe to the newsletter](https://digitaladsnack.com) — that's the best thanks.

## License

MIT — free to use, modify, and share. See [LICENSE](./LICENSE).

---

*Keywords: free AI tools for Meta ads · Facebook ad copy generator · Meta ad hook generator · static ad scorecard · Claude skills for marketers · AI ad copywriting · agent skills marketing · Meta ads creative · digitaladsnack.com*
