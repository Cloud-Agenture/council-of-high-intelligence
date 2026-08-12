# EVIDENCE PACK (research briefs, collected before Round 1)

Labels: **[F]** = sourced fact · **[I]** = interpretation · **[⚠]** = folklore / unverified / contested.

---

## A. DALIO / BRIDGEWATER — mechanisms

**Believability weighting.** [F] Weight opinions by demonstrated track record, not seniority. Qualification test is two-pronged: the person (1) has successfully done the thing **at least 3 times**, AND (2) can give a good causal explanation of why it works. Both required.

**Tooling.** [F] Dot Collector (real-time 1–10 ratings on 100+ attributes), Baseball Cards (per-person strength/weakness profile), algorithms converting dots into believability weights.

**The resolution rule — most transferable mechanism.** [F] Votes display **two tallies simultaneously**: one-person-one-vote average AND believability-weighted average. If they agree → done. If they diverge → re-deliberate. If deliberation fails → the believability-weighted result wins.

**Documented exploit.** [F-press] WSJ: in a personnel dispute Dalio weighted Greg Jensen's account higher because Jensen's *investing* believability was high. [I] **Cross-domain believability leakage is the core failure of any weighted-vote system — weights must be domain-scoped.**

**PriOS.** [F] From ~2016 Bridgewater ran a project (David Ferrucci, ex-IBM Watson) to codify the Principles into algorithms. [I] No public evidence it reached full deployment. "Bridgewater automated management" = aspiration, not verified fact.

**All Weather.** [F] Four quadrants — growth ↑/↓ and inflation ↑/↓ **relative to expectations**; each quadrant gets ~25% of *risk*, not capital. Bonds levered up to equalize risk contribution. Public "All Seasons" proxy ≈ 30% equities / 55% Treasuries / 7.5% gold / 7.5% commodities.
Load-bearing assumption: **stock/bond correlation stays low or negative.**
[F-press] **2022 failure**: stock/Treasury correlation ≈ **+0.65** vs long-run ≈ −0.2. HFR Risk Parity 10% Vol index **−19.5%** vs global 60/40 **−16.1%** — the diversified levered product lost MORE than the naive one. All Weather reported ≈ **−22%** in 2022 (worse than −20% in 2008); exact figure contested (−12% to −22% across analyses).
[I] Mechanism: leverage is sized off a covariance matrix; when correlations regime-shift, the leverage justified by diversification multiplies a single common factor (real rates).

**Holy Grail.** [F-quoted] Dalio: "fifteen or more good, uncorrelated return streams… reduce your risk by about eighty percent… five times the return for the same amount of risk."
[F-math] For N zero-correlated equal-vol streams σ_p = σ/√N (N=15 → −74% risk). **But** with average pairwise correlation ρ, σ_min = σ·√ρ **regardless of N**. ρ=0.6 (typical equities) caps risk reduction at ~23% — 1,000 stocks at ρ=0.6 diversify barely better than 5.
[I] **Rule: the marginal value of the Nth stream is governed by ρ, not N.** Same applies to council members and to AI agents: correlated agents add nothing.

**Pure Alpha.** [F] Launched 1991. Alpha/beta separation; ~30–40 uncorrelated positions; rules accepted only if "timeless and universal" — must hold across many decades AND many countries. Execution ~99% systematic.
[F-press] MPI replicated Pure Alpha II with lagged dynamic-beta liquid ETFs at **R² ≈ 67%** — much of "alpha" is time-varying beta.

**Epistemics.** [F] Replace "I'm right" with **"How do I know I'm right?"** Find the most believable people who *disagree* and understand their reasoning. "Pain + Reflection = Progress" — errors logged and converted into new written principles.
[I] Bridgewater's drawdown control is *ex ante* (diversify, cap risk contribution), not *ex post* stop-losses — which is exactly why 2022 got through.

**Performance reality.** [F-press] Pure Alpha II **2012–2024: <3% annualized** (a lost decade). 2020 worst drawdown in fund history. 2022 +9.4% (peaked +22%, gave it back). 2023 **−7.6%**. 2024 +11.3%. 2025 **+33%** (best year in ~50 yrs). Long-run claim ≈11.4% annualized since Dec 1991 — front-loaded. AUM ~$150bn (2022) → **~$102bn**, Pure Alpha deliberately shrunk toward $50–60bn: an admission of capacity decay.
[F] Rob Copeland, *The Fund* (2023) documents the Principles culture as surveillance/conformity; Bridgewater disputes it. Both sides interested parties.

