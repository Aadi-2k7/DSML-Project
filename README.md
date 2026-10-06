# COVID-19 India: Exploratory Data Analysis

An end-to-end exploratory data analysis (EDA) of the COVID-19 pandemic in India, built with Python. The project loads state-level case data and national vaccination data directly from public sources, cleans and standardises it, engineers key epidemiological metrics, and presents the findings through a series of visualisations.

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![pandas](https://img.shields.io/badge/pandas-data%20analysis-150458)
![Matplotlib](https://img.shields.io/badge/Matplotlib-visualisation-11557c)
![Seaborn](https://img.shields.io/badge/Seaborn-statistical%20plots-4c72b0)

---

## Table of Contents

- [Overview](#overview)
- [Data Sources](#data-sources)
- [Methodology](#methodology)
- [Visualisations](#visualisations)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Output](#output)
- [Limitations](#limitations)
- [Future Work](#future-work)
- [Author](#author)

---

## Overview

This project answers questions such as:

- How did confirmed cases, recoveries and deaths evolve across India over time?
- Which states and union territories were the most and least affected?
- How do recovery and death rates compare across states?
- How did the daily case load change month to month?
- How did India's vaccination drive progress?

The entire workflow, from data ingestion to cleaned export, is contained in a single reproducible script.

## Data Sources

| Dataset | Description | Source |
|---|---|---|
| State-wise cases | Daily confirmed, cured and death counts per state/UT | [imdevskp/covid-19-india-data](https://github.com/imdevskp/covid-19-india-data) |
| Vaccinations | Daily national vaccination figures for India | [Our World in Data](https://github.com/owid/covid-19-data) |

Both datasets are fetched live from their public GitHub repositories, so no manual download is required.

## Methodology

### 1. Data Ingestion
Both datasets are read directly from raw GitHub URLs with `pandas.read_csv`. Shape, data types and missing-value counts are inspected up front.

### 2. Data Cleaning
- Renamed columns to a consistent, code-friendly schema (`date`, `state`, `confirmed`, `deaths`, `cured`, ...).
- Converted `date` to `datetime`, and coerced `deaths` to numeric, filling invalid entries with zero.
- Standardised inconsistent state/UT names (for example `Telengana` and `Telangana***` merged into `Telangana`, and `Union Territory of ...` prefixes removed).
- Removed duplicate `(date, state)` records and sorted chronologically per state.

### 3. Feature Engineering
- **Active cases** = confirmed - deaths - cured
- **Recovery rate (%)** = cured / confirmed x 100
- **Death rate (%)** = deaths / confirmed x 100
- **Daily new confirmed cases** derived from the national cumulative series
- **Month** field for time-based aggregation

### 4. Analysis
- National time series built by aggregating state records by date
- Latest-date snapshot with a ranked Top 10 of affected states
- Monthly new-case pivot table for the top 5 states
- Correlation analysis across national metrics

## Visualisations

| # | Chart | Purpose |
|---|---|---|
| 1 | Line chart | Cumulative confirmed, recovered and deaths for India |
| 2 | Bar chart | Daily new confirmed cases |
| 3 | Horizontal bar | Top 10 states by confirmed cases |
| 4 | Horizontal bar | Recovery rate of the top 10 affected states |
| 5 | Multi-line chart | Case trajectory of the top 5 states |
| 6 | Pie chart | Share of total confirmed cases by state |
| 7 | Line chart | National recovery rate over time |
| 8 | Scatter plot | Recovery rate vs death rate, sized by case count |
| 9 | Heatmap | Correlation between COVID-19 metrics |
| 10 | Box plot | Distribution of daily new cases by month |
| 11 | Line chart | Vaccination progress (total doses and fully vaccinated) |
| 12 | Horizontal bar | 10 least-affected states/UTs |

## Tech Stack

- **Language:** Python 3
- **Data handling:** pandas, NumPy
- **Visualisation:** Matplotlib, Seaborn

## Project Structure

```
DSML-Project/
├── covid_analysis.py        # Full analysis pipeline
├── cleaned_covid_india.csv  # Generated cleaned dataset (created on run)
└── README.md
```

## Getting Started

### Prerequisites
- Python 3.9 or higher
- An active internet connection (data is loaded from GitHub)

### Installation

```bash
# Clone the repository
git clone https://github.com/Aadi-2k7/DSML-Project.git
cd DSML-Project

# (Optional) create a virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # macOS / Linux

# Install dependencies
pip install numpy pandas matplotlib seaborn
```

### Run

```bash
python covid_analysis.py
```

Charts open one after another; close each window to proceed to the next. For an interactive experience, the script can also be pasted into a Jupyter Notebook or run cell by cell in VS Code.

## Output

Running the script produces:

- Console summaries of data shape, cleaning results and the latest national statistics (confirmed, recovered, deaths, recovery rate, death rate)
- The 12 visualisations listed above
- `cleaned_covid_india.csv`, the cleaned and enriched state-level dataset, ready for further analysis or modelling

## Limitations

- The state-level case dataset is a historical snapshot and may not extend to the end of the pandemic.
- Reported figures depend on the quality and reporting practices of the upstream sources.
- Because data is pulled from remote URLs, the script will fail if those files are moved or removed.

## Future Work

- Add per-capita normalisation using state population data
- Build interactive dashboards with Plotly or Streamlit
- Add time-series forecasting of case trends
- Analyse state-wise vaccination coverage against case outcomes

## Author

**Aditya**

- GitHub: [@Aadi-2k7](https://github.com/Aadi-2k7)
- LinkedIn: [linkedin.com/in/aadi-2k7](https://linkedin.com/in/aadi-2k7)

---

If you found this project useful, consider giving it a star.
