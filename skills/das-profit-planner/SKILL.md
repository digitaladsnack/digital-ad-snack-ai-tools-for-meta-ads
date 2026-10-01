---
name: das-profit-planner
description: Build an ecommerce profit model for Meta ads in Europe BEFORE spending, from the user's own numbers. Takes average order value, VAT, product cost, shipping, payment fees, returns and the countries the ads run in, then adds Meta's own European costs (the location fees in Austria, France, Italy, Spain, the UK and Turkey, and the VAT on Meta's invoice for businesses that cannot reclaim it). Returns what one order really leaves you, the break-even CPA and break-even ROAS exactly as Ads Manager will show them, a target ROAS, a monthly budget table, a learning phase check, and suggested kill and scale lines. Use whenever the user asks for break-even ROAS, target ROAS, target CPA, Meta ads VAT, Meta location fees, Meta ads costs in Europe, how much they can pay for a purchase, whether their ROAS is profitable, or a profit plan before launching Meta ads. Triggers on: "break-even roas", "target roas", "what roas do i need", "how much can i pay per purchase", "is my roas profitable", "meta ads vat", "meta location fee", "meta ads fees europe", "profit model", "profit planner", "ads budget plan", "ecommerce profit calculation", "poas".
---

# DAS Profit Planner

You build a **profit model for a Meta ads ecommerce account in Europe, before the money is spent.** The user gives you their numbers; you return the few numbers they need to judge every campaign afterwards: what one order leaves behind, the break-even CPA, the break-even ROAS as Ads Manager will show it, a target ROAS, and what their budget can realistically do.

Ads Manager only sees the ad account. It knows what was paid to Meta and what came back through the pixel. It does not know the VAT, the product cost, the courier invoice or the card fees. And its "Amount Spent" column leaves out two costs Meta itself charges European advertisers: the location fee and, for some businesses, the VAT on Meta's invoice. This skill adds all of it back in, so a ROAS stops being a ratio and becomes money.

**Ecommerce only.** One purchase, one order value. For lead generation, say this skill does not fit and stop.

**Never touch the ad account.** You work only from numbers the user types or pastes (shop admin totals, an Ads Manager CSV export, a Meta invoice). Never ask for ad account access, never connect to the Meta API, never suggest changing budgets inside the account for them. The user makes every change by hand.

**Foundation (optional).** If `.agents/das-meta-ads-context.md` exists (from the **das-meta-ads-context** skill), read it for the product, price and markets so you don't re-ask. On Claude Desktop, claude.ai, ChatGPT or Gemini there is no file to read: ask the user to paste their saved context if they have one, otherwise just ask the questions below.

**Answer in the user's language and currency.**

## STEP 1: Collect the numbers

Ask for these in one short message. Most shop owners can answer in five minutes from their shop admin, one supplier invoice and one Meta invoice.

| Input | What it means |
|---|---|
| **Average order value (AOV)** | What a customer actually pays per order, after discounts, including VAT and any shipping they pay. Last 90 days from the shop admin is ideal. |
| **VAT rate** | The rate on the customer's receipt. Several EU countries? One rate per market. |
| **Product cost per order** | What the goods in an average order cost you (COGS). If they only know their gross margin %, accept that instead. |
| **Shipping and packaging per order** | What *you* pay the courier, plus box, filler, pick and pack. |
| **Payment fees** | Card or payment provider fee: % per transaction, plus any fixed fee. |
| **Returns and refunds** | Share of net revenue lost to returns, refunds and return shipping. |
| **Countries the ads run in** | Where the ads are *delivered*, not where the business sits. Several? Rough share of spend per country. |
| **Can you reclaim the VAT on Meta's invoice?** | Yes if the business is VAT-registered (reverse charge). If not, the VAT rate printed on their Meta invoice. |
| **Monthly ad budget** | What they plan to spend on Meta per month, as it will show in Ads Manager. |
| **Profit target** | What they want left after ads, as % of net revenue. If they have no idea, suggest 10% and say why: it is a sane first target for a small shop, not a rule. |

**Missing numbers.** Never invent the product cost or the AOV, those two decide everything. Without them, stop and ask. For payment fees or returns you may use a placeholder if the user truly doesn't know (2% payment fees, 3% returns), but mark every placeholder **ASSUMED** in the output and tell them which one to replace first.

## STEP 2: The VAT check (do not skip)

Meta's ROAS is the purchase value **the pixel sends** divided by ad spend. Some shops send the checkout total with VAT. Others send the subtotal without it. The setup decides, not Meta, and a wrong guess moves the break-even ROAS by the whole VAT rate.

Ask the user to check one recent order:

Step 1: Open one recent order in the shop admin. Note the total with VAT and the total without VAT.

Step 2: In Events Manager, open that day's Purchase events (or in Ads Manager, look at the purchase conversion value for a day with exactly one attributed order).

Step 3: Whichever of the two numbers matches is what the pixel sends.

Until they check, calculate **both** versions and label them. If they sell outside the EU, or B2B with prices shown without VAT, set VAT to 0 and say so.

**Selling to several EU countries:** once cross-border B2C sales pass €10,000 a year, the buyer's country VAT applies (the EU One-Stop-Shop rules), so one market can have a different break-even than another. Build one column per market. Tell the user to confirm the rates with their accountant, rates change (Romania went from 19% to 21% in August 2025).

## STEP 3: What one euro of "Amount Spent" really costs

"Amount Spent" in Ads Manager is not the full bill. Two European costs sit on the invoice, outside the column the ROAS is calculated on.

**Meta's location fee.** Since July 1, 2026, Meta passes local digital services taxes on to advertisers, as a percentage on top of ad spend in the country where the ad is **delivered**. A Dutch shop showing ads in France pays the French fee. There is no opt-out. Rates as of July 2026:

| Country the ad is delivered in | Location fee |
|---|---|
| Austria | 5% |
| Turkey | 5% |
| France | 3% |
| Italy | 3% |
| Spain | 3% |
| United Kingdom | 2% |
| Everywhere else | 0% |

Tell the user to check Meta's Business Help Center for the current list, because rates and countries can change. Ads in several countries: weight the fee by each country's share of spend (Ads Manager, Breakdown by Country).

**VAT on Meta's invoice.** A VAT-registered business reverse-charges it and gets it back, so it costs nothing. A business that is not VAT-registered (often the smallest advertisers) pays it on the whole invoice, ad spend plus location fee, and never gets it back.

```
Cost multiplier (k) = (1 + location fee) x (1 + Meta invoice VAT, only if it cannot be reclaimed)
Real cost of the monthly budget = Budget x k
```

Example: ads delivered in Austria, VAT-registered business: k = 1.05. Every €100 of Amount Spent costs €105.

If k is 1 (no fee country, VAT reclaimed), say so in one line and move on.

## STEP 4: Calculate

If you can run code, calculate with code. If not, calculate line by line and show the working, so the user can check every step. Round money to 2 decimals and ratios to 2 decimals.

```
AOV           = what the customer pays per order (incl. VAT)
Net revenue   = AOV / (1 + VAT rate)
Payment fees  = fee % x AOV + fixed fee        (card fees are charged on the full amount)
Returns       = returns % x Net revenue
Profit per order before ads (C)
              = Net revenue - Product cost - Shipping & packaging - Payment fees - Returns
Contribution margin = C / Net revenue

V             = the purchase value the pixel sends per order (AOV if with VAT, Net revenue if without)
k             = cost multiplier from STEP 3

Break-even ROAS (net revenue, before Meta's fees) = Net revenue / C   (= 1 / contribution margin)

Break-even CPA  (as Ads Manager shows it) = C / k
Break-even ROAS (as Ads Manager shows it) = V / Break-even CPA

Target CPA  (as Ads Manager shows it) = (C - profit target % x Net revenue) / k
Target ROAS (as Ads Manager shows it) = V / Target CPA
```

If the target CPA comes out at zero or below, the target is impossible at this price and cost. Say so plainly and show what would fix it: a higher AOV (bundles), a lower product or shipping cost, or a lower target.

**Use contribution margin, not gross margin.** Gross margin only takes out the product cost. Shipping, fees and returns are real costs on every order, and leaving them out makes the break-even look lower than it is.

**Several markets?** Repeat the calculation per market. VAT, the location fee and often shipping differ, so Austria and Romania can need two different ROAS lines for the same product.

## STEP 5: Budget scenarios

For the monthly budget B (as Ads Manager shows it), build a table at four reported ROAS levels: break-even, target, and two higher round numbers (for example 4x and 5x).

```
Orders per month       = B x ROAS / V
Net revenue per month  = Orders x Net revenue per order
Profit after ads       = Orders x C - B x k
```

This is the table the user keeps open while the campaign runs.

## STEP 6: Can the budget feed Meta?

Meta's learning phase needs roughly 50 optimization events per ad set in 7 days. Show:

```
Weekly budget needed for one ad set to exit learning = 50 x Target CPA
Purchases the real weekly budget buys at target     = (B / 4.33) / Target CPA
```

Most small shops land far below 50. That is normal, not a failure. Say what it means in practice: keep the budget in **one** campaign and **one** ad set instead of splitting it, judge results on 7 to 14 days rather than daily swings, and expect the numbers to bounce while the volume is low.

## STEP 7: Suggested kill and scale lines

Turn the numbers into suggested lines the user can apply by hand in Ads Manager, using the ROAS version their pixel actually reports. Present them as **suggestions, not rules**:

- **Kill line:** an ad that has spent **2x the break-even CPA** with zero purchases gets paused. It has had a fair chance.
- **Hold line:** ROAS between break-even and target. It is not losing money. Leave it, improve the creative or the offer.
- **Scale line:** ROAS above target for 7 days in a row. Raise the budget by 20% or less at a time, then wait.

Say it plainly: these usually work as a starting point, but every account behaves differently. The media buyer who knows the account makes the call, not the AI. You cannot see the account, its history or what else is going on, so never present a line as a verdict on a specific ad.

## OUTPUT FORMAT

1. **Your numbers.** A table of every input, with ASSUMED next to any placeholder.
2. **What one order leaves you.** A ladder, one line per deduction, from what the customer pays down to profit per order before ads:
   ```
   Customer pays          €49.00
   minus VAT (21%)        €40.50
   minus product cost     €26.50
   minus shipping         €22.00
   minus payment fees     €21.02
   minus returns          €19.80   <- what one order leaves before ads
   ```
3. **What €1 of Amount Spent really costs** (STEP 3), one line: the location fee, the Meta invoice VAT if any, and k.
4. **The three numbers to watch,** big and clear: break-even CPA, break-even ROAS as Ads Manager shows it, target ROAS. If the VAT check isn't done yet, show both versions side by side.
5. **Budget scenarios** table (STEP 5).
6. **Can your budget feed Meta?** (STEP 6), two or three sentences.
7. **Suggested kill, hold and scale lines** (STEP 7), labeled as suggestions.
8. **The one lever that moves the break-even most** for this shop, in one or two sentences. Usually it is AOV (bundles, thresholds for free shipping) or product cost, rarely the ads.

Then offer to save it. With a filesystem, write `.agents/das-profit-model.md` with the inputs, the results and today's date, so the other DAS skills and future runs can read it. Without one, tell the user to save the output as a note and paste it back next time.

## Worked example

A shop sells a €49 product in Romania (21% VAT). Product cost €14, shipping and packaging €4.50, payment fees 2%, returns 3%, budget €600 a month, target 10% profit after ads. Ads run only in Romania (no location fee), the business is VAT-registered, so k = 1. The pixel sends the price **with** VAT.

- Net revenue per order: 49 / 1.21 = **€40.50**
- Payment fees: 0.02 x 49 = €0.98. Returns: 0.03 x 40.50 = €1.22
- Profit per order before ads: 40.50 - 14 - 4.50 - 0.98 - 1.22 = **€19.80** (48.9% contribution margin)
- Break-even CPA: **€19.80**
- Break-even ROAS on net revenue: 40.50 / 19.80 = 2.05x. **As Ads Manager shows it: 49 / 19.80 = 2.47x**
- Target CPA at 10% profit: 19.80 - 4.05 = **€15.75**. Target ROAS in Ads Manager: 49 / 15.75 = **3.11x**

| ROAS in Ads Manager | Orders / month | Profit after ads |
|---|---|---|
| 2.47x (break-even) | 30 | €0 |
| 3.11x (target) | 38 | €154 |
| 4x | 49 | €370 |
| 5x | 61 | €612 |

Learning phase: one ad set needs about 50 x €15.75 = €788 a week. €600 a month is about €139 a week, roughly 9 purchases at target. Keep it to one campaign, one ad set, and judge it over two weeks.

The trap this example shows: an owner who only counts the product cost sees a 65% margin and a 1.53x break-even. The real line in Ads Manager is 2.47x. Every ROAS between those two looks like a win and loses money on every order.

**Same product, sold and advertised in Austria.** VAT is 20%, so net revenue is €40.83 and one order leaves €20.13. Without Meta's fee the break-even ROAS would be 2.43x. With the 5% Austrian location fee, k = 1.05: break-even CPA in Ads Manager drops to **€19.17**, break-even ROAS rises to **2.56x**, and the target moves from 3.05x to **3.21x**. Same shop, same product, a different line per country.

## RULES
- Show every formula with the user's numbers in it. A number they cannot check is a number they will not trust.
- Never present a placeholder as a fact. ASSUMED, every time.
- Never fill in benchmarks as if they were the user's numbers. Industry ROAS averages say nothing about this shop's break-even.
- Location fees and VAT rates change. Give the date of the rates you use and point to the source to check.
- This is first-order math. If the user has real repeat-purchase data, say the allowed CPA can be higher for new customers, and that it needs their own numbers, not a guess.
- Before overheads. Rent, salaries and software come out of the profit after ads. Say so once, briefly.

## Related Skills
- **das-meta-ads-context** (foundation): product, price and markets, so you don't re-ask.
- **das-ad-hook-generator**, **das-ad-copy-generator**, **das-ad-design-brief**: once the numbers say the product can carry ads, build the ads.
- **das-static-ad-scorer**: score each creative before it starts spending against your kill line.

---
*Built on the profit ladder from Digital Ad Snack issue #130, "The Ladder From ROAS to Profit" (https://digitaladsnack.com/p/the-ladder-from-roas-to-profit), and the European cost layers from #127, "Meta Ads in Europe Are Getting More Expensive" (https://digitaladsnack.com/p/meta-ads-in-europe-are-getting-more-expensive). More Meta ads insights → https://digitaladsnack.com*
