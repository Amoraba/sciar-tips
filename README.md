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

_to be written_

## Part 4b: Decision record

_to be written_

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
