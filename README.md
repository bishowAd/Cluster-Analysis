#  Student Performance Clustering Analysis

An unsupervised machine learning project applying **K-Means** and **Hierarchical Clustering** to student exam data, with a full data science pipeline — from visual exploration and quality checks to dimensionality reduction, discretization, and cluster evaluation.

---

##  Overview

This project analyzes student academic performance data to discover natural groupings among students based on study habits, sleep, attendance, and exam outcomes. The goal is to identify meaningful student profiles without using labeled outcomes, using two classic clustering algorithms evaluated against multiple metrics.

---

## Dataset

**File:** `student_exam_scores.csv`

| Feature | Description |
|---|---|
| `student_id` | Unique student identifier |
| `hours_studied` | Weekly hours spent studying |
| `sleep_hours` | Average nightly sleep hours |
| `attendance_percent` | Class attendance rate (%) |
| `previous_scores` | Prior academic performance score |
| `exam_score` | Final exam score |

---

##  Pipeline

### 1. Visual Exploration
- **Histograms** for each numeric feature
- **Box-Whisker plots** to spot spread and outliers
- **Violin plots** for distribution shape
- **Pairplot (scatter matrix)** for pairwise relationships
- Summary statistics: mean, median, std, skewness, kurtosis

### 2. Data Quality & Cleaning
- Missing value check
- Duplicate `student_id` removal
- **IQR-based outlier detection** per feature (with bounds and counts reported)

### 3. Handling Redundancy
- **Chi-Square test** between `attendance_level` and `sleep_hours` to check feature independence
- **Correlation heatmap** (Seaborn) across all numeric features

### 4. Dimensionality Reduction — PCA
- StandardScaler normalization before PCA
- Scree plot and cumulative variance plot
- 95% variance threshold evaluated

### 5. Discretization
Features binned into Low / Medium / High:

| Feature | Bins |
|---|---|
| `hours_studied` | 0–3, 3–6, 6–10 |
| `sleep_hours` | 0–5, 5–7, 7–10 |
| `previous_scores` | 0–60, 60–80, 80–100 |
| `exam_score` | 33rd / 67th percentile splits |

- Bar charts for each discretized distribution
- Chi-Square tests for all discretized feature pairs (e.g., `hours_studied_binned` vs `exam_score_binned`)
- Jittered scatter matrix of discretized features

### 6. Feature Standardization
All five features standardized with `StandardScaler` before clustering.

---

##  Clustering Methods

### K-Means (k=3)
- `n_init=10`, `random_state=42`
- Visualized across 4 feature pairs vs exam score
- Cluster summary statistics (mean ± std per feature)

### Hierarchical Clustering (k=3)
- Ward linkage (`AgglomerativeClustering`)
- Dendrogram generated via SciPy

---

## Evaluation Metrics

| Metric | K-Means | Hierarchical |
|---|---|---|
| Silhouette Score | — | — |
| Davies-Bouldin Index | — | — |
| Calinski-Harabasz Index | — | — |

> *Scores populate when the notebook is run. Higher Silhouette and Calinski-Harabasz scores are better; lower Davies-Bouldin is better.*

---

##Tech Stack

| Tool | Purpose |
|---|---|
| Python | Core language |
| Pandas / NumPy | Data manipulation |
| Matplotlib / Seaborn | Visualization |
| Scikit-learn | PCA, clustering, evaluation metrics |
| SciPy | Dendrogram / linkage |

---

##etting Started

### 1. Clone the repo

```bash
git clone https://github.com/bishowAd/<repo-name>.git
cd <repo-name>
```

### 2. Install dependencies

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy
```

### 3. Add the dataset

Place `student_exam_scores.csv` in the project root directory.

### 4. Run the notebook

Open `project_cluster.ipynb` in Jupyter and run all cells top to bottom.

---

# roject Structure

```
clustering-analysis/
├── project_cluster.ipynb     # Main analysis notebook
├── student_exam_scores.csv   # Dataset (not included in repo)
└── README.md                 # You are here
```

---

# References

- Pedregosa et al. — *Scikit-learn: Machine Learning in Python*, JMLR 12, 2011
- Jake VanderPlas — *Python Data Science Handbook*
- Tan, Steinbach, Karpatne, Kumar — *Introduction to Data Mining*, 2nd Ed., Morgan Kaufmann, 2011

---
