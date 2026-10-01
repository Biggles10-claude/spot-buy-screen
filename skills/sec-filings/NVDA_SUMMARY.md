# NVDA SEC filings summary (secondary / IR — live EDGAR blocked)

Sources:
- NVIDIA IR SEC Filings page (HTTP 200): https://investor.nvidia.com/financial-info/sec-filings/default.aspx
- EDGAR index (cited via WebSearch, not fetched live): accession 0001045810-26-000021
- NVIDIA Q2 FY2027 10-Q primary doc URL (cited): https://www.sec.gov/Archives/edgar/data/1045810/000104581026000075/nvda-20260726.htm
- FY2026 results IR PR: https://investor.nvidia.com/news/press-release-details/2026/NVIDIA-Announces-Financial-Results-for-Fourth-Quarter-and-Fiscal-2026/default.aspx
- edgar.tools snapshot of 10-K (secondary): https://app.edgar.tools/filing/1045810/0001045810-26-000021

Verified facts (label confidence):
| Item | Value | Source confidence |
|---|---|---|
| CIK | 0001045810 | Public / known |
| Latest 10-K filed | 2026-02-25 | EDGAR index via WebSearch + NVIDIA IR filing details |
| 10-K period end | 2026-01-25 | EDGAR index |
| FY2026 revenue | $215.9B | edgar.tools / IR context (Med — secondary parse) |
| FY2026 net income | $120.1B | edgar.tools (Med — secondary) |
| FY2026 total assets | $206.8B | edgar.tools (Med) |
| Latest 10-Q period | quarter ended 2026-07-26 | SEC 10-Q HTML excerpt via WebSearch |
| Q2 revenue (3mo ended Jul 26, 2026) | $96,221 million | Direct table excerpt from 10-Q via WebSearch (High for that figure) |
| Prior-year Q2 revenue | $46,743 million | Same 10-Q table |
| H1 FY2027 revenue | $177,837 million | Same 10-Q table |

Live Yahoo Finance chart meta (fetched 2026-10-02 AWST from query1.finance.yahoo.com):
- regularMarketPrice: see NVDA_yahoo_chart.json