---

## B. BUFFETT / MUNGER / MARKS / KLARMAN / GRAHAM — mechanisms

**"Rule No.1: never lose money."** [⚠] No shareholder-letter source; earliest Buffett usages oral (~1985). Prior formulation is Graham's. **Encode as principle, not citation.**

**Operational content.** [F/I] The target is **permanent impairment of intrinsic value or forced sale — not drawdown.** Berkshire's market value fell ~50% three times (1973–75, 1998–2000, 2008–09) without violating the rule. **Volatility becomes loss only via leverage or liability-driven selling.**

**Margin of safety.** [F] Graham, *Intelligent Investor* Ch.20. Buy at a discount to a *conservatively* estimated value so that estimation error, not skill, absorbs the loss. Buffett's bridge: build for 30,000 lbs, drive 10,000-lb trucks.

**Owner earnings.** [F] 1986 letter appendix: reported earnings + non-cash charges − average annual maintenance capex required to preserve competitive position and unit volume. The last term must be estimated → the figure is a **range, not a point**.

**Circle of competence.** [F] 1996 letter: "The size of that circle is not very important; knowing its boundaries, however, is vital." **Boundary-knowledge is the constraint, not breadth.**

**20-slot rule.** [F] Munger, 1994 USC talk — a lifetime punch card of 20 investments forces per-decision rigor.

**Hurdle & cash.** [F] 2003 annual meeting: ~**10% pre-tax expected return filter**, held "whether short rates are 6% or 1%" (Munger partially dissented: the hurdle is future opportunity cost). [F] 2024 letter: "Berkshire will never prefer ownership of cash-equivalent assets over the ownership of good businesses" — **cash is residual, not a macro call.** Cash: $163.7B (YE2023) → $334.2B (YE2024) → **record $397.4B at 31 Mar 2026**; net equity sales exceeded purchases by ~$172.9B 2022–2024.

**Munger's psychology.** [F] "Invert, always invert." *The Psychology of Human Misjudgment* (1995/2005) — **25 tendencies**, culminating in **lollapalooza**: confluence of several biases acting together. [I] The encodable part: **bias risk is multiplicative, not additive.**

**Marks.** [F] *Risk Revisited Again* (2015): investors fear "the possibility of permanent loss," not volatility — and he concedes this definition **cannot be measured, even after the fact**. [F] *You Can't Predict. You Can Prepare.* (2001). [F] "I know" vs "I don't know" schools. [F] The dial: the whole job is **"where do we stand?"**, measured by observables (valuation spreads, credit terms, deal quality, investor psychology) — never forecasts; aggressiveness set **inversely** to how much risk others are willingly bearing. [F/I] Second-level thinking: edge requires a non-consensus view **that is also correct**. [⚠] "Two-question memo framework" is not canonical; the durable pairs are "What's it worth? / What's in the price?" and "What's the probability of loss, and how bad if it happens?"

**Klarman.** [F] Absolute-return orientation — "you cannot spend relative performance." Cash held when no bargains exist. Baupost ran 30–50% cash and **returned ~5% of capital to investors at end-2010** because opportunities were insufficient. [⚠] "Cash is a call option with no expiration" — widely attributed, not sourced to *Margin of Safety*.

**Graham.** [F] Defensive investor: never below **25%** nor above **75%** in stocks, 50/50 neutral, rebalanced mechanically. Seven defensive screens incl. P/E ≤15 on 3-yr average earnings, P/B ≤1.5, or **P/E × P/B ≤ 22.5**; current ratio ≥2; 10 straight years of positive earnings.

**Position sizing.** [F] Greenblatt: non-market risk falls 46% at 2 stocks, 72% at 4, **81% at 8**, 93% at 16, 96% at 32 → 6–8 positions in different industries capture nearly all diversification benefit. [F] Kelly f* = (bp−q)/b; practitioner standard is **half-Kelly** (~75% of growth at far lower variance). [⚠] "Buffett/Munger use Kelly" is inference, not record.

**Uncomfortable evidence.** [F] Fama-French HML drawdown ≈ **−55% by mid-2020**, deepest in data from 1925; Arnott et al. attribute essentially all of it to valuation-spread widening, not fundamentals — which also makes the school unfalsifiable in short windows. [F] **Berkshire 2010–2019 total return ~242% vs S&P 500 ~257%** — a decade of underperformance. [I] Survivorship: the canon is written by survivors of the 1950–2000 US regime; managers who blew up leave no letters.

---

