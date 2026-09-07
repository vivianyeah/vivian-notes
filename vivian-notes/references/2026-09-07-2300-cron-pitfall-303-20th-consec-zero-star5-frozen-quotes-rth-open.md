# 2026-09-07 23:00 BJT cron pitfall — P-MR-303 20th consec zero-⭐5

## Summary
20th consecutive zero-⭐5 / zero-trade scan. P-MR-294 → P-MR-297 → P-MR-300 → P-MR-301 → P-MR-302 → **P-MR-303 NEW**.

## Key findings
- US RTH has been open for 1.5h (since 21:30 BJT = 09:30 EDT Tue post-Labor Day) but Stage 2 still returns 0 candidates
- All 32 position prices are IDENTICAL to 22:05 BJT scan (PATH $15.19, HOOD $122.11, DE $693.53, etc.)
- yfinance reports healthy data (92 stocks analyzed per P-MR-260 bb_lo patch)
- Quotes appear frozen at Fri 09-04 close — `yfinance last-good-quote persistence` extending into active RTH
- Cash unchanged at $207.40 across all 09-07 crons
- zt counter: 5 → 6 (P-MR-201 same-BJT-day carry, 5th consecutive time today; P-MR-110 increment)
- cf counter: 0 → 0 (P-MR-125 no increment; cash > $100)

## P-MR-303 classification recipe
When zero-⭐5 streak extends past 20+ scans AND RTH is fully open (≥1h) AND all 32 positions show IDENTICAL prices to the prior cron (inter-scan drift = $0.00), classify as P-MR-303.

Distinct from:
- P-MR-286: yfinance data outage (`closes[-1] == NaN`, `現價=$nan`)
- P-MR-294: 8th consec zero-⭐5 (initial pool-loop discovery, RTH-closed weekend)
- P-MR-302: 19th consec zero-⭐5 (first RTH-open post-Labor Day)

## Watch for resolution
When `len(⭐5) > 0` OR when any position price moves ≥1% vs prior cron → classify "P-MR-303 RESOLVED" and document first triggering candidate.

## Validation log
20/20 consecutive zero-⭐5 scans across P-MR-294/297/300/301/302/303 from 09-04 22:00 → 09-07 23:00 BJT (3 calendar days, 2 RTH-closed days + 1 RTH-open +1.5h day).

## P-MR-256 soft-reset push
Cumulative push #16 SUCCESS: `d2d1ffc..51a563b main -> main` (commit 51a563b).
