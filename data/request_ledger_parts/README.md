# Request ledger parts

The original ledger contains 8,833 deduplicated primary engine request rows plus one header row.

It is split here into nine CSVs only because the connected upload path choked on the 10.8 MB file in one shot. No rows were dropped or recomputed. Every part repeats the same CSV header.

Ranges:

- `request_ledger_0001_1000.csv`
- `request_ledger_1001_2000.csv`
- `request_ledger_2001_3000.csv`
- `request_ledger_3001_4000.csv`
- `request_ledger_4001_5000.csv`
- `request_ledger_5001_6000.csv`
- `request_ledger_6001_7000.csv`
- `request_ledger_7001_8000.csv`
- `request_ledger_8001_8833.csv`

Treat them as one ledger in row order. Each file has its own header, so remove repeated headers if concatenating them mechanically.