## C. RUIN MATHEMATICS, TRADERS, CUSTODY RISK

**Recovery identity.** [F] R = D/(1−D): −10%→+11.1%; −20%→+25%; −50%→+100%; −80%→+400%. Structural, not psychological.

**Variance drain.** [F] g = μ − σ²/2. Two portfolios with μ=8%: σ=10% → g≈7.5%; σ=40% → **g≈0%**. Volatility is a direct subtraction from terminal wealth.

**Ergodicity.** [F] Peters, *Nature Physics* 2019: for multiplicative wealth dynamics, ensemble-average growth strictly exceeds time-average growth. "Expected return" describes a population of parallel investors, not one person's trajectory. [I] **For one account compounding over time, maximize log wealth, not expected return.**

**Kelly.** [F] f* = (μ−r)/σ². Growth at fraction c of Kelly: g(c) = (2c − c²)·g_max. **c=0.5 → ~75% of max growth at ~half the volatility. c=2.0 → growth exactly zero. c>2 → deterministic ruin despite a real edge.** f* is quadratically sensitive to σ and linearly to μ — both estimated. A 2× overestimate of edge pushes you to the zero-growth boundary.

**Risk of ruin.** [F] R = ((1−A)/(1+A))^U, A = edge, U = capital in units of bet size. Ruin probability falls **exponentially in units of capital** → **position size dominates edge.**

**PTJ.** [F] 5:1 reward/risk target — "I can be wrong 80% of the time and still not lose." Uses the 200-day moving average. "The most important rule of trading is to play great defense, not great offense."

**Druckenmiller.** [F] "Preservation of capital and home runs." Concentration + liquidity + wholesale exit. [I] Concentration is survivable only with instant exit capability; a retail investor copying the concentration without the exit discipline copies the risk without the control.

**Van Tharp.** [F] R = entry − stop; R-multiple = P&L ÷ R; Expectancy = (Win% × avg win in R) − (Loss% × avg loss in R); size P = (Equity × risk%) / (Entry − Stop).

**Turtles.** [F] N = 20-day EMA of true range (≈ATR). Unit = (1% of equity)/(N × $ per point). Stop = 2N (2% of equity per unit). Max 4 units/market, 12 units/direction. **Size inversely proportional to volatility → constant risk per position across instruments and regimes.**

**Livermore.** [F] Bankrupt at least three times; method survived, size discipline did not.

**Taleb.** [F] Barbell ≈90% maximally safe / ≈10% convex capped-downside; the middle is avoided because its risk is *mismeasured*. VaR states a threshold but is silent on magnitude beyond it — exactly where ruin lives; also non-subadditive. [F] *Statistical Consequences of Fat Tails*: for ~56 years of S&P 500 daily returns, **a single observation accounted for ~80% of sample kurtosis** → sample variance is not a stable estimator → **Sharpe and beta are unreliable ranking devices** for fat-tailed payoffs.

**Correlation regimes.** [F] 2008 and March 2020: correlations converged to 1 as leveraged holders sold what was liquid, not what was overvalued. March 2020: long Treasuries fell alongside equities despite emergency Fed cuts; **gold fell ~12% peak-to-trough** as it was liquidated for margin. [F] 2022: S&P 500 TR −18.1%, Bloomberg US Agg ≈ −13% (worst on record), 60/40 ≈ −17.5% (worst since 1937). Cause: an inflation shock makes stocks and bonds share a discount-rate driver — **the sign of the correlation is regime-dependent.**
[I] **Diversification is a conditional property. Assume it fails in exactly the scenario you bought it for. The only unconditional controls are cash, position size and non-leverage.**

**Gold.** [F] Peak $850 on 21 Jan 1980; low ~$253–264 in 1999–2001; nominal recovery to $850 only in Jan 2008 (28 years). **Inflation-adjusted, the 1980 high was not surpassed until September 2025 — a ~45-year real drawdown**, peak-to-trough real loss ≈ −80–85%. Long-run gold/S&P correlation ≈ 0 to +0.3, negative in *some* equity drawdowns, positive in liquidity crises. Gold vs 10y TIPS real yield: R² ≈ 84% (2005–2021), ~3% (2022–23), ~7% (since 2024) — **the real-rate relationship broke down.**
[I] Gold is a regime hedge with multi-decade failure windows, not insurance. Size it as a position that can lose 80% real for a generation.

