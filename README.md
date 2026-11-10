# Predicting below-average US nursing homes

MLDA CW1 (Machine Learning and Data Analytics), student ID 00017694.

**Goal.** Predict whether a US nursing home is rated below average (1–2 stars on the CMS Five-Star Quality Rating, about 39% of homes) from operational data: staffing levels, staff turnover, ownership, chain membership, size and occupancy. Supervised binary classification.

**Who would use it.** Families, hospital discharge planners and state regulators who want to spot homes at risk of a low rating before the next inspection.

**Leakage note.** CMS calculates the overall rating from the health-inspection, staffing and quality-measure ratings in the same file. Those columns, and the scores they are built from, are removed before modelling.

**App:** TODO, add the Streamlit Community Cloud link once deployed.

## Data

CMS Nursing Home Care Compare, October 2026 release. Public domain (US federal government data).

| File | Rows (approx.) | Source |
|---|---|---|
| `NH_ProviderInfo_Oct2026.csv` (main table) | 14,686 homes × 102 columns | https://data.cms.gov/provider-data/dataset/4pq5-n9py |
| `NH_HealthCitations_Oct2026.csv` | 418,682 | https://data.cms.gov/provider-data/dataset/r5ix-sfxw |
| `NH_Penalties_Oct2026.csv` | 15,007 | https://data.cms.gov/provider-data/dataset/g6vv-u9sr |
| `NH_Ownership_Oct2026.csv` | 252,468 | https://data.cms.gov/provider-data/dataset/y2hd-n93e |

The linked files are aggregated per home and joined to the main table on the CMS Certification Number (CCN).

The raw files are not in this repository (the citations file is about 165 MB). Download the four CSVs from the links above and put them in `data/raw/` with the file names shown.

## Setup

Requires Python 3.13.

```bash
python3.13 -m venv venv
source venv/bin/activate           # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## Run

```bash
# notebook: open notebooks/ in VS Code or Jupyter with the venv kernel

# Streamlit app
streamlit run app/Home.py
```

## Project layout

```
app/              Streamlit multipage app (Home.py + pages/)
data/raw/         raw CMS downloads (git-ignored)
data/processed/   small processed tables for the app
models/           final saved pipeline and metrics
notebooks/        main analysis notebook
src/              data loading, cleaning and feature code
```

## Licence

Code: MIT (see `LICENSE`). Data: public domain, from the Centers for Medicare & Medicaid Services.
