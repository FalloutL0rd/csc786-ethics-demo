# Ethical Statement

## Data source
- U.S. Energy Information Administration (EIA) Open Data v2 API (key-based, public statistics)
- Endpoint: `https://api.eia.gov/v2/electricity/retail-sales/data/`
- Metric: `price` (reported in cents/kWh, converted here to USD/kWh)

## Principles
- Public statistical data with no PII.
- Usage follows provider terms and reasonable request rates.
- Transformations are minimal and transparent (column selection + unit conversion).
- API key handled locally and masked in logs.

## Potential risks / limitations
- **Revisions**: official series can be updated over time.
- **Representativeness**: state-level averages are not any single customer’s bill.
- **Units**: the source reports in cents/kWh, so unit clarity matters.

## Mitigations
- Keep an append-only provenance log (`DATA_README.md`) with endpoint, parameters, timestamp, output path, and row count.
- Explicit unit conversion documented in code and README.
- Pin the time window (`start`, `end`) in logs so results are reproducible.
