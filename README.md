# Customer Segmentation Project

Segments a retail customer base into distinct, actionable groups based on
**demographics** (age, income, tenure) and **behavior** (purchase frequency,
basket size, recency, channel, engagement, satisfaction) using K-Means
clustering.


## The 5 Segments

| # | Name | Size | Key trait |
|---|---|---|---|
| 0 | Young Digital Buyers | 22.5% | Youngest, 80% online, moderate spend |
| 1 | Premium Loyalists | 16.7% | Highest income & spend ($16.5K/yr) — top revenue driver |
| 2 | Budget Regulars | 26.5% | Largest group, low spend, highest satisfaction |
| 3 | Occasional Big Spenders | 17.4% | Big baskets ($216), rare visits — churn risk |
| 4 | Steady Mid-Tier (At Risk) | 16.9% | Long tenure, lowest satisfaction |

Full profiles and recommended actions for each are in the report / notebook.

## How to Use With Your Own Data

1. Replace `customer_data.csv` with your own file (or skip `generate_data.py`
   entirely and load your file directly).
2. Make sure your columns match — or edit the `cluster_features` list near
   the top of `segmentation_analysis.py` (Section 4 in the notebook) to
   point at your own numeric columns.
3. Re-run the script or notebook. Everything downstream (k-selection,
   clustering, charts, profiling) recalculates automatically.

## Running It Yourself

```bash
pip install pandas numpy scikit-learn matplotlib seaborn

# Script version
python generate_data.py          # creates customer_data.csv
python segmentation_analysis.py  # runs the full pipeline, saves charts + segmented CSV

# Notebook version
jupyter notebook Customer_Segmentation_Analysis.ipynb
```

## Method Summary

- **Preprocessing:** median imputation for missing satisfaction scores;
  z-score standardization of 11 numeric features.
- **Model selection:** k evaluated from 2–10 using inertia (elbow method)
  and silhouette score; k=5 chosen for business interpretability and
  balanced cluster sizes (17–27% of the base each).
- **Model:** `sklearn.cluster.KMeans(n_clusters=5, n_init=10, random_state=42)`.
- **Visualization:** PCA (2 components, ~50% combined variance explained)
  for 2D cluster plotting.
