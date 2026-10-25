# University coursework — data & ML projects

This repository collects **assignments and mini-projects from my university courses** in data science, machine learning, and analytics. Each folder entry is a self-contained notebook or script: exploratory analysis, models, and sometimes dashboards or pipelines tied to real (or realistic) datasets.

---

## Projects at a glance

| Project | Focus | Stack (high level) |
|--------|--------|-------------------|
| **Anomaly detection in network security** | Unsupervised learning on firewall-style traffic logs | `pandas`, `scikit-learn` (K-Means, DBSCAN, PCA), `seaborn` / `matplotlib` |
| **Hotel reviews — sentiment & scraping** | Text data, labeling, and optional web scraping | `pandas`, Kaggle data, Selenium (Agoda), classical ML in `hotels0.py` |
| **Sentiment analysis (LSTM, PyTorch)** | Deep learning for review sentiment | `PyTorch`, LSTM, plus optional **Dask** + **MongoDB** pipeline in the notebook |
| **Wildfire area predictions** | Regression on weather features + multi-region forecast API | `pymongo`, **Weatherbit** API, `sklearn` linear regression, **Plotly** treemap |
| **Asylum seekers — multiview dashboard** | Exploratory / policy-oriented visualization | **Tableau** (exported view below) |

---

## Anomaly detection in network security

**Goal:** Treat network log features (ports, bytes, packets, actions) as vectors, normalize and encode them, then **cluster** traffic to surface unusual groups.

**What it does:**

- Loads a CSV of log-like records (`log2.csv` in the original workflow), checks consistency (e.g. totals vs. components), and explores the distribution of actions.
- Applies **MinMax scaling** and one-hot encoding where needed, then uses **K-Means** (with elbow and **PCA** 2D plots) and **DBSCAN** for density-based clusters.
- Reports **silhouette** and **Davies–Bouldin** style diagnostics to compare clustering quality.

This is a typical **unsupervised learning** lab: you interpret clusters rather than predicting a single “attack” label from a static dataset.

---

## Hotel reviews (`hotels.ipynb` / `hotels0.py`)

**Goal:** Work with **large-scale review text**: combine positive and negative review columns from a public hotel dataset, optionally augment with **Agoda** reviews scraped via **Selenium**, and build features for sentiment-related tasks.

**What it does:**

- Merges positive and negative reviews into one table with a binary **positive / negative** indicator.
- Demonstrates an end-to-end path from **CSV discovery** to **targeted scraping** (paths and drivers are environment-specific in the script—adjust before running).

Use this as a template for **NLP data prep** and **weak supervision** from ratings.

---

## Sentiment analysis — LSTM with PyTorch (`sentiment-analysis-lstm-pytorch.ipynb`)

**Goal:** Classify sentiment on review text using a **neural** model instead of bag-of-words alone.

**What it does:**

- Trains an **LSTM** in **PyTorch** on review data.
- The notebook also sketches a **big-data style** path: load CSV with **Dask**, push to **MongoDB** with `dask-mongo`, and read back for analysis (connection strings in the notebook must be configured locally).

---

## Wildfire predictions (`wildfire predictions.py`)

**Goal:** Relate **weather and environmental** inputs to **estimated fire area**, then use a trained **linear regression** model to score **forecast** weather from an API across **Australian regions**.

**What it does:**

- Optionally pulls historical rows from **MongoDB**; merges with CSV-based training data.
- Calls the **Weatherbit** daily forecast API for several lat/long points (NSW, NT, QLD, SA, TAS, VIC, WA).
- Outputs predictions and a **Plotly** treemap of regional averages, with **RMSE** and **R²** in the title for a quick sanity check.

> **Note:** API keys and Mongo URIs in scripts are placeholders or secrets—**rotate keys** and use environment variables before sharing or re-running publicly.

---

## Visualization — asylum seekers (Tableau)

A **multiview Tableau** workbook summarizes asylum-related indicators; the snapshot below is the image exported from that dashboard.

![Multiview Tableau dashboard — asylum seekers](Multiview%20Tableau%20Asylum%20Seekers.png)

This piece is pure **visual analytics**: filters, small multiples, and composition to compare categories and trends at a glance.

---

## How to run these

1. **Python:** Use Python 3.x with the packages each script imports (`pandas`, `scikit-learn`, `torch`, etc.). Notebooks expect Jupyter or VS Code.
2. **Data & secrets:** Several projects assume local CSV files, API keys, or database URIs—configure those before execution.
3. **Browsers / Selenium:** Hotel scraping requires a matching ChromeDriver and valid URL list.

---

## License & context

Coursework artifacts are shared for **portfolio and learning** purposes. If you reuse ideas or code, cite the course context and adapt credentials, data paths, and dependencies to your own environment.
