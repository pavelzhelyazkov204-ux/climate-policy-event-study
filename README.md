# Do Markets React to Climate Policy Signals?

Event-study analysis from my bachelor thesis, examining how European equity markets
(France, Italy, Spain) reacted to US political events widely seen as climate policy
signals: the **2024 US presidential election** (2024-11-06) and the **2025 presidential
inauguration** (2025-01-20).

## Methodology

For each event, the pipeline:

1. **Loads daily total returns** for French (CAC), Italian (FTSE MIB) and Spanish (IBEX)
   constituents, plus firm attributes (GICS industry, ESG score) from Refinitiv Eikon.
2. **Cleans the panel** — drops stocks with excessive missing/zero/flat return series and
   filters implausible observations.
3. **Estimates expected returns** over an estimation window that excludes the event window,
   using two models:
   - **CAPM** (market model against the STOXX Europe 600), and
   - the **Fama-French 3-factor model** (Mkt-RF, SMB, HML from the Kenneth French data library).
4. **Computes abnormal returns** (AR), average abnormal returns (AAR) and cumulative average
   abnormal returns (CAAR) over event windows of ±1, ±3 and ±5 trading days.
5. **Tests significance** with the **Patell (1976)** standardized-residual test and the
   **BMP (Boehmer-Musumeci-Poulsen, 1991)** test, both with and without the
   **Kolari-Pynnönen (2010)** cross-sectional correlation adjustment.
6. **Aggregates results** by GICS sector and by an ESG-based green/brown classification
   (A-grades = "Green", D-grades = "Brown"), and plots sector-level CAAR paths and
   daily AR distributions.

## Notebooks

| Notebook | Description |
|---|---|
| `01_inauguration_event_study.ipynb` | Main event study — 2025 US inauguration, combined FR/IT/ES sample |
| `02_election_day_event_study.ipynb` | Same pipeline for the 2024 US election result |
| `03_france_election_event_study.ipynb` | Earlier France-only version, where the methodology was developed |

## Data

The input data (daily stock returns, GICS industries and ESG scores) was retrieved via the
**Refinitiv Eikon API** under a university license and is **not redistributed in this
repository**. Fama-French factors come from the
[Kenneth French data library](https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html).

To run the notebooks you need:

- A Refinitiv Eikon / Workspace app key, exposed as an environment variable:
  `EIKON_APP_KEY`
- The input Excel/CSV files (`*_stock_returns.xlsx`, `*_stock_attributes.xlsx`,
  `famafrench.csv`) placed next to the notebooks.

## Setup

```bash
pip install -r requirements.txt
```
