# Marketing Campaign Data Pipeline

An end-to-end project on a real-world messy marketing dataset.
Covers data cleaning, SQL analytics, EDA, and predictive modeling.

---

## Overview

Raw marketing campaign data is rarely clean. This project takes a messy
2020-row dataset with currency symbols, typos, mixed booleans, duplicate
columns, and logical errors — and transforms it into an analytics-ready
database with actionable insights.

---

## Pipeline Steps

|           Step             |                     Description                            |
|----------------------------|------------------------------------------------------------|
| 1. Header Cleaning         | Normalized column names (strip, lowercase, replace spaces) |
| 2. Currency Parsing        | Removed $ symbols, converted spend to float using regex    |
| 3. Categorical Typos       | Fixed misspelled channel names using a fuzzy cleanup map   |
| 4. Boolean Standardization | Unified Y/N/Yes/No/True/1 → consistent bool dtype          |
| 5. Date Parsing            | Converted date strings to datetime64                       |
| 6. Duplicate Columns       | Detected and removed duplicate 'clicks' column             |
| 7. Logical Integrity       | Flagged campaigns where clicks > impressions               |
| 8. Outlier Handling        | Winsorized extreme spend values using IQR method           |
| 9. Feature Extraction      | Extracted season from campaign_name using regex            |

---

## EDA Highlights

- **Facebook** had the highest total ad spend across all channels
- **Launch** campaigns had the highest average ROI by season
- **Clicks and conversions** were strongly correlated (r = 0.86)
- **Campaign duration** had near-zero correlation with performance

---

## SQL Analytics

Loaded cleaned data into SQLite and ran business queries including:
- Channel performance summary (spend, conversions, ROI)
- Top 10 most efficient campaigns by ROI
- Best channel per season breakdown
- Active vs inactive campaign comparison

---

## ML Model

**Target:** Predict number of conversions per campaign
**Model:** Linear Regression (scikit-learn)
**Features:** spend, impressions, duration, CTR, channel, season
**Result:** R² = 0.70 on held-out test set

The model explains 70% of variance in conversions. Feature importance
analysis showed impressions and spend as the strongest predictors.

---

## Tech Stack

- Python (pandas, numpy, sklearn, seaborn, matplotlib)
- SQL (SQLite via sqlite3)
- Regex
- Google Colab

---

## Files

|               File                  |              Description                  |
|-------------------------------------|-------------------------------------------|
| `marketing_campaign_data_messy.csv` | Raw input dataset                         |
| `marketing_pipeline.ipynb`          | Full notebook (cleaning → EDA → SQL → ML) |

---

## Key Takeaways

- Real-world data requires systematic, documented cleaning before analysis
- SQL and Python complement each other well for analytics pipelines
- Even after thorough cleaning, 30% of conversion variance is unexplained —
  likely due to factors outside the dataset (ad creative, targeting, etc.)