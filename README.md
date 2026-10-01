# Digital Ad Snack: AI Tools for Meta Ads

**Free, open AI agent skills that help you research, write, and pressure-test Meta (Facebook & Instagram) ads, built by a media buyer who's managed €500k+ in ad spend.**

Built by [Frici Barabas](https://digitaladsnack.com), writer of **[Digital Ad Snack](https://digitaladsnack.com)**, the newsletter that turns Meta ads strategy into something you can actually use. Want sharper Meta ads every week? [Subscribe to the newsletter](https://digitaladsnack.com).

These work as installable skills in [Claude Code](https://claude.ai) (and any agent that supports the [Agent Skills spec](https://agentskills.io): Codex, Cursor, Windsurf), **and** as copy-paste prompts in any AI (ChatGPT, Gemini, Claude, Grok). No paid tools required.

## What are Skills?

Skills are markdown files that give an AI agent specialized knowledge and workflows for a task. Add them to your setup and the agent recognizes when you're working on a Meta ads task and applies the right frameworks instead of generic advice.

## How Skills Work Together

The `das-meta-ads-context` skill is the **foundation**. Every other skill reads it first to understand your product, audience, Voice-of-Customer, positioning, and how aware your buyers actually are before doing anything. You build it once; every other tool reuses it.

```
                    ┌──────────────────────────────────────────────┐
                    │            das-meta-ads-context              │
                    │      (foundation: read first, always)        │
                    │   product · persona · VoC · positioning      │
                    │  · 5 awareness levels · awareness x concept  │
                    └──────────────────────┬───────────────────────┘
                                           │
        ┌──────────────────┬───────────────┴───────┬──────────────────┐
        ▼                  ▼                       ▼                  ▼
┌───────────────┐  ┌───────────────┐      ┌───────────────┐  ┌───────────────┐
│ das-ad-hook-  │  │ das-ad-copy-  │      │ das-ad-design-│  │ das-static-ad-│
│ generator     │  │ generator     │      │ brief         │  │ scorer        │
├───────────────┤  ├───────────────┤      ├───────────────┤  ├───────────────┤
│ 32 hooks, one │  │ copy kits for │      │ layout, shot  │  │ 26-point      │
│ per awareness │  │ 8 static ad   │      │ list & text   │  │ readiness     │
│ level         │  │ concepts      │      │ placement map │  │ score         │
└───────────────┘  └───────────────┘      └───────────────┘  └───────────────┘

   The natural order, and how they hand off:
     context → hook (pick the angle) → copy (write it) → design (build it) → score (check it)

   Before any of it: das-profit-planner tells you the ROAS the ads have to hit to make money.
```

See each skill's **Related Skills** section for the full map. More skills are added over time.

## Available Skills

| Skill | Description |
|-------|-------------|
| [das-meta-ads-context](skills/das-meta-ads-context/) | **Foundation.** Build a `.agents/das-meta-ads-context.md` for your brand: product, buyer persona, Voice-of-Customer, positioning, the 5 problem awareness levels, and which of the 8 static ad concepts fit at each level. Run this first. |
| [das-ad-hook-generator](skills/das-ad-hook-generator/) | Generate 32 scroll-stopping ad hooks from a product URL across 4 categories, labeled by type **and awareness level**, with a top 5 that gives you one hook per level instead of five aimed at the same buyer. |
| [das-ad-copy-generator](skills/das-ad-copy-generator/) | Generate ready-to-paste Meta ad copy for the 8 evergreen static ad concepts (headlines, subheadlines, body, features/benefits, CTAs), with length, product placement, and CTA pressure set by the awareness level you're targeting. |
| [das-ad-design-brief](skills/das-ad-design-brief/) | Picks **which of the 8 concepts** each ad should be, based on awareness level and the assets you have, then writes a designer-ready brief for each: core message, on-image copy, visual direction, layout, and what to avoid. |
| [das-static-ad-scorer](skills/das-static-ad-scorer/) | Score a static ad image against a 26-point Creative Readiness Scorecard before you spend: element breakdown, total, launch verdict, and the top 3 fixes. |
| [das-profit-planner](skills/das-profit-planner/) | **Before you spend.** Your break-even CPA, the break-even ROAS exactly as Ads Manager will show it (VAT included or not, depending on your pixel, plus Meta's location fees in Austria, France, Italy, Spain, the UK and Turkey), a target ROAS, a monthly budget table, and suggested kill, hold and scale lines. Built for European shops. |

## What each skill does

### 🧭 das-meta-ads-context: *the foundation*
**Your brand brief for Meta ads, built once and reused by every other tool.** Run it first. It interviews you (or reads your product URL), then saves a `.agents/das-meta-ads-context.md` capturing your product, buyer persona, the exact words your customers use (Voice-of-Customer), your positioning, your offer, how your buyer shows up at each of the **5 problem awareness levels**, and which of the 8 static ad concepts fit at each level. Every other skill reads this file first, so your copy, hooks, designs, and scores are grounded in your real audience instead of generic AI guesses, and you never repeat yourself. *Based on the Digital Ad Snack Meta ads research framework.*

### 🎯 The 5 awareness levels (why this matters)
Eugene Schwartz mapped these in 1966 and nothing since has replaced them. They describe how close someone is to buying, and they decide which concept fits, which hook lands, how long the copy runs, what the image looks like, and how hard the CTA pushes.

| Level | Who they are | Share of a cold audience |
|---|---|---|
| **1. Unaware** | Don't know they have a problem | ~70% |
| **2. Problem-Aware** | Feel the itch, haven't named it | ~15% |
| **3. Solution-Aware** | Researching categories of solution | ~10% |
| **4. Product-Aware** | Know you exist, deciding if you're worth it | ~5% |
| **5. Most Aware** | Ready, need a reason to act now | ~3% |

Most brands only ever run level 4 and 5 ads: *here's what we sell* and *here's a discount*. That's 100% of the creative talking to 8% of the audience, and then people blame the algorithm. These skills build for all five.

### ✍️ das-ad-copy-generator
**This copywriter skill creates ready-to-paste copy for the 8 evergreen static ad concepts.** Tell it which concept you want and how many headlines, subheadlines, body texts, features/benefits, and CTAs. It returns a full copy kit in your brand's voice, flagging every line drawn from real customer reviews with ✓VoC (usually the strongest performers). The 8 concepts:

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
**32 scroll-stopping hooks from a single product URL.** The hook is the first line, the one that stops the scroll. This skill generates 32 hooks across 4 categories (Product-, Problem-, Benefit-, and Solution-focused), each labeled by type (Curiosity, Bold Statement, UGC Review, Social Proof, Problem-Agitation, Aspirational…), then ranks the top 5 with a one-line reason each works. Built on the **[Digital Ad Snack 180+ Ad Hook Library →](https://e.pcloud.link/publink/show?code=XZVdkcZe8497V3cqdFkfQOzP7ko2y6jfzrk)**

### 🎨 das-ad-design-brief
**Which of the 8 concepts should this ad be?** That's the hardest call in creative strategy, and every other tool hands it back to you.

Say *"give me 5 ad concepts for people who don't know they have this problem"* and it picks the concepts itself, using your awareness level, your brand's fit map, and the visual assets you actually have. Then it writes a designer-ready brief for each: the concept and why it fits, the awareness level, the core message, the copy that goes on the image, the visual direction, the layout in words, and how that concept fails at that awareness level.

No pixel dimensions, no font sizes, no software tutorials. A brief describes the ad. How it gets made is your designer's job, or the template pack's.

### 📊 das-static-ad-scorer
**Scores your finished ad before you spend a cent.** Upload a static ad image and it grades it against the 8 criteria of a high-converting static ad: Headline/Hook, Subheadline, Additional Copy, Visuals, Offer, CTA, plus the 5-Second Rule and the Scroll Test. You get a total out of 26, a clear launch verdict (13+ = ready to launch, 17+ = strong winner), the top 3 improvements ranked by impact, and one thing it already nails. Built on the **[Digital Ad Snack Meta Static Ads Creative Readiness Scorecard →](https://e.pcloud.link/publink/show?code=XZ0TevZdkYCqSqjvX4RHxHHQvQciz81FYek)**

### 💶 das-profit-planner: *before you spend*
**Know your break-even ROAS before the first euro goes to Meta.** Ads Manager only sees the ad account. It does not know your VAT, your product cost, the courier invoice or the card fees. This skill adds them back in, one line at a time, and gives you the ROAS you need to see *in Ads Manager* to make money. It checks whether your pixel sends prices with or without VAT, because that alone moves the break-even by the whole VAT rate. It also adds what Meta charges European advertisers outside the "Amount Spent" column: the location fee (5% in Austria and Turkey, 3% in France, Italy and Spain, 2% in the UK) and the VAT on Meta's invoice when you can't reclaim it. You also get a target ROAS for the profit you want, a monthly budget table, a check on whether your budget can feed Meta's learning phase, and suggested kill, hold and scale lines. They are a starting point: you know your account, the AI doesn't. VAT per country for shops selling across Europe. *Built on the profit ladder from [Digital Ad Snack #130](https://digitaladsnack.com/p/the-ladder-from-roas-to-profit).*

## Install

### Option 1: One command (recommended)
Uses [`npx skills`](https://github.com/vercel-labs/skills) to install straight into Claude (`~/.claude/skills/`):

```bash
# Install all 6 skills
npx skills add digitaladsnack/digital-ad-snack-ai-tools-for-meta-ads

# Or just the ones you want
npx skills add digitaladsnack/digital-ad-snack-ai-tools-for-meta-ads --skill das-meta-ads-context das-ad-copy-generator

# See what's available
npx skills add digitaladsnack/digital-ad-snack-ai-tools-for-meta-ads --list
```

### Option 2: Claude Code plugin
```
/plugin marketplace add digitaladsnack/digital-ad-snack-ai-tools-for-meta-ads
/plugin install das-meta-ads-skills@digital-ad-snack
```

### Option 3: Manual
```bash
git clone https://github.com/digitaladsnack/digital-ad-snack-ai-tools-for-meta-ads.git
mkdir -p ~/.claude/skills
cp -R digital-ad-snack-ai-tools-for-meta-ads/skills/* ~/.claude/skills/
```

Then just describe what you need: *"set up my meta ads context"*, *"give me ad hooks"*, *"generate meta ad copy for [url]"*, *"design brief for that ad"*, *"score my ad"* (attach the image), or *"what's my break-even ROAS"*. The right skill triggers automatically.

### Option 4: Claude Desktop or Claude web (no terminal)
Works on any paid Claude plan. Nothing to install, no command line.

1. **Download the skills.** On this repo click the green **Code** button → **Download ZIP**, then unzip it. Inside `skills/` you'll find one folder per skill.
2. **Zip each skill folder on its own.** Right-click `das-meta-ads-context` → *Compress* (Mac) or *Send to → Compressed folder* (Windows). Repeat for each skill you want.
   > The zip must contain the **folder**, with `SKILL.md` inside it. Zipping just the `SKILL.md` file will not work.
3. **Turn on code execution.** Claude → **Settings → Capabilities** → enable **Code execution and file creation**.
4. **Upload.** Claude → **Customize** (bottom-left) → **Skills** → **+** → **Upload a skill** → pick your zip. Claude reads the `SKILL.md` and shows you a summary of what it does.
5. **Toggle it on.** Repeat for each skill.

Start with `das-meta-ads-context`, then add the others as you need them. Once they're on, just describe your task in plain language and Claude picks the right skill by itself.

## Use without an agent (any AI, free)

1. Open the skill folder you want → open its `SKILL.md`.
2. Copy the instructions (everything below the frontmatter).
3. Paste into a new chat in ChatGPT, Claude, Gemini, etc., or save them as a [Claude Project](https://claude.ai) instruction.
4. Start with `das-meta-ads-context` to build your brand brief, then use the other skills.

> Skills that have a `references/` folder (context, copy generator, design brief) work best if you paste those files in too, or attach them to the Project.

> The Static Ad Scorer needs an AI that can see images. Upload your ad creative when prompted.

## Quickstart: your first five ads

If you've never used a skill before, do exactly this. It takes an afternoon and produces a full launch batch.

**1. Build your context (once, ~40 min).** Type:
> *"Set up my Meta ads context for [your product URL]"*

Answer the questions. Paste in 3 to 5 real customer reviews if you have them, this single step makes everything downstream better. Approve it when it looks right. You never do this again.

**2. Get your hooks (~10 min).** Type:
> *"Give me ad hooks for my product"*

You get 32, plus a top five with **one hook per awareness level**. Those five are your five ads.

**3. Write the copy (~30 min).** For each of the five, type:
> *"Write the copy for the [concept] ad at [awareness level]"*

**4. Get the design briefs (~15 min).** Type:
> *"Create 5 ad concepts for [who they're for]"*

It picks which of the 8 concepts each ad should be and briefs each one: core message, the copy on the image, the visual, the layout. Hand them to a designer, or build them yourself.

**5. Score before you spend (~10 min).** Upload each finished image:
> *"Score my ad"*

Fix anything below 13 out of 26. Then launch all five in **one campaign, one ad set**.

**A note on what "awareness level" means:** it's how close someone is to buying. Ad 1 is for people who don't know they have a problem, ad 5 is for people ready to buy today. Running all five means you're advertising to the whole audience instead of only the ~8% already shopping. The `das-meta-ads-context` skill explains this and maps it to your brand.

## Who's behind this

I'm **Frici Barabas**, Meta ads agency owner (10+ years, €500k+ managed, €10M+ generated) and writer of **Digital Ad Snack**, read by performance marketers and DTC operators across Europe.

- 📰 **Newsletter:** [digitaladsnack.com](https://digitaladsnack.com)
- 🎨 **200+ High Converting Static Meta Ad Templates** (Canva) + the **180+ Ad Hook Library** and **Creative Readiness Scorecard** → [digitaladsnack.com](https://digitaladsnack.com)

If these tools save you time, [subscribe to the newsletter](https://digitaladsnack.com/subscribe). That's the best thanks.

## License

MIT: free to use, modify, and share. See [LICENSE](./LICENSE).

---

*Keywords: free AI tools for Meta ads · Facebook ad copy generator · Meta ad hook generator · static ad scorecard · Claude skills for marketers · AI ad copywriting · agent skills marketing · Meta ads creative · digitaladsnack.com*
