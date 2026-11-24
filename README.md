# Sciar Tips · CA2 (H9LOCHFFT)

- **Live site (GitHub Pages):** https://amoraba.github.io/sciar-tips/
- **Repository:** https://github.com/Amoraba/sciar-tips

**My question:** When a kitchen porter can see the hours that earned him no tips, and can raise it without going through his manager, does the silence behind "nobody has ever complained" break?

> Sciar, Halloran's and everyone in them are fictional, invented for teaching. Staff view: [app.html](https://amoraba.github.io/sciar-tips/app.html) · Landing page: [index.html](https://amoraba.github.io/sciar-tips/)

## Part 1: The people

**Internal: Aoife Rennick (CEO, Sciar).** She needs an alpha that works for staff on the devices they have: "Make it work on a phone. Nearly all restaurant staff only have phones." (04-aoife.md)

**External: Rafael (kitchen porter, Halloran's).** He needs to understand his pay and ask without being exposed: "i dont understand how they count it" and "please dont say it was me who ask" (01-rafael.md).

**Accessibility and culture:** Rafael writes in a second language on a damaged phone: "sorry for my english" and "my phone screen is broken so i cannot read the page good" (01-rafael.md). So the staff view uses large plain-English text, a Portuguese toggle and no long links.

## Part 4a: Theory behind the build

## Part 4a: Theory behind the build

**Leadership — Transactional leadership (Burns, 1978):** Declan's emphasis on established rules and control over the points formula reflects a transactional approach, where defined expectations and rewards guide behaviour. His request to hide the formula suggests that consistency and managerial control are prioritised over employee participation. This explains the preference for predictable administration but misses employees' perceptions of fairness.

**Culture — Organisational silence and psychological safety (Morrison and Milliken, 2000; Edmondson, 1999):** Rafael's request not to be identified, alongside Niamh's rejection of a complaints feature, suggests conditions in which employees may withhold concerns. This influenced the inclusion of a concern-submission feature in the staff dashboard.

These choices affect Sciar's competitive advantage: owner control may support customer retention, while employee transparency and voice could differentiate Sciar through trust. However, individual messages cannot establish the culture of an entire organisation, and the theories do not prove why employees remain silent.

## Part 4b: Decision record

## Part 4b: Decision record

**Decision 1 — Aoife's request to remove the concern feature:** I considered removing it, directing employees to Niamh, or retaining a private submission mechanism. I retained the feature because Rafael fears being identified when raising concerns. I prioritised employee voice and psychological safety while avoiding a public complaints wall. Submissions remain visible only to the submitting user on their device; they are not transmitted to management. Evidence of a trusted, secure alternative could change this decision.

**Decision 2 — AI-generated retention claim:** Aoife recommended using the claim that transparent tip distribution improves staff retention by 34%. I considered using it, removing it, or replacing it with a verifiable claim. I rejected it because the AI market scan supplied no supporting source. Accuracy and credibility outweighed marketing appeal. An independently verified study with a relevant methodology could change my decision.

**Personal bias — Customer-centricity bias:** I initially favoured Declan's preferences because he pays Sciar. I recognised that this could lead me to undervalue employees' needs. I therefore retained owner control of the full points configuration while providing employees with greater visibility into their own payments.

## Part 4c: The Struggle (written without AI)

_to be written_

---

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
