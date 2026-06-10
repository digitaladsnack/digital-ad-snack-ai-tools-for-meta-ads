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

## What each skill does (in plain English)

### 🧭 das-meta-ads-context — *the foundation*
**Your brand brief for Meta ads, built once and reused by every other tool.** Run it first. It interviews you (or reads your product URL), then saves a `.agents/das-meta-ads-context.md` with your product, buyer persona, the exact words your customers use (Voice-of-Customer), your positioning, and which of the 8 static ad concepts fit you. Every other skill reads it first — so you never repeat yourself. *Based on the DAS Meta ads research framework.*

### ✍️ das-ad-copy-generator
**Ready-to-paste ad copy for the 8 evergreen static ad concepts.** Pick a concept (Before & After, Us vs. Them, Social Proof, USP, Lo-Fi Social Proof, Product Showcase, Deals/FOMO, Meme) and how many headlines, subheadlines, body texts, and CTAs you want — it generates a copy kit in your brand's voice and flags every line built from real customer reviews with ✓VoC. *Based on the DAS 200+ High Converting Static Meta Ad Templates pack.*

### 🪝 das-ad-hook-generator
**32 scroll-stopping hooks from a single product URL.** Generates hooks across 4 categories (Product, Problem, Benefit, Solution), each labeled by type (Curiosity, Bold Statement, UGC Review, Social Proof…), with the top 5 ranked and a one-line reason each works. *Based on the DAS 180+ Ad Hook Library.*

### 📊 das-static-ad-scorer
**Scores your finished ad before you spend a cent.** Upload a static ad image and it grades it on the 8 criteria of a great static ad — Headline, Subheadline, Copy, Visuals, Offer, CTA, plus the 5-Second Rule and the Scroll Test — out of 26 points, with a launch verdict (13+ = ready, 17+ = winner), the top 3 fixes, and one thing it nails. *Based on the DAS Meta Static Ads Creative Readiness Scorecard.*

## Install — Claude Code (plugin marketplace)

```
/plugin marketplace add YOUR-USERNAME/digital-ad-snack-ai-tools-for-meta-ads
/plugin install das-meta-ads-skills@digital-ad-snack
```

Or install manually (Claude Code / Claude Desktop / any Agent Skills agent):

```bash
git clone https://github.com/YOUR-USERNAME/digital-ad-snack-ai-tools-for-meta-ads.git
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
