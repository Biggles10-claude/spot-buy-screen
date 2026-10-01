# Spot Buy Screen — Research Audit

**Audit timestamp:** 2026-10-02 07:16 AWST (Australia/Perth)  
**Board as-of:** 2026-10-02 ~00:26 AWST (prices/picks from original publish)  
**Live URL:** https://biggles10-claude.github.io/spot-buy-screen/  
**Auditor:** Grok Bot (executor) reviewing artifacts under `skills/` + `research/`

---

## Rubric (10 points)

| Dimension | Max | Score | Evidence |
|---|---:|---:|---|
| Pipeline completeness (steps 1–7 ran) | 2 | 1.2 | STATUS shows STEP1–7; EDGAR/13F primary fetches failed |
| Primary-source depth (EDGAR/IR/XBRL) | 3 | 1.0 | EDGAR HTTP 403 (BLOCKER.md); MSFT IR PR strong; NVDA secondary; EQIX empty |
| Valuation rigor (ratios + DCF) | 2 | 0.5 | Ratios for NVDA+MSFT only; scenario earnings table only — DCF missing FCF/WACC/XBRL |
| Pick coverage quality (15 names) | 2 | 1.0 | MSFT/NVDA deeper; EQIX/ASML/TSM/NEM/BHP/SOL thin vs theme/price only |
| Documentation & labeling | 1 | 0.8 | STATUS, BLOCKER, secondary labels present; board lacked audit/pipeline UI until this pass |
| **Total** | **10** | **4.5** | |

---

## Verdict

| Field | Value |
|---|---|
| **Thoroughness score** | **4.5 / 10** |
| **Thorough?** | **no** |
| **Critical gaps** | **5** (EDGAR block; incomplete DCF; ratios only 2 names; 13F secondary-only; thin sleeve names) |
| **Invented-data check** | **Pass with caveats** — no fabricated prices found; board prices match `research/quotes` / CoinGecko / Yahoo artifacts. Filing figures for NVDA FY are **secondary** (edgar.tools / WebSearch). Scenario PTs are labeled illustrative. SEC HTML URLs are cited but **not fetched live** from this box (403). |

Honest lean: **not thorough**. The pipeline executed end-to-end and documented blockers, but primary filings were unreachable, DCF was incomplete, and a majority of the 15 picks lack dedicated deep-dive artifacts comparable to MSFT/NVDA.

---

## Critical gaps vs nice-to-haves

### Critical
1. **EDGAR 403** — All `data.sec.gov` / `sec.gov` fetches from box egress blocked by Akamai (“Undeclared Automated Tool”). Most `*_list.txt` / `*_doc.txt` are 39-byte error stubs (MSFT/EQIX); NVDA list files captured error traces (~734 B) not filing JSON.
2. **DCF incomplete** — `skills/models/SCENARIO_DCF.md` is reverse-earnings / exit-multiple scenarios only. Missing: FCF bridge, WACC, diluted-share XBRL, buyback schedule.
3. **Ratios coverage** — Only NVDA + MSFT in `skills/ratios/`. EQIX omitted by design (no verified fundamentals). No ratios for AAPL/GOOGL/ASML/TSM/NEM/BHP/JPM/META.
4. **13F primary missing** — Berkshire Q2 2026 accession `0001193125-26-352200` known; holdings from aggregators (13f.finance / PortfolioSavvy / Forbes). Live CIK JSON 403 (`fetch_attempt.txt`).
5. **Thin picks** — EQIX (price + theme), ASML/TSM/NEM/BHP (Yahoo + OCBC/CMC secondary PDFs), SOL (price + macro blog) lack company-level filing or IR deep dives.

### Nice-to-haves
- Segment / Intelligent Cloud growth series for MSFT invalidation tracking
- Spot ETF flow time-series artifact (not just The Block article URL)
- Cross-check CoinGecko vs Yahoo for all crypto at card level (already partial)
- Peer comps for EQIX (DLR, etc.) once filings available

---

## Per-pick confidence (artifact-depth audit)

Confidence here is **research-depth confidence**, not a price target. Based on files present under `skills/` + `research/`, not invented diligence.

| Ticker | Horizon | Audit conf. | Why (artifacts) |
|---|---|---|---|
| MSFT | MEDIUM | **High** | IR FY2026 PR figures; `MSFT_SUMMARY.md`; ratios.json; scenario_dcf.json |
| NVDA | MEDIUM | **Med** | `NVDA_SUMMARY.md` secondary 10-K/10-Q excerpts; ratios; scenarios; EDGAR not live |
| AAPL | LONG | **Med** | BRK 13F secondary multi-aggregator; Yahoo price; no Apple IR/10-K deep dive in repo |
| GOOGL | MEDIUM | **Med** | BRK Q2 add documented in `BRK_Q2_2026_SUMMARY.md` (secondary); Yahoo price |
| IBIT | SHORT | **Med** | Yahoo price + The Block flow article + Bitfinex macro |
| ETH | SHORT | **Med** | CoinGecko + Yahoo cross-check + flow/macro URLs |
| BTC | LONG | **Med** | CoinGecko + Yahoo + ETF flow article |
| JPM | SHORT | **Med** | Official IR earnings-call notice + Yahoo; no 10-Q deep dive |
| META | SHORT | **Med** | Secondary earnings calendars (FXEmpire/InvestingCalendar) + Yahoo — date not IR-confirmed in artifact |
| NEM | MEDIUM | **Low** | Yahoo + CMC/OCBC theme PDFs only |
| BHP | LONG | **Low** | Yahoo + CMC/OCBC theme PDFs only |
| ASML | LONG | **Low** | Yahoo + OCBC/SOXX commentary; no ASML order/bookings primary |
| TSM | LONG | **Low** | Yahoo + OCBC PDF; no TSMC filings in repo |
| EQIX | MEDIUM | **Low** | `EQIX_SUMMARY.md` explicitly Low; IR path 404; EDGAR empty stubs; Yahoo price only |
| SOL | SHORT | **Low** | CoinGecko price + Bitfinex macro; no protocol/fundamentals artifact |

