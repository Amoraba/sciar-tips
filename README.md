# Sciar Tips · CA2 (H9LOCHFFT)

- **Live site (GitHub Pages):** https://amoraba.github.io/sciar-tips/
- **Repository:** https://github.com/Amoraba/sciar-tips
- **Staff view (the product):** https://amoraba.github.io/sciar-tips/app.html

**My question:** When a kitchen porter can see the hours that earned him no tips, and can raise it without going through his manager, does the silence behind "nobody has ever complained" break?

> Sciar, Halloran's and everyone in them are fictional, invented for teaching. Staff view: [app.html](https://amoraba.github.io/sciar-tips/app.html) · Landing page: [index.html](https://amoraba.github.io/sciar-tips/)

## Part 1: The people

**Internal: Aoife Rennick (CEO, Sciar).** She needs an alpha that works for staff on the devices they have: "Make it work on a phone. Nearly all restaurant staff only have phones." (04-aoife.md)

**External: Rafael (kitchen porter, Halloran's).** He needs to understand his pay and ask without being exposed: "i dont understand how they count it" and "please dont say it was me who ask" (01-rafael.md).

**Accessibility and culture:** Rafael writes in a second language on a damaged phone: "sorry for my english" and "my phone screen is broken so i cannot read the page good" (01-rafael.md). So the staff view uses large plain-English text, a Portuguese toggle and no long links.

## Part 4a: Theory behind the build

**Leadership: transactional leadership (Burns, 1978).** Declan runs the tip split as a top-down exchange of fixed rules for rewards. He says "They don't need the formula, they need the money" and "the kitchen porters are on the kitchen rate and they know that" (02-declan.md). The theory explains why the rule is owner-set and hidden. It misses how staff judge fairness. Rafael took on Mehmet's late shifts, yet his pay is "same like before, almost same" (01-rafael.md). From week 9, about 20 of his weekly hours fell after 23:00 and earned nothing (payouts.csv, staff_id = S12).

**Culture: organisational silence (Morrison and Milliken, 2000) and psychological safety (Edmondson, 1999).** Niamh writes "Nobody has ever complained about the split" (03-niamh.md). Yet Rafael did ask her in September and was told "is the system, is fair for everybody", and he now pleads "please dont say it was me who ask" (01-rafael.md). Silence is being read as agreement.

**Design choice:** because the manager is the only channel ("If someone has a problem they come to me", 03-niamh.md), the concern feature is private to the person who raises it and is not routed through Niamh or Declan.

**Competitive advantage:** owner control wins the paying customer. But a tips product that staff distrust will be blamed in the first pay dispute, so staff trust is what protects Sciar's reputation with every later restaurant (inferred).

**Limit:** both theories come from larger organisations, and five messages cannot show a whole culture. Transactional leadership also misses personal dependence: Declan is "good to me with my visa letter" (01-rafael.md).

## Part 4b: Decision record

**Decision 1 (request changed): Aoife (04-aoife.md) and Niamh (03-niamh.md) asked me to drop "raise a concern".**
- *Options:* remove it, send concerns to Niamh, or keep a private feature.
- *Criteria:* the least powerful user must be able to speak; Rafael's fear of being identified; owner and investor confidence.
- *What decided it:* Rafael already asked Niamh and was dismissed, so routing concerns through her would repeat the silence. I kept the feature but made it private.
- *Underlying need:* Aoife fears "owners will run a mile". The build still serves her: there is no public "moaning wall", nothing is sent to the owner, and the alpha stores concerns only on the user's phone.
- *What would change my mind:* owners in a further pilot leaving because of the feature, or Halloran's adopting an independent channel staff trust.

**Decision 2 (AI suggestion rejected): the AI market scan's advice to "Lead marketing with the 34% retention statistic" (05-market-scan.md).**
- *Options:* use it, use it with a caveat, or replace it with a figure from the pack.
- *Criteria:* every number on the landing page must reproduce from the pack, with no legal claims.
- *What decided it:* the scan cites a "Hospitality Workforce Report, 2027" but no source was attached, and nothing in the pack supports it. I replaced it with the pilot's card tips in and out (€31,754.13 and €31,754.09, takings.csv and payouts.csv).
- *What would change my mind:* the report itself, with its method and sample.

**Bias: automation bias.** At 14:58 UTC on 24 November I told the AI "ill follow you" and accepted all its suggested defaults (ai-log/session-01-claude-code.md). Earlier, at 14:22, I had assumed the CEO set the split rule until the pack showed it was Declan. I caught it when reviewing this README, and re-checked each decision against the pack.

## Part 4c: The Struggle (written without AI)

So first Declan's decision I believe will not produce and promote a healthy relationship with his employees the business solution needs more transparency and we obviously can see someone of the team not getting paid fairy because he works after 23:00.. Raphael's message is clear representation of this problem here and I believe it can even be worse and spread to more employees if not handled properly. The AI market data is not accurate and cannot be shared on the website unfortunately  because the claims are not true. Moving forward I will try to make sure from a stakeholders management perspective that I discuss such challenges with the business owner in advance and try to solve their teams problem during the requirements gathering session while we still have a chance to propose ideas, sadly we are a bit behind in this case and can not challenge Declan's decision at this point of time. 

Commit Hash = 2c810d7

## Appendix: how the figures were checked and what I assumed

Not part of the word counts above.

**Data checks** (run against `data/payouts.csv` and `data/takings.csv`, unmodified from the pack):

- All 152 payout rows: `points` = `points_per_hour` × (`hours` − `hours_after_2300`). 0 mismatches.
- Each week's `week_pool_eur` equals SUM(`card_tips_eur`) in takings.csv for that week. 12 of 12 weeks match.
- Each `tip_payout_eur` equals pool × points ÷ SUM(points) for that week, to the cent. 0 mismatches.
- Card tips in, weeks 1–12: €31,754.13. Paid out: €31,754.09 (rounding).
- Service charge, weeks 1–12: €9,004.69. Every non-zero row has `service_charge_paid_to` = `house`.
- Rafael (S12), weeks 1–12: 527.5 hours, 178.5 after 23:00 (34%), €679.02 paid.

**Hidden figures on the staff view** (the Monday text shows only the payout):

- The week's tip pool: `data/takings.csv`, filter `week = N`, SUM(`card_tips_eur`).
- Hours that earned no tips: `data/payouts.csv`, filter `staff_id = S12, week = N`, `hours_after_2300`.

**Assumptions:**

- The staff view is a demo of one person's view (Rafael, S12). It has no login, and it is not a staff management system.
- "Week N" is the pilot week in the data, and the payout shown is the one for that week's work.
- Mehmet (S13) left after week 8. This is inferred from his rows stopping, and it matches Rafael's "since Mehmet go".
- Niamh's "the chefs are on a better hourly rate" cannot be checked, because the pack has no wage data.
- Colleague figures appear only for the whole team (12 or 13 people). Floor manager (1), bar (2) and kitchen porter (1–2) are never shown as groups.
- The concern feature is simulated. It saves to `localStorage` on the device only and sends nothing.
- The Portuguese text was machine-translated with AI and has not been checked by a native speaker. The page says so.

**AI use:** the pages and the parts of this README marked for AI use were built with Claude Code. The sessions are in [`ai-log/`](ai-log/).
