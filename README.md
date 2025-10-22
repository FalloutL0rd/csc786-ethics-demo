# Data Collection - EIA Residential Electricity Price

**Real project:** IEC 61850 GOOSE messaging + ICS security.

- I looked for any public APIs exposing GOOSE/ICS/substation communication data. None exist publicly (due to critical-infrastructure protections).
- No other related APIs I could find would provide a direct benefit to my project or related paper.
- As a result, I switched to something more straightforward that still allowed me to get the practice of this process.

This pulls monthly residential electricity price for South Dakota from the EIA (Energy Information Administration).
- Pulls a small time window (last N years).
- Normalizes the response and saves one clean CSV.
- Logs a tiny provenance line (endpoint, params, timestamp, output, rows).

## What this includes
- A notebook that:
  - Calls `https://api.eia.gov/v2/electricity/retail-sales/data/`
  - Filters `state = SD`, `sector = RES`, `frequency = monthly`
  - Converts EIA `price` cents/kWh into USD/kWh for clean look
  - Saves to `data/processed/eia_price_residential_SD_<start>_to_<end>.csv`
  - Appends one JSON line to `DATA_README.md` (key is masked)

## How to run
1. Get a free key: https://www.eia.gov/opendata/index.php
2. In the notebook:
  - Paste your key or set `EIA_API_KEY` as an env var
  - Pick how many years back (`YEARS_BACK`)
  - Run all cells

Example config:
```python
STATE = "SD"
SECTOR = "RES"
YEARS_BACK = 6