**Note:** Original `picks.json` confidence for AAPL was High (sponsorship narrative). Audit downgrades to **Med** on artifact depth. MSFT remains **High**. EQIX/SOL correctly Low in picks; ASML/TSM/NEM/BHP audit to **Low** (were Med in picks.json).

---

## Invented-data / secondary-only flags

| Claim area | Status |
|---|---|
| Live board prices | Backed by `research/quotes/*.json` and/or `coingecko_prices.json` as-of 2026-10-02 ~00:20–00:26 AWST |
| MSFT FY2026 revenue/OI/NI/EPS | Backed by Microsoft IR PR (official) cited in `MSFT_SUMMARY.md` |
| NVDA FY2026 rev/NI/assets; Q2 rev table | **Secondary** — edgar.tools / WebSearch excerpts; label Med |
| BRK portfolio $299.25B; AAPL ~$66B; GOOGL add | **Secondary aggregators**; accession cited; primary XML not on disk |
| Scenario PTs (MSFT/NVDA) | **Illustrative only** — not advice; incomplete DCF inputs |
| META earnings ~27–28 Oct | **Unverified / secondary calendars** — confirm via Meta IR |
| EQIX fundamentals | **Unverified** — price only from Yahoo |

No board claim was found that invents a filing number without a cited secondary path. Remediation is to replace secondary with primary, not to invent “fixes.”

---

## Recommended remediations (actionable)

1. **Retry EDGAR** via `https://data.sec.gov/` with a declared User-Agent (`OrgName email@domain`) from a non-blocked egress; persist submissions JSON + primary 10-K/10-Q HTML/XBRL for NVDA, MSFT, EQIX, AAPL, GOOGL.
2. **Complete DCF** — pull cash-flow XBRL → FCF; set explicit WACC and terminal growth; replace or supplement exit-PE scenarios; document assumptions in `skills/models/`.
3. **EQIX deep-dive** — fetch Equinix IR PDF / latest 10-K once EDGAR or IR works; record bookings, utilization, AFFO/debt; upgrade confidence only after artifacts land.
4. **Primary 13F** — download accession `0001193125-26-352200` information table XML/HTML from SEC when reachable; replace aggregator tables.
5. **Extend ratios** — at least AAPL, GOOGL, ASML, TSM, JPM, META, NEM, BHP (or explicitly exclude with reason).
6. **Thin-name deep dives** — one IR/earnings primary page each for ASML (orders), TSM (utilization), NEM (AISC), BHP (copper/iron guidance), SOL (only if keeping — else drop or keep Low).
7. **META date** — replace calendar scrapes with Meta Investor Relations confirmed date before SHORT event sizing.
8. **Board UX (this pass)** — surface audit verdict, pipeline log, gap remediations, per-pick confidence + skill artifact links on the live Pages board.

---

## Pipeline log (what each skill produced)

| Step | Skill / action | Output on disk | Quality |
|---|---|---|---|
| 1 | analyst-kit-core | STATUS onboarded; gh=Biggles10-claude | OK |
| 2 | sec-filings | BLOCKER.md; NVDA/MSFT/EQIX summaries; Yahoo charts; many 39 B stubs | Partial — EDGAR blocked |
| 3 | 13f | BRK_Q2_2026_SUMMARY.md; fetch_attempt.txt (403) | Secondary only |
| 4 | ratios | RATIOS.md + ratios.json (NVDA, MSFT) | Partial |
| 5 | models | SCENARIO_DCF.md + scenario_dcf.json | Illustrative; DCF incomplete |
| 6 | picks + HTML | research/picks.json; index.html (15 picks) | OK structure; thin research on many names |
| 7 | publish | Pages live HTTP 200 ~00:26 AWST | OK |
| 8 | **audit (this run)** | research/AUDIT.md + rebuilt index.html | Surfaces gaps |

---

## Sources for this audit

- `STATUS.md`, `skills/sec-filings/BLOCKER.md`, `*_SUMMARY.md`, `skills/13f/BRK_Q2_2026_SUMMARY.md`, `skills/ratios/*`, `skills/models/*`, `research/picks.json`, `research/quotes/*`, `research/coingecko_prices.json`, prior `index.html`
