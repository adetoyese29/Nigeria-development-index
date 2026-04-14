# Nigeria Development Index (1960–2024)
### A Data-Driven Analysis of National Progress Across Six Sectors

![Python](https://img.shields.io/badge/Python-3.x-blue) ![pandas](https://img.shields.io/badge/pandas-data--analysis-green) ![matplotlib](https://img.shields.io/badge/matplotlib-visualization-orange) ![Data: World Bank](https://img.shields.io/badge/Data-World%20Bank%20WDI-lightgrey)

---

## Overview

Nigeria is a country of strong opinions and weak data. Arguments about which president ruined the country or which decade was the worst are everywhere — in barbershops, on Twitter, at family dinners. Almost none of those arguments are grounded in numbers.

This project builds a **Nigeria Development Index (NDI)** — a composite scoring system that measures Nigeria's performance across six sectors every year from 1960 to 2024, using real data from the World Bank. It then uses this index to:

1. Track Nigeria's development arc across seven decades
2. Score each democratic president since 1999 on objective, sector-by-sector performance

---

## Key Findings

### Nigeria's Development Score by Decade

| Decade | Composite Score |
|--------|----------------|
| 1960s | 0.230 |
| 1970s | 0.392 |
| 1980s | 0.524 |
| 1990s | 0.426 ← SAP & Military Rule |
| 2000s | 0.549 |
| 2010s | **0.649** ← Best decade on record |
| 2020s | 0.591 ← COVID + Naira collapse |

### Presidential Performance (1999–2023)

| President | Composite | Economy | Education | Fiscal | Human Dev | Infrastructure | Security |
|-----------|-----------|---------|-----------|--------|-----------|----------------|----------|
| **Buhari** | **0.655** | 0.647 | 0.594 | 0.472 | **0.911** | **0.801** | 0.508 |
| Jonathan | 0.650 | **0.766** | **0.603** | 0.639 | 0.796 | 0.679 | 0.418 |
| Yar'Adua | 0.606 | 0.711 | 0.589 | **0.760** | 0.729 | 0.509 | 0.339 |
| Obasanjo | 0.536 | 0.614 | 0.579 | 0.664 | 0.587 | 0.425 | 0.348 |

> **Important caveat:** A higher composite score does not mean a better president — it means better measured outcomes averaged across tenure. Context matters enormously. Buhari's top score is driven by Human Development and Infrastructure gains that were decades in the making, while his Fiscal Health score (0.47) reflects the naira collapse and debt accumulation of his era.

---

## The Six Sectors

| Sector | Indicators | Weights |
|--------|------------|---------|
| **Economy** | GDP per capita, Inflation, GDP growth, Exchange rate, Unemployment | 0.30 / 0.25 / 0.20 / 0.15 / 0.10 |
| **Human Development** | Life expectancy, Child mortality, Water access | 0.45 / 0.35 / 0.20 |
| **Education** | Primary, Secondary, Tertiary enrollment | 0.40 / 0.40 / 0.20 |
| **Infrastructure** | Electricity access, Internet usage | 0.60 / 0.40 |
| **Fiscal Health** | External debt, Oil rents, Foreign aid, FDI, Remittances | 0.30 / 0.25 / 0.20 / 0.15 / 0.10 |
| **Security** | Political stability, Voice & accountability, Battle deaths | 0.45 / 0.35 / 0.20 |

---

## Methodology

**Normalization:** Every indicator is scaled to 0–1 using min-max normalization, where 0 = worst Nigeria ever recorded for that indicator and 1 = best.

**Inversion:** Eight indicators where higher values are worse (inflation, exchange rate depreciation, unemployment, child mortality, oil dependency, external debt, foreign aid dependency, battle deaths) are inverted so that 1 always means good and 0 always means bad.

**Weighting:** Indicators are combined using deliberate weights reflecting relative importance within each sector. Weights within each sector sum to 1.0.

**Aggregation:** Weighted scores are summed per year to get a yearly sector score, then averaged within each decade or presidential tenure.

---

## Limitations

- The World Bank did not track Nigeria consistently before 1980. Early decade scores (1960s, 1970s) are based on fewer indicators and should be interpreted with caution.
- Some important indicators — poverty headcount, literacy rate — have too many gaps to use reliably and were excluded.
- Presidential tenure averages hide variation *within* a presidency. A president who improved in year 1 and collapsed in year 7 scores the same as one who maintained steady mediocrity.
- Oil prices, global economic cycles, and inherited conditions are not accounted for in this model.
- Security sector data is only available from 1996 onward.
- This analysis measures *outcomes*, not governance quality. Some outcomes improve regardless of who is in power.

---

## Challenges

### Technical challenges:

- Writing visualization code from scratch for the first time — particularly the radar chart, which required manual angle calculation using numpy.linspace and closing the polygon loop
- Handling a wide-format dataset with 1,500+ rows and reshaping it to long format using pd.melt() before any analysis was possible
- Designing a normalization strategy that works fairly across indicators with completely different units and scales
- Deciding which indicators to invert — getting the direction of "good" wrong would corrupt every score silently
- Identifying and fixing a Python string concatenation bug (missing comma) that caused two indicators to escape inversion undetected, producing subtly wrong scores across all decades

### Methodological challenges:

- Selecting 20 indicators from 1,500+ without cherry-picking — balancing data coverage, relevance, and avoiding redundancy
- Assigning weights without a ground truth to validate against — every weight is a judgment call that shapes the final rankings
- Deciding how to handle missing data for early decades without discarding those decades entirely
- Accounting for the fact that some indicators (life expectancy, child mortality) move slowly over time regardless of who is governing

---
## How to Run

**Requirements**
```
pandas
numpy
matplotlib
seaborn
jupyter
```

Install dependencies:
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

Run the notebook:
```bash
jupyter notebook Nigeria_Development_Index.ipynb
```

The notebook runs sequentially from data loading to chart generation. All charts are saved automatically to the project directory.

**Dataset:** Download the Nigeria dataset from the [World Bank WDI portal](https://databank.worldbank.org/source/world-development-indicators) and place it in the project root as `API_NGA.csv`.

---

## Project Structure

```
nigeria-development-index/
│
├── Nigeria_Development_Index.ipynb   ← main analysis notebook
├── API_NGA.csv                       ← World Bank dataset (download separately)
├── README.md
├── requirements.txt
└── charts/
    ├── chart1_decade_composite.png
    ├── chart2_sector_trajectories.png
    ├── chart3_presidential_ranking.png
    ├── chart4_heatmap.png
    └── chart5_radar.png
```

---

## Data Source

World Bank — World Development Indicators (WDI)  
Nigeria dataset downloaded from [databank.worldbank.org](https://databank.worldbank.org/source/world-development-indicators)

---

**Read article on medium**
https://medium.com/@toyeseadelowo/nigeria-development-index-2acf0703cb76

---

*Built with Python · pandas · matplotlib · seaborn*  
*Author: Adelowo Kehinde Adetoyese · 2026*
