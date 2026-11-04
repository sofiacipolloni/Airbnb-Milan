# Who really rents Milan on Airbnb? — reproducible analysis

Sofia Cipolloni · Laura Ferri — Scientific Data Visualization, 11 November 2026

## What is in this folder

| Item | What it is |
|---|---|
| `airbnb_milan_analysis.ipynb` | The whole analysis, already run: Part A computes every number in the slides, Part B draws every chart. |
| `data/listings.csv` | Inside Airbnb, Milan, snapshot of 21 September 2026 (the exact file we used). |
| `fonts/` | The Inter font used in the charts (SIL Open Font License); the notebook registers it automatically. |
| `figures/` | The charts, named after their slide (`slide08_h_dendro_col.png` …); `extra_` = tested but not shown in the deck. |
| `results/` | Intermediate tables written by the notebook (cleaned measures, PCA, clusters, tests, model outputs). |
| `requirements.txt` | Exact package versions. |

## How to run it

```bash
python -m venv .venv && source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab airbnb_milan_analysis.ipynb                  # then Kernel → Restart & Run All
```

It takes a few minutes (about 3 on our machine). Run it from this folder: the paths (`data/`, `fonts/`, `results/`, `figures/`) are relative.

## Reproducibility

* Every random step uses the seed 2026, so cluster labels, bootstrap values, test results and charts come out the same at every run.
* With the versions in `requirements.txt` the charts are pixel-identical to those in the presentation. With different versions of scikit-learn the neural network's AUC may move in the third decimal.
* Hypothesis tests were run on **all seven** held-out variables (Superhost, guest rating, CIN licence code, latitude, longitude, neighbourhood, room type — latitude and longitude combined into the distance from the Duomo). The slides show four of them; the full table is printed in section A7 and the other charts are saved as `extra_*`.
