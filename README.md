# Who really rents Milan on Airbnb?

## Overview

### Data
[Inside Airbnb](https://insideairbnb.com) snapshot of Milan on **21 September 2026**: 25,338 listings from 11,475 hosts, 90 columns. After removing shared and hotel rooms, listings with no price on the day and implausible prices (below 20 € or above 2,000 €), the analysis covers **21,510 entire homes and private rooms**.

Variables are split in two blocks:
- **11 measures used to find the types**: size (guests, bedrooms, beds, bathrooms, amenities), price, use (minimum nights, days available, reviews in the last 12 months), host (number of listings, years on Airbnb).
- **7 variables held out to test them**, never shown to the clustering: Superhost badge, guest rating, CIN licence code, latitude, longitude, neighbourhood, room type.

### Questions
1. Do Milan listings fall into distinct types?
2. What is each type like?
3. Do the types differ in hosting quality and licence compliance?
4. Are the types spread differently across Milan?
5. Can the listing alone predict a Superhost?
6. Is the market growing, and who drives it?

### Main results
1. **Four types**, found with PCA (4 components, 66% of the variance), Ward hierarchical clustering and k-means. They are real (silhouette 0.27 vs 0.18 on shuffled data) and stable (bootstrap ARI 0.98), with soft borders.
2. **Active hosts** (45%), **large flats** (16%), **property managers** (25%), **monthly rentals** (14%).
3. Managers are rarely Superhosts (18% vs 45% of active hosts); monthly rentals rarely show the CIN code (29% vs over 90% for the other types).
4. Managers concentrate near the Duomo, monthly rentals at the edge; pricier neighbourhoods have more managers (Spearman ρ = 0.73).
5. On hosts never seen in training, a neural network reaches AUC 0.83 vs 0.81 for logistic regression. The more listings a host has, the lower the chance of being a Superhost.
6. 81% of today's listings entered the market in 2022 or later. The share of new listings from hosts with 11+ listings rose from 8% (2015) to 45% (2026).

### Limitations and future work
- **One day only.** The snapshot shows only listings still active in September 2026, so earlier years are underestimated. Several snapshots over time would allow a true panel analysis.
- **Reviews are not bookings**, and the first review is only a proxy for when a listing entered the market.
- **Asking prices**, not prices actually paid.
- **Listings of the same host are not independent.** Handled with host-clustered errors and a host-based train/test split.
- **Moderate cluster structure**: soft borders between types. Fuzzy or model-based clustering could assign listings to more than one type.

---

## How to run it

### Folder contents

| Item | What it is |
|---|---|
| `airbnb_milan_analysis.ipynb` | The analysis: Part A computes and prints the results, Part B draws the charts. |
| `data/listings.csv` | Inside Airbnb file for Milan, 21 September 2026. |
| `fonts/` | Inter font used in the charts (SIL Open Font License), registered by the notebook. |
| `results/` | Intermediate tables written by the notebook. |
| `figures/` | Charts numbered by phase: `01_eda_…`, `02_pca_…`, `03_hclust_…`, `04_kmeans_…`, `05_bootstrap_…`, `06_types_…`, `07_test_…`, `08_superhost_…`, `09_time_…`. |
| `requirements.txt` | Package versions. |
| `presentation.pdf` | The slides presenting the results. |

### Steps

```bash
python3 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab airbnb_milan_analysis.ipynb
```

Then **Kernel → Restart & Run All**. Run it from this folder, since all paths are relative. All random steps use the seed 2026, and the full run takes a few minutes.