# SEC EDGAR blocker (2026-10-02 AWST)

All requests to sec.gov / data.sec.gov / efts.sec.gov from this box return **HTTP 403**
(Akamai: "Your Request Originates from an Undeclared Automated Tool"), including:
- `python3 edgar.py` with `SEC_EDGAR_UA="BigglesResearch biggles10-claude@users.noreply.github.com"`
- curl with proper User-Agent + Accept
- google-chrome --headless dump-dom

Workaround used: public IR pages, Yahoo Finance quote/filings pages, WebSearch
summaries that cite EDGAR accession/date, CoinGecko for crypto. Filing *lists*
and financial figures below are only those verified from non-SEC public pages or
explicitly labeled as secondary. No invented numbers.
