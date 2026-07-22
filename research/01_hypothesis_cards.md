# Phase 3 — Hypothesis cards (batch B2026-07-22)

Rules applied: ≤3 planned variants per hypothesis; ≥7 independent mechanisms; blueprints used as economic prompts only (no copied formulas).

Shared baseline unless pack overrides: Equity · FASTEXPR · USA · TOP3000 · Delay 1 · Pasteurization On · Unit Verify · NaN Off · Visualization On · Test period 1y · Max Trade Off · Truncation 0.01.

---

## C01 — PV-R06 — Volume-amplified short reversal
- **Economic mechanism:** Temporary liquidity-driven price pressure; abnormal participation makes a one-day move more likely to reverse next sessions.
- **Chosen fields (public PV):** `returns`, `volume`; group `subindustry`
- **Expected sign:** Negative short return with high relative volume → positive next relative return (expression short the pressure → long the bounce).
- **Expected horizon:** 1–5 days
- **Data lag:** Session OHLC/volume; Delay 1
- **Baseline pack:** P1 (Subindustry, Decay 6, Trunc 0.01)
- **Primary confounder:** Size/liquidity loading; crowded generic reversal
- **Expected failure:** Momentum news days; earnings gaps
- **Variants:** (1) field: close/open-1 instead of returns; (2) window: vol mean 10 vs 20; (3) neut: Industry
- **Kill:** Sign flips across neighboring windows; sub-universe collapse; self-corr ≥ live limit vs existing reversal book
- **Originality:** Volume scale is a participation conditioner, not a plain open–close rank clone of the public teaching example.

## C02 — SX-02 — Residual momentum
- **Mechanism:** Continuation in stock-specific returns after removing contemporaneous industry co-movement.
- **Fields:** `returns`, group `industry`
- **Sign:** Higher residual multi-week sum (skipping recent days) → long
- **Horizon:** ~20–120d (skip ~5d)
- **Lag:** Delay 1 price
- **Pack:** P2 (Industry, Decay 10)
- **Confounder:** Incomplete residualization leaving sector beta
- **Failure:** Trend crashes; 2009/2020-style reversals
- **Variants:** market vs industry residual; L=60/90; Sector neut
- **Kill:** No incremental yearly stability vs raw momentum; only one L works
- **Originality:** Residual definition + skip window; not another raw close lookback.

## C03 — SX-05 — Smooth-path momentum
- **Mechanism:** Paths driven by many moderate days are more persistent than paths dominated by one jump.
- **Fields:** `returns`
- **Sign:** Positive medium momentum × low jump-concentration → long
- **Horizon:** ~40–80d
- **Pack:** P2
- **Confounder:** Mechanical low-vol / low-event exposure
- **Failure:** Event-driven trends that are genuinely informative
- **Variants:** jump metric max vs top-2 share; L=40/60; gate vs multiply
- **Kill:** Identical PnL to plain momentum; fragile to removing largest day
- **Originality:** Explicit path-quality penalty, not return magnitude alone.

## C04 — SX-08 — Illiquidity shock / recovery
- **Mechanism:** Unexpected Amihud-style illiquidity shocks pressure prices; partial normalization can predict recovery.
- **Fields:** `returns`, `close`, `volume` (dollar volume proxy)
- **Sign:** Baseline v1 tests **shock** (high unexpected illiquidity → short). Recovery leg is variant 2.
- **Horizon:** 10–40d
- **Pack:** P3 (Industry, Decay 12)
- **Confounder:** Permanent illiquidity premium vs temporary shock
- **Failure:** Microcap concentration; denominator zeros
- **Variants:** shock z-score window; recovery/reversion leg; Market neut
- **Kill:** Entire edge from bottom liquidity decile; weight concentration fail
- **Originality:** Separates unexpected shock from slow illiquidity level.

## C05 — SX-09 — Improving gross profitability
- **Mechanism:** Rising operating productivity (gross profit / assets) is more timely than static profitability.
- **Fields:** map in Data Explorer — gross profit / profit before depreciation analogs; total assets; avoid inventing IDs
- **Sign:** Positive industry-relative improvement → long
- **Horizon:** 1–4 quarters
- **Pack:** P4 (Industry, Decay 20)
- **Confounder:** Value/quality overlap; financials
- **Failure:** Restatements; sector accounting differences
- **Variants:** level vs Δ; sequential vs YoY; exclude financials if operator available
- **Kill:** Works only as static GP/A clone; stale between filings
- **Status:** FIELD_MAP_REQUIRED

## C06 — SX-11 — Accrual quality
- **Mechanism:** Earnings far above operating cash flow are less persistent.
- **Fields:** net income / earnings; operating cash flow; assets scaler
- **Sign:** High accruals → short
- **Horizon:** quarterly
- **Pack:** P4
- **Confounder:** Industry structure of WC; banks
- **Variants:** total vs WC accruals; scale choice; Industry vs Subindustry
- **Kill:** Sign unstable across industries; coverage < usable book
- **Status:** FIELD_MAP_REQUIRED

## C07 — SX-16 — Cash-conversion-cycle improvement
- **Mechanism:** Shortening CCC (DIO+DSO−DPO) signals operating efficiency gains.
- **Fields:** inventory/receivable/payable day counts or components to construct CCC
- **Sign:** CCC decrease → long
- **Horizon:** quarterly
- **Pack:** P4
- **Confounder:** Seasonality; service firms with empty inventory
- **Variants:** component ablation; industry filter; YoY Δ
- **Kill:** Driven by one CCC leg only with unstable sign
- **Status:** FIELD_MAP_REQUIRED