**Bonds.** [F] ΔP/P ≈ −D_mod × Δy + ½C(Δy)². Duration 8 → −8% per +100bp. TLT (duration ≈16–17) fell ≈ **−31% in 2022** — a zero-default-risk instrument, halved without a missed payment. Rate risk ≠ credit risk; credit adds a second loss channel correlated with equities.
[I] "Bonds are safe" conflates nominal principal at maturity with mark-to-market and real purchasing power. Only short-duration high-quality paper approximates the safe leg of a barbell.

**CUSTODY / JURISDICTION — directly material to this Principal:**
- [F] **SIPC** (US brokers only): $500,000 per customer, $250,000 cash sub-limit. Covers *missing* assets on broker failure — not market losses. A non-US entity is **not** SIPC-covered even when routing orders to NASDAQ/NYSE.
- [F] **Freedom24** = Freedom Finance Europe Ltd, Cyprus, CySEC licence 275/15, MiFID II; Investor Compensation Fund ceiling **€20,000** per client.
- [F] **Poland**: KDPW compensation scheme, KNF-supervised — 100% of first €3,000, then 90% of the excess, **capped at €22,000**. Excludes investment losses.
- [F] **Armenia**: Deposit Guarantee Fund covers **bank deposits only** (16m AMD / 7m AMD FX). **No securities-investor compensation scheme identified** for brokerage client assets. *(Negative search finding — verify with the CBA directly.)*
- [F] **Freedom Holding (FRHC, NASDAQ)**: Aug 2023 Hindenburg allegations (sanctions circumvention, inflated revenue, commingling of client funds, AML/KYC failures) → Oct 2023 DOJ/SEC scrutiny reported, company disclosed OFAC and SEC inquiries → Jan 2024 **company-commissioned** external review found no evidence of fake revenue (not a regulator finding) → **March 2026: SEC issued a Wells Notice to Freedom Holding Corp., its principal shareholder and CEO Timur Turlov**, signalling contemplated civil proceedings; company filed a Wells response (8-K, reported June 2026). **UNRESOLVED as of Aug 2026.** *(Primary SEC filing was egress-blocked; confirmed via secondary reporting — verify the 8-K directly.)*

[I] **Custody rule:** compensation ceilings (€20k / €22k / $500k) are trivial relative to a real portfolio. The binding control is **counterparty concentration limits per broker-jurisdiction**, not compensation schemes. Two of this Principal's three brokerage relationships sit under the **same parent group with an unresolved Wells Notice** — that is correlation, not diversification.

---

## D. DATA, TOOLING AND INTEGRATION REALITY (Aug 2026)

**Broker rails.**
- [F] **Freedom24 Tradernet API is public and documented** (auth via apiKey+apiSecret generated in the account UI; Python SDK; NodeJS WebSocket client). **Order placement IS supported.** The official `tradernet-api` GitHub org published **MCP servers for Claude Desktop / Claude Code / Codex / Cursor** in June 2026 (updated Aug 2026, MIT). Their own README warns every call hits a **real money account**.
  [I] **This is the single largest design risk in the whole project: the broker ships an LLM-agent interface that can trade. Read-only credential separation must be enforced in code, not in policy.**
- [F] **Interactive Brokers**: TWS API + Client Portal Web API, converging into one OAuth 2.0 "IBKR Web API". Market-data subscriptions are per TWS username, not per account.
- [F] **Alpaca**: free = 15-min delayed + IEX-only realtime; $99/mo full SIP. US-entity onboarding is the constraint for an EU team.
- [F] **Polish bank brokerages (mBank / BOŚ / PKO BP): no public retail trading API found.** Only XTB documents one (xStation5), and XTB is CFD-heavy — a different instrument set. [I] **Architect the Polish leg as a manual-execution leg with file-import reconciliation.**

