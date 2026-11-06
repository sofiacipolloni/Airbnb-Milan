# Who really rents Milan on Airbnb?

## The data

[Inside Airbnb](https://insideairbnb.com) publishes a snapshot of every Airbnb listing in a city. We use **Milan on 21 September 2026**: 25,338 listings from 11,475 hosts, with 90 columns describing the home (guests, bedrooms, beds, bathrooms, amenities), the price and the minimum stay, availability, reviews, the host (number of listings, years on Airbnb, Superhost badge), the CIN licence code, the position and the room type. After cleaning, the analysis covers 21,510 entire homes and private rooms.

## The goals

We want to find out who actually rents out Milan on Airbnb, through six questions:

1. **Types.** Do Milan listings fall into distinct types? (PCA, hierarchical clustering, k-means, bootstrap stability)
2. **Profiles.** What is each type like?
3. **Trust.** Do the types differ in Superhost badge, guest rating and CIN licence code? (hypothesis tests on variables the clustering never saw)
4. **Place.** Are the types spread differently across Milan? (distance from the Duomo, neighbourhoods, maps)
5. **Prediction.** Can the listing alone predict a Superhost? (logistic regression vs neural network)
6. **Time.** Is the market growing, and who drives the growth?

## What is in this folder

| Item | What it is |
|---|---|
| `airbnb_milan_analysis.ipynb` | The analysis: Part A computes and prints the results, Part B draws the charts. |
| `data/listings.csv` | The Inside Airbnb file for Milan, 21 September 2026. |
| `fonts/` | The Inter font used in the charts (SIL Open Font License), registered by the notebook. |
| `results/` | Intermediate tables written by the notebook (cleaned measures, PCA, clusters, tests, model outputs). |
| `figures/` | The charts, numbered by phase: `01_eda_…`, `02_pca_…`, `03_hclust_…`, `04_kmeans_…`, `05_bootstrap_…`, `06_types_…`, `07_test_…`, `08_superhost_…`, `09_time_…`. |
| `requirements.txt` | Package versions. |

## How to run it

```bash
python -m venv .venv && source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab airbnb_milan_analysis.ipynb                  # then Kernel → Restart & Run All
```

Run it from this folder, since the paths (`data/`, `fonts/`, `results/`, `figures/`) are relative. It takes a few minutes.
