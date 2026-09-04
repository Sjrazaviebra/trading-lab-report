# 110 trading ideas, no survivors

> **A report on method.** I examined 110 trading ideas across two years of gold data, under one
> rule: the specification **and the kill criterion** are written and timestamped in `git` **before**
> the first measurement.
>
> **Not one demonstrated an edge.** What is left is not a set of strategies — it is **21 measured
> decision rules**, and **22 errors of mine that the protocol caught**.

<sub>**English** &nbsp;·&nbsp; [Français](README.fr.md)</sub>

## 🔎 [**Open the interactive report →**](https://sjrazaviebra.github.io/trading-lab-report/)

*Nine tabs. **The register of all 110 ideas expands row by row** — what each one did, its family,
where it came from, and the reason it was closed. Search, filters, sorting. The 21 rules with the
measurement behind each. The chronicle of the lab. Light and dark theme. Nothing to install.*

<sub>Prefer a single text file? → [**RAPPORT.md**](RAPPORT.md) (French)</sub>

---

### Three things you will find here and nowhere else

**The break-even correction nobody displays**
`p* = (R + c) / ((n + 1) × R)` — your 10× reward target does not need a 9.1% hit rate,
**it needs 10.5% once the spread is paid.** On short horizons, this single correction decides the
sign of the result.

**The order-flow indicator that would have said "sell" while gold doubled**
Across **22 months** and **34.8 million futures contracts**, with the aggressor side supplied by
the exchange rather than inferred: **price rose 111%, cumulative delta lost 628,629 contracts.**

**MetaTrader 5's `iATR` is not Wilder's ATR**
It is a simple moving average of true ranges. **Median gap 8.9%, 90th percentile 25%.**
If you set thresholds with it, they are not the thresholds you think they are.

---

### What this repository contains — and what it does not

| ✅ contains | ⛔ does not contain |
|---|---|
| the full report, written from scratch | no market data *(redistribution forbidden by the providers and by the exchange licence)* |
| the 110-idea register, each with what it did and why it closed | no strategy code, no retained settings, no parameter values |
| the 21 rules, each with the number that established it | no performance figures presented as backed evidence |
| the limits, self-declared and unprompted | no personal data, no account identifiers, no machine paths |

### ⚠️ Disclaimer
This is **not investment advice**, nor a recommendation, nor an offer. Past performance, whether
measured or simulated, is not a reliable indicator of future results. Leveraged trading carries a
**risk of total loss of capital**.

### Licence
The text is published under **[CC BY 4.0](LICENSE)** — reusable with attribution.

*J. Razavi — September 2026*