**Data sources.**
- [F] Free backbone first: **SEC EDGAR / data.sec.gov** (`submissions`, `companyconcept`, `companyfacts`, `frames`; full-text `efts.sec.gov`) — max **10 req/s**, descriptive `User-Agent` with org + email **mandatory** (403 without). **FRED** (~120 req/min with free key). **ECB Data Portal** + **Eurostat** (SDMX, free, no key). **US Treasury** fiscaldata JSON API + daily par-yield-curve XML feed. **FINRA** short-interest API (twice monthly, Rule 4560).
- [F] Paid entry that fits a 4-person team: **EODHD** (€19.99 EOD / €59.99 fundamentals / €99.99 all-in-one; incl. US Treasury rates beta and ETF holdings) + **Finnhub** (60 req/min free tier; free tier forbids monetised/redistributing apps) ≈ <€100/mo covers ~80% of need. **Tiingo** has the cheapest explicit commercial licence ($50/mo). Skip Databento/Intrinio (wrong band).
- [F] **Polygon.io covers no bonds and no physical commodities**; billed per asset class.
- [F] **ETF holdings: no official APIs.** Issuers publish daily-holdings CSVs at undocumented URLs; scrapers exist (`talsan/ishares`, `etf-scraper`). **iShares reports trading-day month-ends, Vanguard calendar month-ends — do not naively join.**
- [I] **Holdings-overlap must be computed in-house** (weight-intersection over two holdings vectors). Two "different" ETFs commonly share **60–80%** of holdings — exactly the hidden concentration a system like this exists to catch.
- [F] Tracking error needs index TR series (licensed); **TER is the best free predictor of tracking difference.** Replication method (physical vs synthetic), sec-lending policy and counterparty caps are **UCITS disclosure documents, not APIs** (UCITS caps single-counterparty swap exposure at 10% of NAV) → needs a document-extraction agent, not a feed.
- [F] **World Gold Council**: datasets but no free API; since **18 Mar 2025 LBMA Gold Price history was removed at ICE Benchmark Administration's request** — LBMA history now needs a licence. Use spot feed or GLD/IAU NAV as proxy.
- [F] News/sentiment: **Marketaux** free 100/day, $29/mo 2,500/day (entity-level sentiment) — best value. **GDELT 2.0** free, ~1 req/5s, rolling 3-month window, strong on macro/geopolitics, weak on tickers. **NewsAPI developer tier is non-commercial by ToS**; commercial from $449/mo — avoid. RavenPack/BigData.com institutional, no public pricing.

**Libraries (GitHub-verified 12 Aug 2026).**
- [F] Alive: **QuantLib** (BSD, pushed 2026-08-12 — the right tool for the bond leg), **Riskfolio-Lib** (BSD-3, CVaR/HRP/risk-parity/drawdown models), **PyPortfolioOpt** (MIT, **repo moved to `PyPortfolio/PyPortfolioOpt`**), **quantstats** (Apache-2.0, tearsheets).
- [F] **Dead / trap: `backtrader`** — last push Aug 2024 **and GPL-3.0** (copyleft trap for a proprietary internal system); **`empyrical`** — last push Jul 2024, Quantopian defunct. **`vectorbt` licence is NOASSERTION** (community edition of commercial VectorBT PRO) — needs legal review before commercial use.

**Prior art in multi-agent finance.**
- [F] **TradingAgents** (Apache-2.0, 97.8k★, arXiv 2412.20138): specialist agents → **bull vs bear debate** → risk manager → trader. 357 open issues, research-grade. [I] Steal the debate topology; do not run its trading loop.
- [F] **ai-hedge-fund** (virattt, **MIT**, 62.8k★): agents personified as famous investors + risk/portfolio managers; explicitly educational/simulated. [I] Most reusable licence — best scaffolding to fork.
- [F] **OpenBB** (71.8k★, licence "Other"/AGPL-historically — verify): one interface over dozens of data providers. [I] Most production-usable item; use as the data-abstraction layer, check licence before embedding.
- [F] **Qlib** (Microsoft, MIT, 47.3k★): industrial, but China-A-share-centric adapters, 472 open issues. **FinRobot** (Apache-2.0, demo-grade), **FinGPT** (MIT, useful as a sentiment-scoring component only).
- [I] **None are production-usable as-is.**

**Compliance (MiFID II — high level, not legal advice).**
- [F] Investment advice = a **personal recommendation** to a **client** on specific instruments, presented as suitable for that person or based on their circumstances.
- [F] **ESMA supervisory briefing ESMA35-43-3861 (2023)** updated 13-year-old guidance for new business models, social media and apps, and states: **implicit recommendations count** — "best in class", "award-winning" framing can constitute a personal recommendation; **presentation and personalisation, not intent, are decisive.**
- [I] Practical constraints: the 4 team members are not "clients" — internal use is materially different, but **re-assess with counsel the moment output reaches an external investor** (Poland/KNF and Armenia/CBA are separate regimes). Human-in-the-loop always; **no order-placement rights in the agent runtime**; present evidence/scenarios/ranges, never "BUY AAPL"; persist inputs, prompts, sources, model versions and timestamps.
- [I] **The more likely near-term breach is data licensing, not securities law** — Finnhub/Tiingo/NewsAPI free tiers forbid commercial use, and a 4-person fund investing its own money is commercial use.