## C08 — SX-19 — Analyst forecast innovation
- **Mechanism:** Revisions unusual vs that stock’s own revision history matter more than raw consensus change.
- **Fields:** forward EPS / estimate revision series
- **Sign:** Positive standardized innovation → long
- **Horizon:** 5–40d
- **Pack:** P5 (Subindustry, Decay 8)
- **Confounder:** Coverage bias; stale consensus
- **Variants:** raw vs ts_zscore; breadth confirm; dispersion scale
- **Kill:** No edge after coverage/liquidity controls
- **Status:** FIELD_MAP_REQUIRED

## C09 — SX-22 — Multi-quarter surprise persistence
- **Mechanism:** Sequence of same-sign standardized surprises predicts drift beyond one print.
- **Fields:** standardized unexpected earnings (SUE) or actual−expected
- **Sign:** Positive weighted surprise history → long
- **Horizon:** 20–60d post events
- **Pack:** P5
- **Confounder:** Overlapping event windows; look-ahead on announce dates
- **Variants:** 2 vs 3 lags (cap 3); equal vs decay weights
- **Kill:** Identical to single-quarter PEAD; timing audit fails
- **Status:** FIELD_MAP_REQUIRED

## C10 — SX-25 — Fresh vs stale news
- **Mechanism:** Novel stories should outweigh reprints/stale headlines.
- **Fields:** sentiment aggregate + novelty/staleness if present
- **Sign:** Fresh positive sentiment → long (short opposite)
- **Horizon:** 1–15d
- **Pack:** P6 (Subindustry, Decay 5)
- **Confounder:** Attention/large-cap bias; MNAR missingness
- **Variants:** fresh-only vs freshness-weighted; intensity gate
- **Kill:** All-news version dominates; sparse coverage book
- **Status:** FIELD_MAP_REQUIRED

## C11 — SX-27 — Residual option skew
- **Mechanism:** Stock skew after removing market/sector skew and ATM IV level carries downside information.
- **Fields:** put−call IV skew; ATM IV; sector/market
- **Sign:** High residual skew → short equity
- **Horizon:** 5–30d
- **Pack:** P7 (Market, Decay 8)
- **Confounder:** Earnings IV crush; sparse names
- **Variants:** raw vs residual; maturity bucket; IV control on/off
- **Kill:** Edge only in top options-liquidity names; coverage fail
- **Status:** FIELD_MAP_REQUIRED

## C12 — SX-30 — Short interest + crowding
- **Mechanism:** Rising short interest is more bearish when days-to-cover / borrow stress also rises.
- **Fields:** short interest/float; days to cover / borrow fee if available
- **Sign:** Confirmed short increase → short stock
- **Horizon:** 20–90d; respect publication lag
- **Pack:** P8 (Industry, Decay 15)
- **Confounder:** Short squeezes; reporting lag
- **Variants:** level vs Δ; confirmation gate; lag audit
- **Kill:** Opposite sign in squeeze regimes; lag unclear
- **Status:** FIELD_MAP_REQUIRED

## C13 — SX-31 — Clustered insider buys
- **Mechanism:** Multiple independent discretionary buyers are more informative than one small purchase.
- **Fields:** insider buy counts/value; exclude automatic plans when tagged
- **Sign:** Higher size-normalized buyer breadth → long
- **Horizon:** 20–120d
- **Pack:** P8
- **Confounder:** Sparse events; Form-4 lag
- **Variants:** breadth vs dollar; executive filter; window 20/60
- **Kill:** Top-name concentration; no breadth effect
- **Status:** FIELD_MAP_REQUIRED

## C14 — SX-32 — Customer→supplier lead-lag
- **Mechanism:** Customer residual returns lead suppliers beyond own and industry momentum.
- **Fields:** relationship/customer links + returns
- **Sign:** Positive lagged customer residual → long supplier
- **Horizon:** 5–40d
- **Pack:** P9 (Sector, Decay 10)
- **Confounder:** Stale links; shared industry already neutralized
- **Variants:** lag 5/10; residual definition; prove vs own momentum
- **Kill:** Zero incremental R² vs own/industry momentum
- **Status:** FIELD_MAP_REQUIRED

## C15 — SX-39 — Two-family ensemble
- **Mechanism:** Average of one slow fundamental/analyst leg and one fast price/event leg only if daily PnL correlation is low.
- **Fields:** survivors from C05/C08 + C01/C02
- **Sign:** Average rank of two validated legs
- **Horizon:** blended — only after each leg alone passes
- **Pack:** P10 (Market, Decay 10)
- **Confounder:** Data-mined pairing; horizon mush
- **Variants:** pair choice; equal avg vs gate; require corr < 0.3 on daily PnL
- **Kill:** Legs highly correlated; ensemble worse than best leg
- **Status:** DEPENDS_ON_SURVIVORS

## Mechanism diversity check

| Family | Candidates |
|---|---|
| Short reversal / microstructure | C01 |
| Momentum / path | C02, C03 |
| Liquidity | C04 |
| Fundamental quality/efficiency | C05, C06, C07 |
| Analyst / earnings | C08, C09 |
| News | C10 |
| Options | C11 |
| Positioning | C12, C13 |
| Network | C14 |
| Ensemble | C15 |
