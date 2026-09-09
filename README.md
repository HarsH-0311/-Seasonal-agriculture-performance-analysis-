# Seasonal Agriculture Performance Analysis

A data analytics project investigating how agricultural performance — yield, profitability, and resource use — varies across India's three farming seasons (Kharif, Rabi, Zaid), using 4,000 farm-level records across 8 states.


## Problem Statement

Agricultural performance is shaped by seasonal variation in rainfall, temperature, humidity, and farming practices, but raw farm-level records don't clearly show how yield, profitability, and resource use actually change from one season to another. This project analyzes seasonal patterns statistically, tests whether the observed differences are significant, and translates the findings into evidence-based agricultural planning recommendations.

## Dataset

- **4,000 records** across **8 states** (Andhra Pradesh, Gujarat, Karnataka, Madhya Pradesh, Maharashtra, Punjab, Tamil Nadu, Telangana)
- **3 seasons:** Kharif, Rabi, Zaid
- Multiple crops, with environmental (rainfall, temperature, humidity, soil), resource (fertilizer, pesticide, water efficiency), and economic (revenue, cost, profit) variables per farm

## Methodology

1. **Data cleaning** — group-wise (Season × Crop) median imputation for missing environmental values; IQR-based outlier capping (winsorization) rather than deletion, to preserve sample size
2. **Feature engineering** — profit margin, cost/revenue/profit per hectare, profitability flag
3. **Exploratory analysis** — season-wise distributions of yield, profit, and resource use; state × season and crop × season breakdowns
4. **Statistical testing** — ANOVA and Kruskal-Wallis (parametric + non-parametric) to test whether seasonal differences are significant
5. **Correlation analysis** — environmental and resource factors vs. yield and profit
6. **Anomaly detection** — high-rainfall/low-yield outlier cases

## Key Findings

| Metric | Kharif | Rabi | Zaid |
|---|---|---|---|
| Avg. Yield (t/ha) | 5.50 | 5.03 | 4.64 |
| Avg. Profit (₹) | 178,915 | 87,689 | **-24,805** |
| Farms at a loss | 42.2% | 51.1% | **64.5%** |
| Rainfall (mm) | 852 | 436 | 299 |

- **Kharif is the strongest season** — highest yield, highest profit, lowest loss rate.
- **Zaid is the weakest season** — the only season with negative average profit, and nearly two-thirds of its farms lose money, driven by low rainfall and the lowest water-use efficiency of the three seasons.
- **Water-use efficiency, not rainfall volume, is the strongest driver of yield** (r = 0.93) — far ahead of any environmental variable, including rainfall itself (r = 0.03).
- **The best season is not uniform across states** — most states peak in Kharif, but Karnataka peaks in Zaid and Maharashtra/Punjab peak in Rabi, meaning state-level (not just season-level) recommendations are needed.
- Statistical testing (ANOVA + Kruskal-Wallis) confirms profit, revenue, water efficiency, and disease/pest risk differ significantly by season; for Yield specifically, the two tests disagree (ANOVA not significant, Kruskal-Wallis significant), which is discussed in the notebook as a sign of skewed, non-normal yield data.

## Recommendations

- Prioritize crop insurance and irrigation-efficiency support for **Zaid-season** farms, where losses are most severe.
- Promote water-use efficiency (drip/sprinkler irrigation, scheduling) over simply increasing water access.
- Localize seasonal advisories by state rather than issuing a single national recommendation.
- Investigate an excess-rainfall threshold for Kharif, where high-rainfall/low-yield anomalies cluster.

## Repository Contents

```
├── Seasonal_Agriculture_Performance_Analysis.ipynb   # Full analysis notebook
├── seasonal_agriculture_performance_dataset.csv      # Source dataset
├── Seasonal_Agriculture_Performance_Analysis_PPT.pptx # Project presentation
├── requirements.txt                                   # Python dependencies
└── README.md
```

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook Seasonal_Agriculture_Performance_Analysis.ipynb
```

Run all cells top to bottom (**Kernel → Restart & Run All**) to reproduce every table, chart, and statistical test in the notebook.

## Tech Stack

- Python 3, Jupyter Notebook
- Pandas, NumPy — data cleaning & feature engineering
- Matplotlib, Seaborn — visualization
- SciPy (`scipy.stats`) — ANOVA & Kruskal-Wallis significance testing

## Author

Harsh Hedaoo
